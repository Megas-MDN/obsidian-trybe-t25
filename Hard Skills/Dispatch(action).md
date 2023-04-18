[[Redux]]
[[React]]
[[Actions]]

Para enviar uma `action` para o `reducer` é necessário passá-la como argumento para a função `dispatch()`.

```jsx
dispatch({type: 'INCREMENT_COUNTER'});
```

`Dispatch` é uma função do Redux. Você chama `store.dispatch` para despachar uma ação. Esta é a única maneira de acionar uma mudança de estado. 
Com o React Redux, seus componentes nunca acessam a store diretamente - `connect` faça isso por você. O React Redux oferece duas maneiras de permitir que os componentes despachem ações:

-   Por padrão, um componente conectado recebe `props.dispatch` e pode despachar ações por conta própria.
-   `connect` pode aceitar um argumento chamado `mapDispatchToProps`, que permite criar funções que despacham quando chamadas e passam essas funções como props para seu componente.

As `mapDispatchToProps` funções são normalmente chamadas de `mapDispatch`abreviações, mas o nome da variável real usado pode ser o que você quiser.

### Padrão: `dispatch` como um Prop

Se você não especificar o segundo argumento para `connect()`, seu componente receberá `dispatch`por padrão. Por exemplo:

```jsx
connect()(MyComponent)  
// which is equivalent with  
connect(null, null)(MyComponent)  
  
// or  
connect(mapStateToProps /** no second argument */)(MyComponent)
```

Depois de conectar seu componente dessa maneira, seu componente recebe `props.dispatch`. Você pode usá-lo para despachar ações para a loja.

```jsx
function Counter({ count, dispatch }) {  
	return (  
		<div>  
			<button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>  
			<span>{count}</span>  
			<button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>  
			<button onClick={() => dispatch({ type: 'RESET' })}>reset</button>  
		</div>  
	)  
}
```

### Fornecendo um parâmetro `mapDispatchToProps`

Fornecer um `mapDispatchToProps`permite especificar quais ações seu componente pode precisar despachar. Ele permite que você forneça funções de despacho de ação como adereços. Portanto, em vez de ligar para `props.dispatch(() => increment())`, você pode ligar `props.increment()`diretamente. Existem algumas razões pelas quais você pode querer fazer isso.

Primeiro, encapsular a lógica de despacho na função torna a implementação mais declarativa. Despachar uma ação e deixar o armazenamento do Redux lidar com o fluxo de dados é _como_ implementar o comportamento, e não _o que_ ele faz.

Um bom exemplo seria despachar uma ação quando um botão é clicado. Conectar o botão diretamente provavelmente não faz sentido conceitualmente, e nem ter a referência do botão `dispatch`.

```jsx
// button needs to be aware of "dispatch"  
<button onClick={() => dispatch({ type: "SOMETHING" })} />  
  
// button unaware of "dispatch",  
<button onClick={doSomething} />
```

Depois de agrupar todos os nossos criadores de ação com funções que despacham as ações, o componente fica livre da necessidade de arquivos `dispatch`. Portanto, **se você definir seu próprio `mapDispatchToProps`, o componente conectado não receberá mais `dispatch`.**

#### Lógica de despacho de ação de passagem para [componentes](https://react-redux.js.org/using-react-redux/connect-mapdispatch#pass-down-action-dispatching-logic-to--unconnected--child-components "Link direto para o título")

Além disso, você também ganha a capacidade de passar as funções de despacho de ação para componentes filho (provavelmente desconectados). Isso permite que mais componentes despachem ações, mantendo-os "inconscientes" do Redux.

```jsx
// pass down toggleTodo to child component  
// making Todo able to dispatch the toggleTodo action  
const TodoList = ({ todos, toggleTodo }) => (  
	<div>  
		{todos.map((todo) => (  
			<Todo todo={todo} onClick={toggleTodo} />  
		))}  
	</div>  
)
```

Isso é o que o React Redux `connect` faz - ele encapsula a lógica de falar com a loja Redux e permite que você não se preocupe com isso. E é isso que você deve usar totalmente em sua implementação.

## Duas formas `mapDispatchToProps`

