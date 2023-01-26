[[React]]
[[Redux]]
[[Actions]]
[[API]]
[[Operações Assíncronas]]




O `redux-thunk` é um [middleware](https://redux.js.org/understanding/history-and-design/middleware) que, no contexto de uma aplicação **_Redux_**, nada mais é que um **interceptador** que captura **todas** as `actions` enviadas pela `store` **antes** delas chegarem a um `reducer`.

>Fazendo uma analogia com pedido online de produto, se a `action` fosse o produto que você comprou em algum site e o `reducer` fosse você, o **middleware** seria o correio, o qual intercepta o produto antes de chegar até você, de modo a garantir que a entrega ocorra corretamente.

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

![Fluxo de dados do redux-thunk](https://content-assets.betrybe.com/prod/ee873216-313d-4b21-98e1-14bc761efaa1-Fluxo%20de%20dados%20do%20redux-thunk.gif)
>Extraído de: redux.js.org/tutorials/fundamentals/part-6-async-logic

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/06bc61c7-2405-44ef-863e-13d649d88998/day/8f5d937b-83d0-47e2-bf8f-3b7a6238b068/lesson/c5c36fa2-aaa2-439c-bc21-727a35b0d1d6)