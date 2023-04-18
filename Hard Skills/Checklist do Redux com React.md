

Para conectarmos o _Redux_ ao _React_ precisamos fazer algumas configurações, definidas pelo próprio _Redux_. Preparamos um checklist abaixo que poderá servir como um guia para quando você for implementar uma aplicação que utilize o _Redux_.

💡 É importante ressaltar que a estrutura das pastas apresentada abaixo é **apenas uma sugestão**. Você tem liberdade para estruturar da maneira que preferir!

## Antes de começar

-   [x] pensar como será o _formato_ do seu estado global
-   [x] pensar quais actions serão necessárias na sua aplicação

## Instalação

-   [x] npx create-react-app my-app-redux;
-   [x] npm install –save redux react-redux;
-   [x] npm install –save @redux-devtools/extension

## Criar dentro do diretório `src`:

-   [x] diretório `redux`

## Criar dentro do diretório `redux`

-   [x] diretório `actions`
-   [x] diretório `reducers`
-   [x] arquivo `index.js`

## Criar dentro do diretório `actions`:

-   [x] arquivo `index.js`.

## Criar dentro do diretório `reducers`:

-   [x] arquivo `index.js`.

## Criar dentro do arquivo `redux/index.js`:

-   [x] importar o createStore
-   [x] configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)
-   [x] importar o rootReducer
-   [x] criar e exportar a store

Exemplo:

```js
import { legacy_createStore as createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from '../reducers';

const store = createStore(rootReducer, composeWithDevTools());

export default store;
```

## Criar dentro do arquivo `redux/reducers/index.js`:

-   [x] estado inicial
-   [x] criar função reducer com `switch` retornando apenas a opção `default`
-   [x] criar `rootReducer` usando o `combineReducers`
-   [x] exportar `rootReducer`

Exemplo:

```js
import { combineReducers } from 'redux';

const INITIAL_STATE = {};

const exampleReducer = (state = INITIAL_STATE, action) => {
 switch(action.type) {
   default:
    return state;
 }
}

const rootReducer = combineReducers({ exampleReducer })

export default rootReducer;
```

## No arquivo `./src/index.js`:

-   [x] importar a `store`
-   [x] importar o `Provider`, para fornecer os estados a todos os componentes encapsulados pelo `<App />`

Exemplo:

```js
// Na importação
import { Provider } from 'react-redux';
import store from './redux/store'
```

```js
// No render
 <Provider store={ store } >
   <App />
 </Provider>
```

## No arquivo `redux/actions/index.js`:

-   [x] criar e exportar os actionTypes

Exemplo:

```js
// ACTIONS TYPES
export const ADD_EMAIL = 'ADD_EMAIL';
```

-   [x] criar e export os actions creators necessários

Exemplo:

```js
// ACTIONS CREATORS
export const addEmail = (email) => ({
  type: ADD_EMAIL,
  email,
})
```

## Nos reducers:

-   [ ] criar os casos para cada action criada, retornando o devido estado atualizado

## Nos componentes que irão ler o estado:

-   [ ] criar a função `mapStateToProps`
-   [ ] exportar usando o `connect`

## Nos componentes que irão modificar o estado:

-   [ ] acessar a função `dispatch` diretamente das _props_ do componente
-   [ ] exportar usando o `connect`

Exemplo:

```js
// No import
import { connect } from 'react-redux';
```

```js
// No export
export default connect(mapStateToProps)(Component)
```