[[Redux]]
[[Operações Assíncronas]]
[[Funções]]


O `redux-thunk` é um [middleware](https://redux.js.org/understanding/history-and-design/middleware) que, no contexto de uma aplicação **_Redux_**, nada mais é que um **interceptador** que captura **todas** as `actions` enviadas pela `store` **antes** delas chegarem a um `reducer`.

> Fazendo uma analogia com pedido online de produto, se a `action` fosse o produto que você comprou em algum site e o `reducer` fosse você, o **middleware** seria o correio, o qual intercepta o produto antes de chegar até você, de modo a garantir que a entrega ocorra corretamente.

Para fazer uso do `redux-thunk`, é preciso instalá-lo via `npm`:

```bash
npm install redux-thunk
```

Para habilitar o uso do `redux-thunk` na sua aplicação, é preciso fazer uso da função `applyMiddleware()` do **_Redux_**:

```js
// arquivo em que a redux store é criada
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import reducer from '/path/to/your/root/reducer';

// ...

const store = createStore(reducer, applyMiddleware(thunk));
// ...
```

Para usar o `redux-thunk` junto com o `Redux Devtools`, é preciso passar o `applyMiddleware(thunk)` como parâmetro para a função `composeWithDevTools`, como no exemplo a seguir:

```js
// arquivo em que a redux store é criada
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import reducer from '/path/to/your/root/reducer';
import { composeWithDevTools } from '@redux-devtools/extension';

// ...

const store = createStore(reducer, composeWithDevTools(applyMiddleware(thunk)));
// ...
```

O `thunk` é uma função que encapsula uma operação para que ela seja feita posteriormente. Em termos práticos, isso significa que você está definindo uma função que vai ser **retornada** por uma outra função com mais lógica adicionada a ela.

Até agora, ao criar uma `action creator`, essa função deveria retornar sempre um objeto (action). Com `redux-thunk`, você consegue definir uma `action creator` **que retorna uma função** em vez de retornar um objeto - tecnicamente o nome dessa função é `thunk action creator`.

Na função que é retornada pelo `thunk action creator` você poderá realizar uma operação assíncrona. Uma vez finalizada a operação, você conseguirá enviar uma `action` com os dados obtidos por ela, da mesma forma que tem feito até então.

Note a conveniência que isso traz: toda essa lógica de lidar com operações assíncronas está encapsulada na sua respectiva `action` assíncrona, deixando nítido para quem for fazer uso dela. Na sua aplicação, sob a perspectiva de um componente **_React_**, ele estaria consumindo uma `action` como uma outra qualquer.

Como foi dito, o `thunk action creator` deve retornar uma função. Ela pode fazer uso das funções `dispatch` e `getState`, que recebe como parâmetros.

No exemplo abaixo, temos duas actions: `REQUEST_MOVIES_STARTED` E `RECEIVE_MOVIES`. A primeira deve ser disparada no momento em que a api é chamada, enquanto a segunda apenas após o recebimento dos dados assíncronos. Ambas são disparadas dentro do `thunk action creator`:

```js
//src/redux/actions/index.js

// action creator
const requestMoviesStarted = () => ({
  type: 'REQUEST_MOVIES_STARTED',
});

// action creator
const receiveMovies = (movies) => ({
  type: 'RECEIVE_MOVIES',
  movies,
});

// thunk action creator: deve retornar uma função
export function fetchMovies() {
  return (dispatch, _getState) => { 
    dispatch(requestMoviesStarted()); // dispatch da action 'REQUEST_MOVIES_STARTED' 
    return fetch('alguma-api-qualquer.com')
      .then((response) => response.json())
      .then((movies) => dispatch(receiveMovies(movies))); // dispatch da action 'RECEIVE_MOVIES'
  };
}
```

No componente:

```jsx
//src/components/Movies.js

import { fetchMovies } from './redux/actions';

// ...
class Movies extends Component {
  // ...
  componentDidMount() {
    const { dispatch } = this.props;
    dispatch(fetchMovies()); // enviando a action fetchMovies
  }
  // ...
}
// ...
export default connect()(Movies)
```

Em síntese, um `thunk` nada mais é do que uma `action creator` que deverá retornar uma função ao invés de um objeto. Esta função poderá fazer uma requisição assíncrona. Veja o fluxo na imagem abaixo:

![[Thunk.gif]]
> Extraído de: redux.js.org/tutorials/fundamentals/part-6-async-logic

  
Agora que você já sabe a base teórica de funcionamento do `thunk`, vamos montar uma aplicação que busca imagens de _doguinhos_ por [essa API](https://dog.ceo/dog-api/) e ver, na prática, como utilizar o `redux-thunk`. Primeiro, crie um diretório e use o comando:

```bash
npx create-react-app doguinhos-app
```

Feito o primeiro passo, acesse o diretório do seu novo app e instale as dependências necessárias:


```bash
cd doguinhos-app
npm i redux react-redux @redux-devtools/extension
```

Agora, vamos criar a `store`, `reducer` e `action` da aplicação:

```jsx
// ./src/redux/index.js
import { createStore } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension';
import dogReducer from './reducers/dogReducer'

const store = createStore(dogReducer, composeWithDevTools());

export default store;

```


```jsx
// ./src/redux/reducers/dogReducer.js
const initialState = {
  isFetching: false,
  imagePath: '',
  error: '',
};

function dogReducer(state = initialState, action) {
  switch (action.type) {
    case 'REQUEST_IMAGE':
      return { ...state, isFetching: true };
    case 'GET_IMAGE':
      return { ...state, imagePath: action.payload, isFetching: false };
    case 'FAILED_REQUEST':
      return { ...state, error: action.payload, isFetching: false };
    default:
      return state;
  }
}

export default dogReducer;

```


```jsx
// ./src/redux/actions/index.js
const GET_IMAGE = 'GET_IMAGE';
const REQUEST_IMAGE = 'REQUEST_IMAGE';
const FAILED_REQUEST = 'FAILED_REQUEST';

function getImage(json) {
  return { 
    type: GET_IMAGE, 
    payload: json.message,
  };
}

function requestDog() {
  return { type: REQUEST_IMAGE };
}

function failedRequest(error) {
  return { 
    type: FAILED_REQUEST, 
    payload: error,
  };
}

export function fetchDog() {
  return (dispatch) => {
    dispatch(requestDog());
    return fetch('https://dog.ceo/api/breeds/image/random')
      .then((response) => response.json())
      .then((json) => dispatch(getImage(json)))
      .catch((error) => dispatch(failedRequest(error)));
  };
}

```

Para finalizar a configuração do _Redux_, precisamos adicionar o `Provider` ao arquivo `index.js`:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';
import App from './App';
import store from './redux';

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);

```

Por fim, atualize o arquivo `App.js` com o código abaixo:

```jsx
// ./src/App.js
import React from 'react';
import { connect } from 'react-redux';
import { fetchDog } from './redux/actions';

class App extends React.Component {
  render() {
    const { isFetching, src, dispatch } = this.props;

    if (isFetching) return <p>Loading</p>;

    return (
      <div>
        <button
          style={{ display: 'block' }}
          onClick={() => dispatch(fetchDog())}
          type="button"
        >
          Novo Doguinho
        </button>
        {src && <img style={{ maxWidth: '80%' }} src={src} alt="dog" />}
      </div>
    );
  }
}

const mapStateToProps = (state) => ({
  src: state.imagePath,
  isFetching: state.isFetching,
});

export default connect(mapStateToProps)(App);

```

Ao clicar no botão, a _action_ `fetchDog` é disparada por meio da função `dispatch`. Essa _action_ deve realizar o `fetch` da _API_ e, após receber a resposta, enviar a _ação_ ao _reducer_ para salvar as informações obtidas pela _API_ no estado global.

Rode o `npm start` e depois clique no botão **Novo Doguinho**.

Opa! Você irá se deparar com um erro parecido com o seguinte:

![Erro - Falta do redux-thunk](https://content-assets.betrybe.com/prod/0565c6e7-eef5-4a01-ab82-1ced7a8f2703-Erro%20-%20Falta%20do%20redux-thunk.png)
> Erro - Falta do redux-thunk

O erro _Actions must be plain objects_ nos mostra que **actions precisam ser objetos puros**, ou seja, não podem ser funções.

Para usar `action creators` que retornam funções, nós precisamos de um middleware especial: o `redux-thunk`.

Para vermos o app rodando corretamente, vamos instalar o pacote e alterar nosso código para utilizar o `thunk` corretamente.

```bash
npm i redux-thunk
```

Após a instalação, devemos inserir o `thunk` em nossa aplicação. Precisamos alterar nossa `store` para o código abaixo:

```jsx
// src/redux/index.js
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension';
import thunk from 'redux-thunk';
import dogReducer from './reducers/dogReducer';

const store = createStore(
  dogReducer,
  composeWithDevTools(applyMiddleware(thunk))
);

export default store;

```

Salve a sua aplicação e execute o comando `npm start`. Agora, ao clicar no botão, o erro não deverá mais aparecer.

