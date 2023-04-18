[[React]]
[[Redux]]


O **Redux** é uma biblioteca **independente** que pode ser utilizada com diversos frameworks, como [React](https://reactjs.org/), [Angular](https://angularjs.org/), [Vue](https://vuejs.org/), [Ember](https://emberjs.com/), ou até mesmo com o **JavaScript puro**.

No caso do **React**, a biblioteca **React Redux** é quem faz essa conexão e pode ser instalada em sua aplicação por meio do comando:

```bash
npm install react-redux
```

> React Redux é a biblioteca oficial para realizar a conexão entre **React** e **Redux**

Agora, antes de avançarmos para novos aprendizados sobre esse tema, vamos relembrar alguns conceitos:

-   **Store:** É onde armazenamos o estado global da aplicação, representado por um objeto _JavaScript_.
-   **Action:** É um objeto _JavaScript_ que representa uma ação que precisa acontecer no estado global.
-   **Reducer:** É uma função _JavaScript_ responsável por escrever no estado global, de acordo com a ação solicitada pela `action`.
-   **Dispatch:** É uma função que envia uma `action` para processamento.

# Configurando Redux com React

Na aula de hoje iremos implementar um contador, utilizando o _Redux_ no _React_. Para iniciar, vamos criar e configurar uma aplicação React.

O primeiro passo é criar a aplicação React:

```bash
npx create-react-app my-app
```

Depois, instalamos as dependências que iremos utilizar nessa aula:

```bash
1npm install redux react-redux
```

-   `redux` é a biblioteca que possui a implementação do **Redux**;
-   `react-redux` é a biblioteca que realiza a conexão entre o **Redux** e o **React**.
    

Com as dependências instaladas, vamos implementar o Redux!

## Criando a Store e o Reducer

Para criarmos o estado global da aplicação, precisamos implementar a `store`, que irá armazenar o estado. Para isso, basta importarmos e executarmos a função `createStore` do `redux`.

```jsx
// ./src/redux/index.js
import { createStore } from 'redux';

const store = createStore();

export default store;

```

Com a _store_ pronta, precisamos criar o _reducer_, que é o responsável por escrever no estado global.

Para conseguirmos visualizar as informações do nosso estado global, vamos também adicionar a biblioteca `Redux Devtools`. Para instalá-la, utilize o comando abaixo:

```bash
npm install --save @redux-devtools/extension
```

Agora vamos concluir a construção do nosso estado global:

```jsx
// ./src/redux/index.js
import { createStore } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension';

const INITIAL_STATE = { count: 0 };

const reducer = (state = INITIAL_STATE, action) => state;

const store = createStore(reducer, composeWithDevTools());

export default store;

```

No código acima estamos criando o _reducer_ e o adicionando à _store_. Dessa forma, o _reducer_ está passando ao estado global a chave `count`, com o valor inicial `0`.

## Provider

Para finalizarmos a configuração do _React_ com _Redux_, precisamos passar as informações da `store` para o restante da aplicação. Assim, os componentes criados poderão acessar o estado global que acabamos de criar.

Lembra a biblioteca `react-redux` instalada anteriormente? Ela nos fornece um componente chamado `Provider`. Ele que _proverá_ as informações da _store_ para a nossa aplicação. Para isso, precisamos importá-lo no `./src/index.js` e encapsular o componente `App`, passando a `store` como _prop_:

```jsx
// ./src/index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';
import App from './App';
import store from './redux';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={ store }>
    <App />
  </Provider>,
);
```

# Lendo informações do estado global

Com o nosso _Redux_ configurado, vamos continuar a implementação do contador! Iremos adicionar um contador com dois botões. Ao pressionar o primeiro, o contador deverá `somar 1`. Ao clicar no segundo botão, o contador deverá `somar 5`.

Substitua o arquivo `App.js` pelo código abaixo:

```jsx
// ./src/App.js
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Contador</h1>
        <h2>0</h2>
        <button>Incrementa 1</button>
        <button>Incrementa 5</button>
      </div>
    );
  }
}

export default App;

```

No código acima o nosso contador está com o valor `0`, de forma estática. Nosso objetivo é utilizar o estado global para realizarmos as ações da aplicação. Então precisaremos substituir o valor do contador pelo valor armazenado no estado global `count`, criado anteriormente. Além disso, precisaremos alterar esse valor sempre que os botões forem clicados.

## Função mapStateToProps

Para lermos as informações do estado global com o _Redux_, precisamos utilizar uma função chamada `mapStateToProps`. Ela recebe como parâmetro as informações do estado global e retorna os valores que estão armazenados na `store`. Esses valores poderão ser acessados via _props_ no componente.

```jsx
const mapStateToProps = (state) => ({
  countState: state.count,
});
```

No código acima estamos criando uma _prop_ chamada `countState`, que recebe o valor da chave `count` armazenada no estado global. Agora basta buscarmos essa _prop_ e adicioná-la no código:

```jsx
// import React from 'react';

// class App extends React.Component {
//   render() {
    const { countState } = this.props;
//     return (
//       <div>
//         <h1>Contador</h1>
        <h2>{ countState }</h2>
//         <button>Incrementa 1</button>
//         <button>Incrementa 5</button>
//       </div>
//     );
//   }
// }

const mapStateToProps = (state) => ({
  countState: state.count,
});

// export default App;

```

Note que a função `mapStateToProps` está sendo definida **fora do escopo da classe do componente**.

Adicionando o código acima você irá perceber que o componente ainda não consegue acessar a _prop_ que definimos como `countState`. Isso acontece pois ainda precisamos _conectar_ o componente com o nosso _Redux_. Para fazermos isso podemos utilizar a função _connect_, disponibilizada pela biblioteca `react-redux`, que instalamos anteriormente.

## Connect

Para utilizarmos o connect, precisamos importá-lo da biblioteca `react-redux`:

```jsx
import { connect } from 'react-redux';
```

Para conectarmos a função `mapStateToProps` ao nosso componente fazendo uso do `connect`, utilizamos a sintaxe abaixo:

```js
connect(mapStateToProps)(Component)
```

Utilizando o connect dessa forma, ele irá retornar uma versão “especial” do nosso componente, que estará _conectada_ com a função `mapStateToProps`. No código do componente, podemos chamar o `connect` diretamente na exportação:

```jsx
// import React from 'react';
import { connect } from 'react-redux';

// class App extends React.Component {
//   render() {
//     const { countState } = this.props;
//     return (
//       <div>
//         <h1>Contador</h1>
//         <h2>{ countState }</h2>
//         <button>Incrementa 1</button>
//         <button>Incrementa 5</button>
//       </div>
//     );
//   }
// }

// const mapStateToProps = (state) => ({
//   countState: state.count,
// });

export default connect(mapStateToProps)(App);

```

Pronto! Com isso, nosso componente está acessando o valor armazenado no estado global. Experimente alterar o valor da chave `count` do objeto `INITIAL_STATE`, definido no arquivo `./src/store/index.js`. Sempre que o valor for alterado, você perceberá que o componente `App` irá renderizar o novo valor!

# Escrevendo no estado global

Para finalizarmos o nosso contador, precisamos implementar a lógica de incrementar o estado global do _Redux_. Precisamos fazer com que, sempre que um botão for clicado, o valor do estado global seja alterado.

O responsável por alterar o estado global no _Redux_ é o _reducer_. Entre no arquivo `./src/store` e analise o _reducer_ criado anteriormente. Perceba que ele apenas retorna o estado, sem modificações. Vamos refatorá-lo.

## Criando a função Reducer

Crie um novo arquivo `./src/redux/reducers/counterReducer.js` e adicione o código abaixo:

```jsx
1// ./src/redux/reducers/counterReducer.js
2const INITIAL_STATE = {
3  count: 0,
4};
5
6function counterReducer(state = INITIAL_STATE, action) {
7  switch (action.type) {
8    case 'INCREMENT_COUNTER':
9      return { count: state.count + 1 };
10    default:
11      return state;
12  }
13}
14
15export default counterReducer;
16
```

A função _reducer_ criada acima recebe como parâmetro o estado inicial e uma `action`. Por padrão, a `action` sempre retornará um objeto com a chave `type`, que informa qual _ação_ deve ser feita no estado. Verificamos se a _ação_ é `INCREMENT_COUNTER`. Em caso positivo, ele irá incrementar o valor da chave `count`, que está no estado global, em 1.

Agora precisamos criar a `action`.

## Action e Action Creator

A `action` é um objeto que envia uma _ação_ ao `reducer`, o qual realizará uma alteração no estado global. Podemos defini-la como abaixo:

```js
1const action = { type: 'INCREMENT_COUNTER' }
```

Além da chave `type`, que é obrigatória, podemos enviar outros valores ao `reducer`, como no exemplo abaixo:

```js
1const action = { 
2  type: 'INCREMENT_COUNTER',
3  payload: 10
4}
```

À medida que nossas aplicações ficam mais complexas, é comum que as `actions` possuam mais valores. Por conta disso, uma outra forma de criar as `actions` é por meio das `actions creators`.

As `actions creators` são funções que criam e retornam uma `action`, evitando o trabalho de precisarmos digitar o objeto inteiro toda vez que formos chamar a `action`. Além disso, é uma boa forma de padronizarmos uma ação, evitando assim possíveis erros caso ela seja utilizada várias vezes.

Voltando ao contexto do nosso contador:

-   Ao clicar no primeiro botão, ele incrementa o contador em 1;
-   Ao clicar no segundo botão, ele incrementa o contador em 5.

Sem a `action creator` precisaríamos digitar o objeto inteiro da `action` duas vezes, uma para enviar o valor 1, outra para enviar o valor 5. Consegue perceber como essa maneira não é escalável?

Criando uma `action creator`, poderíamos apenas enviar por parâmetro o valor que deve ser incrementado, evitando que nossa aplicação possua muito código repetido:

```jsx
1// ./src/redux/actions/index.js
2export const actionCreator = (increment = 1) => ({ 
3  type: 'INCREMENT_COUNTER',
4  payload: increment,
5});
```

Agora que temos nossa `action` criada, vamos ajustar a função _reducer_ para incrementar de acordo com o valor recebido pela chave `payload`:

```jsx
1// const INITIAL_STATE = {
2//   count: 0,
3// };
4// function counterReducer(state = INITIAL_STATE, action) {
5//   switch (action.type) {
6//     case 'INCREMENT_COUNTER':
7      return { count: state.count + action.payload };
8//     default:
9//       return state;
10//   }
11// }
12// export default counterReducer;
```

## Ajustando a Store

Para finalizar, precisamos apenas ajustar a _store_ para receber a função _reducer_ que acabamos de criar. Altere o arquivo `./src/store/index.js` conforme abaixo:

```jsx
1import { createStore } from 'redux';
2import { composeWithDevTools } from '@redux-devtools/extension';
3
4import counterReducer from './reducers/counterReducer';
5
6const store = createStore(counterReducer, composeWithDevTools());
7
8export default store;
```

## Escrevendo no estado global com a função `dispatch()`

Você lembra da função `connect` que utilizamos anteriormente para _conectar_ nosso componente `App` com o _Redux_? Quando temos um componente _conectado_, podemos acessar uma _prop_ chamada `dispatch`. Precisamos utilizar essa função para chamar a `action`, a qual enviará a _ação_ para o `reducer` que, por sua vez, realizará a alteração no estado global.

```jsx
1// import React from 'react';
2// import './style.css';
3// import { connect } from 'react-redux';
4import { actionCreator } from './redux/actions';
5
6// class App extends React.Component {
7//   render() {
8    const { dispatch, countState } = this.props;
9//     return (
10//       <div>
11//         <h1>Contador</h1>
12//         <h2>{ countState }</h2>
13        <button onClick={() => dispatch(actionCreator())}>Incrementa 1</button>
14        <button onClick={() => dispatch(actionCreator(5))}>Incrementa 5</button>
15//       </div>
16//     );
17//   }
18// }
19
20// const mapStateToProps = (state) => ({
21//   countState: state.count,
22// });
23
24// export default connect(mapStateToProps)(App);
25
```

Pronto! No código acima:

-   Importamos o `action creator`;
-   Pegamos o `dispatch` por meio das _props_;
-   No clique dos botões, enviamos a informação da _ação_ para o _reducer_, por meio da função `dispatch`.

# Aplicação final

```jsx
import React from 'react';

import { connect } from 'react-redux';

import { actionCreator } from './redux/actions';

  

class App extends React.Component {

render() {

const { dispatch, countState } = this.props;

return (

<div>

<h1>Contador</h1>

<h2>{ countState }</h2>

<button onClick={() => dispatch(actionCreator())}>Incrementa 1</button>

<button onClick={() => dispatch(actionCreator(5))}>Incrementa 5</button>

</div>

);

}

}

  

const mapStateToProps = (state) => ({

countState: state.count,

});

  

export default connect(mapStateToProps)(App);
```



# Imutabilidade do estado global

Quando precisamos manipular o estado de componentes de classe em uma aplicação _React_, precisamos utilizar a função `this.setState()`. Isso acontece pois o estado de um componente é **imutável**, ou seja, não podemos modificá-lo diretamente. Esse mesmo conceito se aplica quando estamos trabalhando com o estado global gerenciado pelo _Redux_.

Isso significa que não podemos escrever diretamente no estado global do _Redux_. Por esse motivo, precisamos utilizar as funções _reducer_, pois elas são as responsáveis por escreverem informações no estado global.

Porém, como o estado é imutável, o _reducer_ **não consegue** atualizar o valor do estado global. Quando o executamos, ele **sobrescreve** o estado.

Voltando ao nosso exemplo do contador, vamos implementar um novo campo que irá contar **o número de vezes que nossos botões foram clicados**. Para isso, iremos adicionar um novo valor ao estado global, a chave `clicks`:

```jsx
1const INITIAL_STATE = {
2  clicks: 0,
3  count: 0,
4};
5
6function counterReducer(state = INITIAL_STATE, action) {
7  switch (action.type) {
8    case 'INCREMENT_COUNTER':
9      return { count: state.count + action.payload };
10    default:
11      return state;
12  }
13}
14export default counterReducer;
```

Quando o _reducer_ executar a ação `INCREMENT_COUNTER`, descrita acima, ele irá reescrever o estado global, adicionando exatamente o que está sendo retornado. Dessa forma, o estado global ficaria assim:

```js
1state = {
2  count: 1
3}
```

Percebe que, dessa forma, ele irá _apagar_ o valor `clicks` que estava no estado? Uma forma de conseguirmos resolver essa questão é utilizando o `spread operator`:

```jsx
1const INITIAL_STATE = {
2  clicks: 0,
3  count: 0,
4};
5
6function counterReducer(state = INITIAL_STATE, action) {
7  switch (action.type) {
8    case 'INCREMENT_COUNTER':
9      return { 
10        ...state, 
11        count: state.count + action.payload,
12      };
13    default:
14      return state;
15  }
16}
17export default counterReducer;
```

Dessa forma, ao executar a ação `INCREMENT_COUNTER`, o _reducer_ irá reescrever o estado global, adicionando todos os valores que **não foram modificados** (`...state`) e irá adicionar a chave `count` com o seu valor atualizado (`count: state.count + action.payload`):

```js
1state = {
2  clicks: 0,
3  count: 1,
4}
```

Mesmo quando o estado possui apenas uma chave, essa é uma prática importante que devemos adotar. Isso facilitará para caso, futuramente, você queira adicionar novas funcionalidades à sua aplicação.

Explore o _reducer_ da aplicação abaixo para entender na prática como funciona a imutabilidade do estado global:

# Aplicação final com imutabilidade

```jsx
const INITIAL_STATE = {
  clicks: 0,
  count: 0,
};

function counterReducer(state = INITIAL_STATE, action) {
  switch (action.type) {
    case 'INCREMENT_COUNTER':
      return {
        ...state,
        count: state.count + action.payload,
      };
    case 'INCREMENT_CLICK':
      return {
        ...state,
        clicks: state.clicks + 1,
      };
    default:
      return state;
  }
}

export default counterReducer;
```

# Utilizando mais de um Reducer

Até agora aprendemos como criar uma _store_ utilizando apenas um _reducer_. Porém, é possível adicionarmos mais de um _reducer_ na nossa aplicação. Para isso, podemos utilizar a função `combineReducers`, disponibilizada pela biblioteca `redux`.

## combineReducers

O método `combineReducers`, como o próprio nome diz, é uma função que faz a _junção_ de todos os _reducers_. Ela deve receber como parâmetro um objeto com todos os `reducers` que serão utilizados:

```jsx
1import { combineReducers } from 'redux';
2
3combineReducers({
4  reducer1,
5  reducer2,
6  reducer3,
7  // ...
8})
```

Voltando ao exemplo da aplicação com o contador, a estrutura do `combineReducers` ficaria da seguinte forma:

```jsx
1// ./src/reducers/index.js
2import { combineReducers } from 'redux';
3import counterReducer from './counterReducer';
4
5const rootReducer = combineReducers({ counterReducer });
6
7export default rootReducer;
```

Perceba que podemos utilizar o `combineReducers` mesmo quando possuímos apenas um _reducer_.

Para fazermos uso do `combineReducers` precisamos informar à _store_ que iremos utilizar os _reducers_ combinados:

```jsx
1import { createStore } from 'redux';
2import { composeWithDevTools } from '@redux-devtools/extension';
3
4import rootReducer from '../reducers';
5
6const store = createStore(rootReducer, composeWithDevTools());
7
8export default store;
9
```

⚠️ Quando utilizamos o `combineReducers`, o estado global se torna um objeto em que as suas chaves são os _reducers_:

```js
1state = {
2  reducer1: { ... },
3  reducer2: { ... },
4  reducer3: { ... },
5}
```

No exemplo do contador, se utilizarmos o `combineReducers`, o estado global ficaria da seguinte forma:

```js
1// Estado global com combineReducers:
2state = {
3  counterReducer: {
4    count: 0,
5  }
6}
7
8// Estado global sem combineReducers:
9state = {
10  count: 0,
11}
```

Logo, a função `mapStateToProps` criada no componente `App` também precisaria ser alterada, conforme abaixo:

```jsx
1const mapStateToProps = (state) => ({
2  countState: state.counterReducer.count,
3});
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/06bc61c7-2405-44ef-863e-13d649d88998/day/d774b23e-9833-4773-aaff-9c83b1aeb397/lesson/a428b656-0b68-4dee-97c8-a0b95434ef30)