[[Passo-a-passo Redux em JavaScript]]
[[Redux]]
[[React]]

Instalar o Redux

```shel
npm i redux
```

Instalar o DevTolls
```shel
npm i redux-devtools-extension
```

Uma boa pratica é criar uma pasta com o nome de Redux e armazenar os conteúdos relacionados ao Redux dentro desta pasta.

Criar o arquivo Store (store.js) que vai ter a Store (estado global), o reducer para atualizar o state e o proprio state.

Deveremos importar a Store e o DevTolls.
```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

});
```

Definir o state inicial da minha aplicação.
```jsx
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const initialState = {
	theme: 'dark',
}
});
```

Definir o reducer
```jsx
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const initialState = {
	theme: 'dark',
}
const reducer = (state = initialState, action) => {
	if (action.type === 'CHANGE_THEME') {
		return {
			theme: state.theme === 'dark' ? 'light' : 'dark';
		}	
	}
	return state;
}
});
```

Criar a Store

```jsx
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const initialState = {
	theme: 'dark',
}
const reducer = (state = initialState, action) => {
	if (action.type === 'CHANGE_THEME') {
		return {
			theme: state.theme === 'dark' ? 'light' : 'dark';
		}	
	}
	return state;
}
const store = createStore(reducer, composeWithDevTolls());

export default store;
});
```

Importar store no `Provider` similar ao `subscriber`.

Vamos precisar instalar o react-redux para utilizar o componente `Provider`.

```shel
npm i react-redux
```
 e importar no arquivo que vai distribuir o estado com todos os componentes (index.js)


Usar o `connect`, ele 'responsável por deixar a aplicação no estado global.
Você precisa chamar ele e importar junto ao export. A função mapStateToProps é um nome sujestivo que lê o estado global e converte em propriedades antes do componet ser reinderizado, neste caso seria o App.
A chave tema vai pegar o estado atual no outro componente (Store) 

```jsx
import { connect } from 'react-redux';
...

const mapStateToProps = () => ({
	tema: state.theme,
})
export default connect(mapStateToProps)(App);
```

Toda função exportada com o connect tem acesso ao dispatch e ao estado global

chamar o dispatch. Neste exemlo vamos vamos adicionar junto a ele um evento onClick.

```jsx
const { dispatch } = this.props;
...

onclick={ () => dispatch({ type: 'CHANGE_THEME'}) }
```




# Código final


App.js
```jsx
import './App.css';
import React from 'react';
import { connect } from 'react-redux';
import Main from './components/Main';
import light from './img/light.png';
import dark from './img/dark.png';
import interruptor from './img/interruptor.png';
import Header from './components/Header';

class App extends React.Component {
  render() {
    console.log(this.props);
    // eslint-disable-next-line react/prop-types
    const { dispatch, theme } = this.props;
    return (
      <Main>
        <Header />

        <button
          id="light-switch"
          type="button"
          onClick={ () => dispatch({ type: 'CHANGE_THEME' }) }
        >
          <img src={ interruptor } alt="interruptor" />
        </button>
        <div className="bulb">
          <img id="light-bulb" src={ theme === 'light' ? light : dark } alt="lampada" />
        </div>
      </Main>
    );
  }
}

const mapStateToProps = (state) => ({
  theme: state.theme,
  name: state.name,
});
export default connect(mapStateToProps)(App);
```

Store.js
```jsx
import { legacy_createStore as createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';

// definir o state da minha aplicacao
const initialState = {
  theme: 'dark',
  name: 'THIAGO',
};

// lógica, reducer
const reducer = (state = initialState, action) => {
  if (action.type === 'CHANGE_THEME') {
    return {
      ...state,
      theme: state.theme === 'dark' ? 'light' : 'dark',
    };
  }

  return state;
};

// criar a store
const store = createStore(reducer, composeWithDevTools());

export default store;
```