O `mapDispatchToProps` parâmetro pode ser de duas formas. Enquanto o formulário de função permite mais personalização, o formulário de objeto é fácil de usar.

-   **Formulário de função** : Permite mais personalização, acesso `dispatch` e opcionalmente `ownProps`
-   **Formulário abreviado de objeto** : mais declarativo e mais fácil de usar

> ⭐ **Observação:** Recomendamos usar o formulário de objeto de `mapDispatchToProps`, a menos que você precise personalizar especificamente o comportamento de despacho de alguma forma.

## Definindo `mapDispatchToProps` como uma [função](https://react-redux.js.org/using-react-redux/connect-mapdispatch#defining-mapdispatchtoprops-as-a-function "Link direto para o título")

Definir `mapDispatchToProps`como uma função oferece mais flexibilidade na personalização das funções que seu componente recebe e como elas despacham ações. Você ganha acesso a `dispatch`e `ownProps`. Você pode usar essa chance para escrever funções personalizadas para serem chamadas por seus componentes conectados.

### [Argumentos](https://react-redux.js.org/using-react-redux/connect-mapdispatch#arguments "Link direto para o título")

1.  **`dispatch`**
2.  **`ownProps` (opcional)**

**`dispatch`**

A `mapDispatchToProps` função será chamada com `dispatch`o primeiro argumento. Você normalmente fará uso disso retornando novas funções que chamam `dispatch()`dentro de si mesmas e passam diretamente um objeto de ação simples ou passa o resultado de um criador de ação.

```jsx
const mapDispatchToProps = (dispatch) => {  
	return {  
		// dispatching plain actions  
		increment: () => dispatch({ type: 'INCREMENT' }),  
		decrement: () => dispatch({ type: 'DECREMENT' }),  
		reset: () => dispatch({ type: 'RESET' }),  
	}  
}
```

Você provavelmente também desejará encaminhar argumentos para seus criadores de ação:

```jsx
const mapDispatchToProps = (dispatch) => {  
	return {  
		// explicitly forwarding arguments  
		onClick: (event) => dispatch(trackClick(event)),  
  
		// implicitly forwarding arguments  
		onReceiveImpressions: (...impressions) =>  
			dispatch(trackImpressions(impressions)),  
	}  
}
```

**`ownProps` (opcional)**

Se sua `mapDispatchToProps` função for declarada como tendo dois parâmetros, ela será chamada `dispatch` como o primeiro parâmetro e `props` passada para o componente conectado como o segundo parâmetro, e será invocada novamente sempre que o componente conectado receber novas props.

Isso significa que, em vez de religar new `props` para action dispatchers na re-renderização do componente, você pode fazer isso quando o seu componente for `props` alterado.

**Ligações na montagem do componente**

```jsx
render() {  
	return <button onClick={() => this.props.toggleTodo(this.props.todoId)} />  
}  
  
const mapDispatchToProps = dispatch => {  
	return {  
		toggleTodo: todoId => dispatch(toggleTodo(todoId))  
	}  
}
```

**Vinculações na `props` mudança**

```jsx
render() {  
	return <button onClick={() => this.props.toggleTodo()} />  
}  
  
const mapDispatchToProps = (dispatch, ownProps) => {  
	return {  
		toggleTodo: () => dispatch(toggleTodo(ownProps.todoId))  
	}  
}
```

### [Retornar](https://react-redux.js.org/using-react-redux/connect-mapdispatch#return "Link direto para o título")

Sua `mapDispatchToProps` função deve retornar um objeto simples:

-   Cada campo no objeto se tornará um prop separado para seu próprio componente, e o valor normalmente deve ser uma função que despacha uma ação quando chamada.
-   Se você usar criadores de ação (em oposição a ações de objeto simples) dentro `dispatch` de , é uma convenção simplesmente nomear a chave de campo com o mesmo nome do criador da ação:

```jsx
const increment = () => ({ type: 'INCREMENT' })  
const decrement = () => ({ type: 'DECREMENT' })  
const reset = () => ({ type: 'RESET' })  
  
const mapDispatchToProps = (dispatch) => {  
	return {  
		// dispatching actions returned by action creators  
		increment: () => dispatch(increment()),  
		decrement: () => dispatch(decrement()),  
		reset: () => dispatch(reset()),  
	}  
}
```

