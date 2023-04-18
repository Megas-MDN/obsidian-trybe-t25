[[React]]
[[DOM]]
[[Componentes]]
[[Props]]
[[State]]

Para auxiliar na lógica de sua aplicação e evitar o mal uso dos recursos disponíveis, cada componente React possui seu próprio **ciclo de vida**.

Como visto no vídeo anterior, existem funções específicas que são executadas ao final de cada fase do ciclo de vida de um componente: `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`. Porém o vídeo também menciona que existem outras funções consideradas menos comuns, como é o caso de `shouldComponentUpdate`, que pode ser chamada na fase de atualização.

Os componentes **React**, assim como os seres vivos, possuem um ciclo de vida. O ciclo do React é dividido em 3 etapas. São elas:

-   Montagem: quando o componente é inicializado e inserido no DOM;
-   Atualização: quando as props ou estados do componente são alterados;
-   Desmontagem: quando o componente morre 🧟‍♂️, sumindo do DOM.
    
Essa é a _big picture_, mas dentro dessas 3 etapas existem vários métodos que podemos interceptar para, assim, agir em determinado momento do ciclo de vida dos componentes.

![[Pasted image 20221024205646.png]]


> Ciclo de vida de um componente React

![[Captura de tela de 2022-10-24 20-58-02.png]]

O ciclo de vida é acessível por meio de métodos nativos dos _class components_. Como exemplo, pense no `render`, que é um método de renderização dos _class components_ e que é chamado toda vez que uma atualização acontece. Ele possui características intrínsecas que permitem adicionar o componente no DOM. Assim como o `render`, outros métodos possuem suas próprias características e objetivos.

> 💡 **Curiosidade:** caso você tenha familiaridade com vídeos em inglês, assista a [esse vídeo](https://www.youtube.com/watch?v=m_mtV4YaI8c), que também está presente nos recursos adicionais. Se não se sentir confortável, tudo bem, pois os conteúdos abordarão todo o tema.

O ciclo de vida e os **principais** métodos funcionam da seguinte maneira:

-   Montagem:
    -   **constructor** - recebe as props e define o estado;
    -   **render** - renderiza o componente, inserindo-o no DOM;
    -   **componentDidMount** - dispara uma ou mais ações após o componente ser inserido no DOM _(ideal para requisições)_;
-   Atualização:
    -   **shouldComponentUpdate** - possibilita autorizar ou não o componente a atualizar;
    -   **componentDidUpdate** - dispara uma ou mais ações após o componente ser atualizado;
-   Desmontagem:
    -   **componentWillUnmount** - dispara uma ou mais ações antes de o componente ser desmontado.

> 💡 **Curiosidade:** além dos métodos citados, há também outros que o próprio React intitula de _Métodos Raramente Usados_, como o `getDerivedStateFromProps` e `getSnapshotBeforeUpdate`. Caso tenha interesse, você pode aprender sobre eles neste [link](https://pt-br.reactjs.org/docs/react-component.html#static-getderivedstatefromprops).

## Entendendo quando cada método é chamado

Vamos agora fazer uma simulação, para ver na prática quando cada método chamado:

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    };
    console.log("construtor");
  }

  componentDidMount() {
    console.log("componentDidMount");
  }

  shouldComponentUpdate(nextProps, nextState) {
    console.log("shouldComponentUpdate");
    return true;
  }

  componentDidUpdate(prevProps, prevState) {
    console.log("componentDidUpdate");
  }

  render() {
    console.log("render");
    return (
      <div>
        <p>Contador</p>
        <button
          onClick={() => this.setState((state) => ({ counter: state.counter + 1 }))}
        >
          Soma
        </button>
        <p>{this.state.counter}</p>
      </div>
    );
  }
}
```

Ao executar o código acima, sem o clique no botão `Soma`, aparecerão as seguintes mensagens no console do seu _browser_:

![[Pasted image 20221024210342.png]]
> As mensagens ‘constructor’, ‘render’ e ‘componentDidMount’ são exibidas no console do navegador

Atente-se para a ordem de chamada dos métodos. As mensagens refletem a ordem de execução dos métodos de ciclo de vida do componente.

Os métodos `shouldComponentUpdate` e `componentDidUpdate` não apareceram no console, pois não houve atualização. Caso o botão `Soma` seja clicado, teremos mais mensagens no console:

![[Pasted image 20221024210417.png]]
> As mensagens ‘constructor’, ‘render’, ‘componentDidMount’, ‘shouldComponentUpdate’, ‘render’ e ‘componentDidUpdate’ são exibidas no console do navegador

Note que, durante o processo de atualização, o método `render` é chamado novamente. Isso acontece porque, quando se atualiza uma props ou estado, o React “pede” que o componente seja renderizado no DOM. Como apresentamos acima, caso seja válido, podemos impedir essa renderização retornando `false` com o método `shouldComponentUpdate`.

Podemos também, nos métodos `shouldComponentUpdate` e `componentDidUpdate`, acessar os estados ou props próximos e anteriores. Para isso, devemos utilizar os parâmetros _nextProps_ e _nextState_ no `shouldComponentUpdate` e _prevProps_ e _prevState_ no `componentDidUpdate`. Veja um exemplo:

Antes, vamos alterar os `console.log()` dos métodos citados acima:

```jsx
shouldComponentUpdate(nextProps, nextState) {
  console.log("shouldComponentUpdate", this.state, nextState);
  return true;
}

