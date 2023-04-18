[[React]]
[[State]]
[[Funções]]


# Peças do Redux

Para criarmos o Redux, precisamos nos familiarizar com os conceitos de: `store`, `reducer` e `actions` bem como a _função para ler o estado_ `getState()` e a função _para escrever o estado_ `dispatch()`.

Para exemplificar a aula de hoje, iremos criar um contador simples com Javascript puro e Redux.


## Criando o Estado Global - store

Podemos considerar a `store` como sendo o _estado global_. É onde o estado da sua aplicação fica registrado e protegido.

Ela é um _objeto_ que traz as funções `getState()`, para ler do estado, e `dispatch()` , para escrever no estado.

Para criar a `store` da sua aplicação, você deverá usar a função `createStore()` do Redux, passando como argumento uma função `reducer` (que veremos a seguir):

```jsx
// Criando a nossa store:
const store = createStore(reducer);
```

[[Reducer]]

O `reducer` é a função responsável por escrever no estado global. Ela tem uma “assinatura” bem definida: deverá receber um _state_ e uma _action_ como parâmetro e retornar um novo estado ou o estado anterior:

```jsx
// Criando uma função Reducer
const reducer = (state, action) => state
```

[[Actions]]

Uma `action` nada mais é do que um objeto que possui obrigatoriamente a chave `type`:

```jsx
// Action para Incrementar nosso contador:
const action = {
  type: 'INCREMENT_COUNTER'
};
```

Definimos o `type` da `action` como sendo a _ação_ que será enviada para o `reducer` para alterar o estado. No caso acima, a `action` irá enviar a ação `INCREMENT_COUNTER` para o `reducer`. Assim que receber essa `action`, o `reducer` será responsável por atualizar o estado global.

[[Dispatch(action)]]

Para enviar uma `action` para o `reducer` é necessário passá-la como argumento para a função `dispatch()`.

```jsx
dispatch({type: 'INCREMENT_COUNTER'});
```

[[GetState()]]

Para ler o estado global, o objeto `store` disponibiliza a função `getState()`. Essa função retorna o estado global:

```jsx
const state = store.getState()
```

[[subscribe()]]

Geralmente iremos precisar fazer ações quando o estado global é atualizado. Por exemplo, toda a vez que o contador é incrementado, precisaremos renderizar o novo valor do estado na tela.

Para isso, o objeto `store` também disponibiliza a função `subscribe()`. Essa função recebe um callback que irá ser chamado toda vez que o estado global sofrer alterações:

```jsx
store.subscribe(() => {
    console.log(`O novo estado global é ${store.getState()}`)
})
```

## Juntando todas as peças

A animação abaixo mostra, de forma didática, como todas as peças são interligadas no Redux:

![[Redux.gif]]
> Extraído de: redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow

![[CicloRedux.png]]

![[CicloRedux2.png]]



## E o Redux Toolkit (RTK)?

Você poderá ter notado que, ao criar a `store`, um _“deprecation warning”_ na função `createStore` no seu editor de código.
![[Pasted image 20221025101716.png]]
Isso acontece porque os mantenedores do Redux criaram uma forma simplificada de configurar e usar o Redux chamada de _Redux Toolkit (RTK)_.

Por mais que entendemos a necessidade de simplificação e utilidade da ferramenta, não nos aprofundaremos nesse momento nessa outra biblioteca. Isso porque ela faz abstrações que dificultam o entendimento da estrutura do Redux. Mas fique à vontade para explorar o [RTK na documentação oficial](https://redux-toolkit.js.org/).

Apesar do _deprecation warning_, o `createStore` [não está deprecado](https://github.com/reduxjs/redux/issues/4325#issuecomment-1095113258) e não há planos de retirada dessa API da biblioteca. De forma opcional, se você preferir remover esse _warning_, basta inserir essa linha na importação:

```jsx
import { legacy_createStore as createStore } from 'redux';
```

# Redux DevTools

Como o Redux traz um fluxo bem definido para “escrever” e “ler” do estado global, é muito útil conseguirmos visualizar na nossa aplicação o que está acontecendo por trás dos panos.

Para isso, existe uma extensão de navegador chamada **Redux Devtools.** Com ela, é possível inspecionar o estado global bem como as actions disparadas e subsequentes alterações no estado.

Para usar o **Redux Devtools** é necessário que você siga dois passos:

-   [Instalar a extensão](https://github.com/reduxjs/redux-devtools/tree/main/extension#installation) no seu navegador de preferência;
-   [Integrar a extensão](https://github.com/reduxjs/redux-devtools/tree/main/extension#usage) no código da sua aplicação.