O retorno da `mapDispatchToProps` função será mesclado ao seu componente conectado como props. Você pode chamá-los diretamente para despachar sua ação.

```jsx
function Counter({ count, increment, decrement, reset }) {  
	return (  
		<div>  
			<button onClick={decrement}>-</button>  
			<span>{count}</span>  
			<button onClick={increment}>+</button>  
			<button onClick={reset}>reset</button>  
		</div>  
	)  
}
```

(O código completo do exemplo Counter está [neste CodeSandbox](https://codesandbox.io/s/yv6kqo1yw9) )

### Definindo a `mapDispatchToProps` função `bindActionCreators`

Embrulhar essas funções manualmente é tedioso, então o Redux fornece uma função para simplificar isso.

> `bindActionCreators`transforma um objeto cujos valores são [criadores de ação](https://redux.js.org/glossary#action-creator) , em um objeto com as mesmas chaves, mas com todos os criadores de ação envolvidos em uma [`dispatch`](https://redux.js.org/api/store#dispatch)chamada para que possam ser invocados diretamente. Veja [Redux Docs em`bindActionCreators`](https://redux.js.org/api/bindactioncreators)

`bindActionCreators` aceita dois parâmetros:

1.  A **`function`** (um criador de ação) ou um **`object`** (cada campo um criador de ação).
2.  `dispatch`

As funções de wrapper geradas por `bindActionCreators`encaminharão automaticamente todos os seus argumentos, portanto, você não precisa fazer isso manualmente.

```jsx
import { bindActionCreators } from 'redux'  
  
const increment = () => ({ type: 'INCREMENT' })  
const decrement = () => ({ type: 'DECREMENT' })  
const reset = () => ({ type: 'RESET' })  
  
// binding an action creator  
// returns (...args) => dispatch(increment(...args))  
const boundIncrement = bindActionCreators(increment, dispatch)  
  
// binding an object full of action creators  
const boundActionCreators = bindActionCreators(  
	{ increment, decrement, reset },  
	dispatch  
)  
// returns  
// {  
// increment: (...args) => dispatch(increment(...args)),  
// decrement: (...args) => dispatch(decrement(...args)),  
// reset: (...args) => dispatch(reset(...args)),  
// }
```

Para usar `bindActionCreators` em nossa `mapDispatchToProps` função:

```jsx
import { bindActionCreators } from 'redux'  
// ...  
  
function mapDispatchToProps(dispatch) {  
return bindActionCreators({ increment, decrement, reset }, dispatch)  
}  
  
// component receives props.increment, props.decrement, props.reset  
connect(null, mapDispatchToProps)(Counter)
```

### [Injetando](https://react-redux.js.org/using-react-redux/connect-mapdispatch#manually-injecting-dispatch "Link direto para o título") manualmente `dispatch` 

Se o `mapDispatchToProps` argumento for fornecido, o componente não receberá mais o padrão `dispatch`. Você pode trazê-lo de volta adicionando-o manualmente ao retorno do seu `mapDispatchToProps`, embora na maioria das vezes você não precise fazer isso:

```
import { bindActionCreators } from 'redux'// ...function mapDispatchToProps(dispatch) {  return {    dispatch,    ...bindActionCreators({ increment, decrement, reset }, dispatch),  }}
```

cópia de

## Definindo `mapDispatchToProps` como um [objeto](https://react-redux.js.org/using-react-redux/connect-mapdispatch#defining-mapdispatchtoprops-as-an-object "Link direto para o título")

Você viu que a configuração para despachar ações Redux em um componente React segue um processo muito semelhante: defina um criador de ação, envolva-o em outra função que se pareça com `(…args) => dispatch(actionCreator(…args))`, e passe essa função wrapper como um suporte para seu componente.

Por ser tão comum, `connect` suporta uma forma de “objeto abreviado” para o `mapDispatchToProps` argumento: se você passar um objeto cheio de criadores de ação em vez de uma função, `connect` automaticamente chamará `bindActionCreators` por você internamente.

**Recomendamos sempre usar a forma "taquigrafia de objeto" de `mapDispatchToProps`, a menos que você tenha um motivo específico para personalizar o comportamento de despacho.**

Observe que:

-   Cada campo do `mapDispatchToProps` objeto é considerado um criador de ação
-   Seu componente não receberá mais `dispatch`como prop

```jsx
// React Redux does this for you automatically:  
;(dispatch) => bindActionCreators(mapDispatchToProps, dispatch)
```

Portanto, nosso `mapDispatchToProps` pode ser simplesmente:

```jsx
const mapDispatchToProps = {  
increment,  
decrement,  
reset,  
}
```

Como o nome real da variável depende de você, você pode querer dar a ela um nome como `actionCreators`, ou até mesmo definir o objeto embutido na chamada para `connect`:

```jsx
import { increment, decrement, reset } from './counterActions'  
  
const actionCreators = {  
	increment,  
	decrement,  
	reset,  
}  
  
export default connect(mapState, actionCreators)(Counter)  
  
// or  
export default connect(mapState, { increment, decrement, reset })(Counter)
```

## [Problemas](https://react-redux.js.org/using-react-redux/connect-mapdispatch#common-problems "Link direto para o título") comuns

### Por que meu componente não está recebendo ? `dispatch`

Também conhecido como

```jsx
TypeError: this.props.dispatch is not a function
```

Este é um erro comum que acontece quando você tenta chamar `this.props.dispatch`, mas `dispatch`não é injetado em seu componente.

`dispatch` é injetado em seu componente _somente_ quando:

**1. Você não fornece `mapDispatchToProps`**

O padrão `mapDispatchToProps` é simplesmente `dispatch => ({ dispatch })`. Se você não fornecer `mapDispatchToProps`, `dispatch`será fornecido conforme mencionado acima.

Em outras palavras, se você fizer:

```jsx
// component receives `dispatch`  
connect(mapStateToProps /** no second argument*/)(Component)
```

**2. Seu `mapDispatchToProps` retorno de função personalizado contém especificamente `dispatch`**

Você pode trazer de volta `dispatch` fornecendo sua `mapDispatchToProps` função personalizada:

```jsx
const mapDispatchToProps = (dispatch) => {  
	return {  
		increment: () => dispatch(increment()),  
		decrement: () => dispatch(decrement()),  
		reset: () => dispatch(reset()),  
		dispatch,  
	}  
}
```

Ou alternativamente, com `bindActionCreators`:

```jsx
import { bindActionCreators } from 'redux'  
  
function mapDispatchToProps(dispatch) {  
	return {  
		dispatch,  
		...bindActionCreators({ increment, decrement, reset }, dispatch),  
	}  
}
```

Veja [este erro em ação na edição #255 do GitHub do Redux](https://github.com/reduxjs/react-redux/issues/255) .

Há discussões sobre fornecer `dispatch` aos seus componentes quando você especifica `mapDispatchToProps`( [resposta de Dan Abramov para #255](https://github.com/reduxjs/react-redux/issues/255#issuecomment-172089874) ). Você pode lê-los para entender melhor a intenção de implementação atual.

### Posso `mapDispatchToProps` sem `mapStateToProps` no Redux ?

Sim. Você pode pular o primeiro parâmetro passando `undefined` ou `null`. Seu componente não se inscreverá na loja e ainda receberá as props de expedição definidas por `mapDispatchToProps`.

```jsx
connect(null, mapDispatchToProps)(MyComponent)
```


### Posso ligar `store.dispatch`

É um anti-padrão interagir com a loja diretamente em um componente React, seja uma importação explícita da loja ou acessando-a via contexto (veja a [entrada Redux FAQ na configuração da loja](https://redux.js.org/faq/storesetup#can-or-should-i-create-multiple-stores-can-i-import-my-store-directly-and-use-it-in-components-myself) para mais detalhes). Deixe o React Redux `connect` lidar com o acesso à loja e use o `dispatch` que ele passa para os adereços para despachar ações.


###### Fonte: https://react-redux.js.org/using-react-redux/connect-mapdispatch