componentDidUpdate(prevProps, prevState) {
  console.log("componentDidUpdate", this.state, prevState);
}
```

Clicando uma vez no botão _Somar_, temos:

![[Pasted image 20221024210540.png]]
> Imagem que mostra as mensagens ‘constructor’, ‘render’, ‘componentDidMount’, ‘shouldComponentUpdate’, ‘componentDidUpdate’ e os estados no console

Perceba que o estado só é de fato atualizado quando chega no método `componentDidUpdate`. Por isso, caso seja necessário impedir uma renderização, você deve utilizar o método `shouldComponentUpdate`, que permite comparar os atuais e próximos estados ou props e adicionar a lógica.

## Requisições e componentDidMount

Vamos falar sobre o método `componentDidMount`, que é um dos mais utilizados em componentes `React` de classe.

Como você já deve ter percebido, trabalhar com requisições a APIs é uma prática muito comum no cotidiano de quem desenvolve. Operações assíncronas requerem uma atenção extra e, para que não ocorram problemas, caso sua requisição tenha que retornar algo para ser renderizado logo que a página carregar, é muito importante que você entenda bem a importância dessa etapa do ciclo de vida.

Para entender melhor, usando React, vamos consumir uma API de Rick and Morty, cujo o endpoint é `https://rickandmortyapi.com/api/character`, e exibir na tela os nomes dos personagens e suas respectivas fotos.

Então, o primeiro passo será criar um `App React` com o já familiar `npx create-react-app my-interdimensional-app` e instalar as dependências:

```bash
npx create-react-app my-interdimensional-app
cd my-interdimensional-app
npm install
```

Caso você queira ver as coisas acontecendo com um pouco mais de estilo, literalmente, é só substituir o conteúdo de `App.css` por:
```jsx
/* App.css */
.App {
  background-size: cover;
  background: linear-gradient(-45deg,#0b0c0c,  #125269, #125269, #0b0c0c);
  color: white;
  padding: 40px 20px;
  text-align: center;
}

.container {
  background-color: rgb(212, 195, 195);
  border-radius: 2px;
  border: 3px solid rgba(0, 0, 0, 0.125);
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.418);
  color: black;
  display: flex;
  flex-direction: column;
  height: 20%;
  margin: 5px;
  width: 300px;
}

.body {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
  padding: 30px;
}
```

Depois de transformar o componente `App.js` em um componente de classe, já podemos definir nosso estado inicial local, para que possamos armazenar nele os dados que a **API** retornará. Em seguida, também podemos fazer a requisição e colocar um título para ser exibido na página. Veja abaixo:

```jsx
// App.js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  constructor(props){
    super(props);
    this.state = {
        characters: [],
    };
  }

  fetchCharacters = () => {
    fetch('https://rickandmortyapi.com/api/character')
    .then(response => response.json())
    .then(data => {
      this.setState({characters: data.results})
    })
  }

  render() {
    return (
      <div className="App">
        <h1>
          Ricky and Morty Characters:
        </h1>
      </div>
    );
  }
}

export default App;
```

Note que a chave `results` é a que contém as informações que queremos, por isso é ela que estamos setando no nosso estado. Verificar se você está inserindo a chave certa é essencial e por isso você não deve deixar de ler a documentação da API que irá consumir para ver como os seus dados são retornados!

