[[Redux]]
[[React]]
[[Redux DevTools Extension]]

# Checklist do react-redux

#### _Antes de começar_

- [ ] Pensar como será o _formato_ do seu estado global. Quais elementos terão seus dados acessados por mais de um componente.
- [ ] Pensar quais actions serão necessárias na sua aplicação (pode ser feita posteriormente).

_Instalações_

```jsx
1 - npm i redux react-redux;
2 - npm i redux-devtools-extension
3 - npm install react-router-dom@v5
```

- [ ] 1 - Instalar o React e o Redux simulmaneamente.
- [ ] 2 - Instalar o Redux DevTolls.
- [ ] 3 - Instalar o React Router 


#### _Criar pasta do Redux dentro da pasta src:_

- [ ] Diretório/pasta do `redux`

#### **Criar dentro do diretório/pasta `redux`**

- [ ] Diretório/pasta [[Store]]
- [ ] Diretório/pasta [[Actions]]
- [ ] Diretório/pasta [[Reducer]]

#### _Criar dentro do diretório/pasta `actions`:_

- [ ] Criar arquivo(s) no formato .js. Ex: `index.js`.

#### _Criar dentro do diretório `store`:_

- [ ] Criar arquivo no formato .js. Ex: `index.js`.

#### _Criar dentro do diretório `reducers`:_

- [ ] Criar arquivo no formato .js. Ex: `index.js`.
- [ ] criar os reducers necessários.
- [ ] criar `rootReducer` usando o `combineReducers` no arquivo index.js caso tenha mais de 1 reducer.
- [ ] Adicionar os valores de `INITIAL_STATE`.

Dica: Manter os nomes das variaveis dos Reducers iguais ao seu nome de arquivo adicionando somente o sufixo Reducer. Ex: 
```jsx
const incrementValorReducer = (state = INITIAL_STATE, action) => {
...
}
export default incrementValorReducer;
```


Exemplo:
_Seu reducer pode seguir esse modelo:_

Reducer 1

```js
const INITIAL_STATE = {};

const nomeReducer1 = (state = INITIAL_STATE, action) => {
  switch(action.type) {
    default:
      return state;
  }
};

export default nomeReducer1;
```

Reducer 2

```js
const INITIAL_STATE = {};

const nomeReducer2 = (state = INITIAL_STATE, action) => {
  switch (action.type) {
    default:
      return state;
  }
};

export default nomeReducer1;
```

CombineReducers
```js
import { combineReducers } from 'redux';
import nomeReducer1 from './nomeReducer1';
import nomeReducer2 from './nomeReducer2';

const rootReducer = combineReducers({
  nomeReducer1,
  nomeReducer2,
});

export default rootReducer;
```

#### _Configurar a Store no arquivo store/index.js:_

- [ ] importar `rootReducer` e usá-lo na criação da `store`
- [ ] configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)
- [ ] exportar a `store`

```js
import { legacy_createStore as createStore } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension';
import rootReducer from '../reducers';

const store = createStore(rootReducer, composeWithDevTools());

export default store;
```

#### _Importar o Provider no arquivo App.js:_

Dica: O `Provider` normalmente é adicionado dentro do arquivo **index.js na pasta /src**.
- [ ] importar o `Provider`
```jsx
import { Provider} from 'react-redux';
```

- [ ] importar a `store`
```jsx
import { store} from 'redux';
```

- [ ] definir o [[Provider]] juntamente com a store, para fornecer os estados a todos os componentes encapsulados em `<App />`.
```jsx
<Provider store={ store }>
	<App />
</Provider>,
```

Ex: /src/index.js
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import store from './redux';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<Provider stpre={ store }>
		<App />
	</Provider> );

```

#### _Na pasta actions:_

- [ ] criar e exportar os actionTypes;`
- [ ] criar e exportar os actions creators necessários

_Exemplo de action types (arquivo actionTypes.js)_

```js
export const USER_LOGIN = 'USER_LOGIN';
```

_Exemplo action creator_

```js
import { USER_LOGIN } from '../actions/actionTypes';
export const minhaAction = (value) => ({ type: USER_LOGIN, value });
```


Ex: /src/redux/actions
```jsx
// Action type
export const ADD_EMAIL = 'ADD_EMAIL';
// Action Creator
export const addEmail = (email) => ({
	type: ADD_EMAIL, email,
})
// Action
{ type: ADD_EMAIL, email, }
```

#### _Nos reducers:_

- [ ] criar os casos para cada action criada, retornando o devido estado atualizado

_Nos componentes que irão ler o estado:_

- [ ] criar a função `mapStateToProps`
- [ ] exportar usando o `connect`

_Nos componentes que irão modificar o estado:_

- [ ] criar a função `mapDispatchToProps`
- [ ] exportar usando o `connect`
- [ ] Desestruturar os meus arquivos que estão no estado global.
- [ ] Como esses arquivos viraram props, utlizar o `this.props`

Dica: `mapStateToProps` só é utilizado nos componetes que você deseja ler o estado global. Se quiser apenas gravar, basta utilizar o `connect`.

/src/componente/...

Ex: Utilização do `mapStateToProps` para gravar no estado global.
```js

...
const mapStateToProps = (state) => ({
  theme: state.theme,
  name: state.name,

export default connect(mapStateToProps)(App);
```

Ex: Quando você precisa apenas gravar no estado global.
```js
...

export default connect()(App);
```

