[[DOM]]
[[JavaScript]]


### Instalar arquivos necessários
1º `npm init -y`
Cria o projeto já com o package.json padrão.
2º`npm i vite`
Instala o vite
3º dentro do Arquivo "package.json" adicionar a informação `"dev": "vite"` (Linha 7).

### Criar os arquivos HTML e Java Script
`index.html e index.js`

Criar o html padrão e dar o comando no terminal `npm run dev`, esse comando vai verificar se o `vite` está funcionando.

Após verificar se o vite está ok devemos importar o HTML da seguinte maneira:
```html
<script type="module" src="./index.js"></script>
```

### Index.js
No exemplo a ser usado estamos criando uma aplicação que vai incrementar toda vez que clicarmos em um botão.

Desta forma começamos no arquivo index.js adicionando o `addEventListener()` para escutar o evento de click

```js
const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

### Adicionar o Redux na aplicação

Para instalar o Redux, abra o terminal e digite:

```bash
npm i redux
```

O proximo passo é importar o Redux:

```js
import { legacy_createStore as createStore } from "redux";

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Agora deveremos criar a Store. Essa Store será o estado global de nossa aplicação, nela ficaram armazenados todas as informações referentes a nosso estado.
Desta forma nosso estado estará dentro desta Store, a função que vai mudar o nosso estado também, e por fim as ações que vamos chamar quando for mudar o estado:

> **Store é aonde vamos armazenar todos os dados compartilhados da aplicação representado por um objeto JavaScript. O State é armazenado na Store do Redux.**


```js
import { legacy_createStore as createStore } from "redux";

const store = createStore()

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Para a criar a Store precisamos passar para a função `createStore` um parametro que é o `reducer`. O `reducer` é a função responsável por mudar o estado da minha aplicação.

```js
import { legacy_createStore as createStore } from "redux";

const reducer = (state, action) => {
	return state;
}

const store = createStore()

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Por sua vez o `reducer` vai receber 2 parametros, o `state` e o `action`.

> **Action é um objeto JavaScript que representa alguma mudança/alteração que precisa acontecer no state.**

> **Reducer é uma função JAvaScript que recebe o estado atual (state) e a ação corrente (action) e retorna um novo estado (new state).
> É responsabilidade dessa função decidir o que acontecerá com o estado de acordo com uma ação (action).**


```js
import { legacy_createStore as createStore } from "redux";

const reducer = (state, action) => {
	return state;
}

const store = createStore(reducer)

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

### Adicionando o estado inicial

Para adicionar o valor inicial do nosso `state` podemos fazer isso diretamente dentro da variavel `reducer` ou criar outra variavel e só chamar ela no `state`.

```js
import { legacy_createStore as createStore } from "redux";

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {
	return state;
}

const store = createStore(reducer)

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

### Instalar a extensão Dev Tolls

Uma boa pratica é instalar o Dev Tolls em seu navegador e em sua aplicação. Este programa facilita o processo de verificar se a nossa aplicação está rodando corretamente. Para instalar ele em nossa apliação, abra o terminal e adiciona o seguinte comando:

```bash
npm i @redux-devtools/extension
```

Depois de instalada deveremos importar.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {
	return state;
}

const store = createStore(reducer)

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Agora vamos chamar o Dev Tolls dentro da `store`, ela será nosso segundo parametro.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Com o Dev Tolls já conseguimos de forma visual acompanhar tudo o que acontece em nosso estado.

### Configurando a ação de incrementar

Agora precisamos configurar a ação que vai incrementar o nosso contador, para isso vamos criar uma variavel contendo nossa ação.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Agora deveremos verificar qual a action foi chamada, como a nossa aplicação só tem um podemos utilizar o laço de repetição [[IF...Else]], porém o mais comum é utilizar o [[Switch...Case]].

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {

});
```

Desta forma sempre que o reducer receber o estado atual ele vai pegar aquele número no momento e incremetar 1. Agora devemos adicionar a ação no botão pois através deste botão que faremos o processo de incrementação.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {
	store.dispatch(action)
});
```

> **Dispatch é uma função que recebe uma action.**


Desta forma já podemos ver pelo Dev Tolls que o estado está sendo atualizado, porém no HTML isso aiinda não acontece.

### Refletir as atualizações do estado no HTML

A propria store tem uma função chamada de `subscribe` que será responsável por fazer o processo de escuta do estado e sempre que ele for alterado, refletir na tela (HTML)

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {
	store.dispatch(action)
});
store.subscribe(() => {

})
```

O proximo passo é pegar o número que será incrementado la do HTML, ele está dentro de uma TAG H2.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {
	store.dispatch(action)
});
store.subscribe(() => {
	const counterElement = document.querySelector("h2");
})
```

Já conseguimos pegar o valor que está na TAG h2, o proximo passo é alterar este valor. A própria `store` possui um metodo que conseguimos verificar o valor atual do estado.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {
	store.dispatch(action)
});
store.subscribe(() => {
	const globalState = store.getState()

	const counterElement = document.querySelector("h2");
})
```

Esse globalState vai me retornar um objeto da seguinte forma:
```jsx
Object { count: 1 }
```
E toda  vez que clicarmos no botão este numero 1 será incrementado.
O próximo passo é utilizar o `innerHTML` para atualizar o valor do contador.

```js
import { legacy_createStore as createStore } from "redux";
import { composeWithDevTolls } from "@redux-devtools/extension"

const INITIAL_STATE = { Cont: 0 };

const reducer = (state = INITIAL_STATE, action) => {

	if (action.type === "INCREMENT_COUNTER") {
	return { count: state.count +1 };
	}
	return state;
}

const store = createStore(reducer, composeWithDevTolls());

const action = {type: "INCREMENT_COUNTER" };

const incrementButton = document.querySelector("button")
incrementButton.addEventListener("click", () => {
	store.dispatch(action)
});
store.subscribe(() => {
	const globalState = store.getState()

	const counterElement = document.querySelector("h2");
	counterElement.innerHTML = globalState.count
})
```

Pronto! estamos conseguindo fazer a interação do estado global com o HTML.

```jsx
import { legacy_createStore as createStore } from 'redux';

import { composeWithDevTools } from '@redux-devtools/extension';

  

// 1. Criando o Reducer com Estado Inicial

const INITIAL_STATE = { count: 0 };

  

const reducer = (state = INITIAL_STATE, action) => {

if (action.type === 'INCREMENT_COUNTER') {

return { count: state.count + 1 };

}

return state;

};

  

// 2. Criando a Store já com Redux Devtools

const store = createStore(reducer, composeWithDevTools());

  

// 3. Criando a Action

const action = { type: 'INCREMENT_COUNTER' };

  

// 4. Disparando a Action

const buttonEl = document.querySelector('button');

buttonEl.addEventListener('click', () => store.dispatch(action));

  

// 5. Lendo do Estado global

store.subscribe(() => {

const globalState = store.getState();

  

const countEl = document.querySelector('h2');

countEl.innerHTML = globalState.count;

  

console.log('Estado atualizado !');

});
```