Depois disso, com nosso estado já recebendo o resultado da **API**, poderíamos fazer uma desestruturação no estado e fazer apenas um `.map` para iterar o array e renderizá-lo na tela. Outro detalhe importante aqui é o uso da `key`, que deve ser um identificador único, como se fosse um `ID` para cada item da lista iterada. Lembre-se: a função das **keys** é ajudar o React a identificar quais itens sofreram alterações para que o React não precise renderizar novamente toda a lista novamente e sim apenas se preocupar com a parte modificada.

Agora, é só criar tags para encapsular as informações que queremos, ou seja, o nome e a imagem dos personagens. Ou será que há mais o que fazer?!
```jsx
// App.js
// import React, { Component }from 'react';
// import './App.css';

// class App extends Component {
//  constructor(props){
//      super(props);
//      this.state = {
//        characters: [],
//      };
//   }

//  fetchCharacters = () => {
//    fetch('https://rickandmortyapi.com/api/character')
//    .then(response => response.json())
//    .then(data => {
//      this.setState({characters: data.results})
//    })
//  }

  render() {
    const { characters } = this.state;
    return (
      <div className="App">
        <h1>
          Ricky and Morty Characters:
        </h1>
        <div className="body">
          {characters.map(({ name, image }) => {
            return (
              <div className="container" key={name}>
                <h3>{name}</h3>
                <img src={image} alt={name}/>
              </div>
            )
          })}
        </div>
      </div>
    );
  }
}

export default App;
```

Você certamente notou que continua aparecendo apenas o título que tínhamos colocado anteriormente na página. Se você der um `console.log` em `characters` notará que o array continua vazio. Aquele velho problema do código ser lido antes da API retornar ataca novamente, mas nada tema, porque com o `componentDidMount` não há problema!

Todos os nossos problemas serão resolvidos apenas chamando a função `fetchCharacters` dentro do `componentDidMount`, mas, caso prefira, você pode fazer o `fetch` diretamente dentro dele. Funcionará das duas formas.

```jsx
//  Primeira maneira:
    fetchCharacters() {
      fetch('https://rickandmortyapi.com/api/character')
      .then(response => response.json())
      .then(data => {
        this.setState({characters: data.results})
      })
    }

    componentDidMount() {
      this.fetchCharacters();
    }

//  Segunda maneira:
    componentDidMount() {
      fetch('https://rickandmortyapi.com/api/character')
      .then(response => response.json())
      .then(data => {
        this.setState({characters: data.results})
      })
    }
```

Ao final, teremos uma aplicação funcionando e um código assim ou bem parecido com isso:

```jsx
// App.js
import React, { Component }from 'react';
import './App.css';

class App extends Component {
    constructor(props){
        super(props);
        this.state = {
            characters: [],
        };
      }

    componentDidMount() {
      fetch('https://rickandmortyapi.com/api/character')
      .then(response => response.json())
      .then(data => {
        this.setState({characters: data.results})
      })
    }

  render() {
    const { characters } = this.state;
    return (
      <div className="App">
        <h1>
          Ricky and Morty Characters:
        </h1>
        <div className="body">
          {characters.map((character) => {
            return (
              <div className="container" key={character.name}>
                <h3>{character.name}</h3>
                <img src={character.image} alt={character.name}/>
              </div>
            )
          })}
        </div>
      </div>
    );
  }
}

export default App;

```

No exemplo utilizado no vídeo, estamos fazendo uma requisição para uma [API de piadas](https://icanhazdadjoke.com/), e para isto nossa função de fetch está sendo chamada dentro do método `componentDidMount`. Este vai ser o primeiro passo para o nosso código ter o mesmo comportamento do vídeo de introdução desta seção.

Inicialmente, vamos criar um componente dentro da pasta `src/components` chamado `DadJoke` que vai ser o responsável por realizar a chamada a nossa API e renderizar a nossa piada.

```jsx
import React from 'react';

class DadJoke extends React.Component {
  constructor() {
    super();

    this.saveJoke = this.saveJoke.bind(this);

    this.state = {
      jokeObj: undefined,
      loading: true,
      storedJokes: [],
    }
  }

  async fetchJoke() {
    const requestHeaders = { headers: { Accept: 'application/json' } }
    const requestReturn = await fetch('https://icanhazdadjoke.com/', requestHeaders)
    const requestObject = await requestReturn.json();
    this.setState({
      jokeObj: requestObject,
    })
  }

  componentDidMount() {
    this.fetchJoke();
  }

  saveJoke() {
    // Esse método será responsável por salvar a piada no array de piadas storedJokes!!

  }

  render() {
    const { storedJokes } = this.state;
    const loadingElement = <span>Loading...</span>;

    return (
      <div>
        <span>
          {storedJokes.map(({ id, joke }) => (<p key={id}>{joke}</p>))}
        </span>

      {
        /*
        Aqui vamos construir nossa lógica com uma renderização condicional
        do nosso componente Joke, a ideia é renderizar um loading enquanto
        esperamos a nossa requisição de piadas finalizar.

        <p>RENDERIZAÇÃO CONDICIONAL</p>
        */
      }

      </div>
    );
  }
}

export default DadJoke;
```

E agora nossa aplicação tem o comportamento esperado conforme visto no primeiro vídeo desta seção. Estamos realizando uma requisição para uma API, e enquanto esperamos o resultado retornar, criamos uma lógica de renderização condicional.

Agora vamos criar um componente para renderizar a nossa piada na tela. Dentro da pasta `src/components` com o nome `Joke`.
```jsx
import React from 'react';

class Joke extends React.Component {
  render() {
    const { jokeObj, saveJoke } = this.props;

    return (
      <div>
        <p>{jokeObj.joke}</p>
        <button type="button" onClick={saveJoke}>
          Salvar piada!
        </button>
      </div>
    );
  }
}

export default Joke;
```

Por fim, vamos importar nosso componente `Joke` para ser renderizado através do `DadJoke` usando uma renderização condicional.
```jsx
import React from 'react';
import Joke from './Joke.js';

class DadJoke extends React.Component {
  constructor() {
    super();

    this.saveJoke = this.saveJoke.bind(this);

    this.state = {
      jokeObj: undefined,
      loading: true,
      storedJokes: [],
    }
  }

  async fetchJoke() {
    this.setState(
      { loading: true }, // Primeiro parâmetro da setState()!
      async () => {
      const requestHeaders = { headers: { Accept: 'application/json' } }
      const requestReturn = await fetch('https://icanhazdadjoke.com/', requestHeaders)
      const requestObject = await requestReturn.json();
      this.setState({
        loading: false,
        jokeObj: requestObject
      });
    });
  }

  componentDidMount() {
    this.fetchJoke();
  }

  saveJoke() {
    this.setState(({ storedJokes, jokeObj }) => ({
      storedJokes: [...storedJokes, jokeObj]
    }));

    this.fetchJoke();
  }

  render() {
    const { storedJokes, loading, jokeObj } = this.state;
    const loadingElement = <span>Loading...</span>;

    return (
      <div>
        <span>
          {storedJokes.map(({ id, joke }) => (<p key={id}>{joke}</p>))}
        </span>

      <p>
        {
          loading 
            ? loadingElement
            : <Joke jokeObj={jokeObj} saveJoke={this.saveJoke} />
        }
      </p>

      </div>
    );
  }
}

export default DadJoke;
```

Vimos no vídeo como fazemos para garantir que algo só rode depois do estado ser atualizado! Passamos como segundo parâmetro da `this.setState` uma callback com a dita lógica!

```jsx
this.setState({ meuEstado: novoValor }, () => {
  // ... Sua lógica aqui
})
```

E para o caso mais complicado? Isto é, **atualizar o estado baseado no estado anterior** e **executar alguma lógica somente depois do estado atualizar** ao mesmo tempo?! Nesse caso tanto o primeiro parâmetro quanto o segundo são callbacks!

```jsx
this.setState(
  (estadoAnterior) => ({ meuEstado: estadoAnterior }), // Primeiro parâmetro!
  () => { /* ... Sua lógica aqui */ } // Segundo parâmetro!
)
```

A sintaxe é um tanto confusa, mas guarde isso na sua caixa de ferramentas para fazer lógicas de `Loading...` quando se está esperando a resposta de uma API! E lembre-se: como a `this.setState` não retorna uma promise, usar **async/await** com ela **NUNCA** vai funcionar.

💡 _Aprendemos no vídeo também sobre como atualizar arrays no estado com base no estado anterior! Use o spread operator! `this.setState(({ meuArrayNoEstado }) => ({meuArrayNoEstado: [...meuArrayNoEstado, novoElemento] }))`_


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/1c36f886-88d1-424c-b7b4-d8350620a118/day/31429191-5625-4eb1-9743-0159b322b0d1/lesson/3bb793e9-339f-4837-82f1-4a777395226c)
