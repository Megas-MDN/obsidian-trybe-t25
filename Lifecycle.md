[[React]]
[[Fetch API]]
[[API]]
[[DOM]]
[[ReactDOM]]


Os componentes **React**, assim como os seres vivos, possuem um ciclo de vida. O ciclo do React é dividido em 3 etapas. São elas:

-   Montagem: quando o componente é inicializado e inserido no DOM;
-   Atualização: quando as props ou estados do componente são alterados;
-   Desmontagem: quando o componente morre 🧟‍♂️, sumindo do DOM.

Essa é a _big picture_, mas dentro dessas 3 etapas existem vários métodos que podemos interceptar para, assim, agir em determinado momento do ciclo de vida dos componentes.

![[CicloDeVida.png]]

O ciclo de vida é acessível por meio de métodos nativos dos _class components_. Como exemplo, pense no `render`, que é um método de renderização dos _class components_ e que é chamado toda vez que uma atualização acontece. Ele possui características intrínsecas que permitem adicionar o componente no DOM. Assim como o `render`, outros métodos possuem suas próprias características e objetivos.

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


## Entendendo quando cada método é chamado

Vamos agora fazer uma simulação, para ver na prática quando cada método chamado:

```jsx
lass Counter extends React.Component {
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

![[imgconstrutor.webp]]

Atente-se para a ordem de chamada dos métodos. As mensagens refletem a ordem de execução dos métodos de ciclo de vida do componente.

Os métodos `shouldComponentUpdate` e `componentDidUpdate` não apareceram no console, pois não houve atualização. Caso o botão `Soma` seja clicado, teremos mais mensagens no console:

![[imgconstrutor2.webp]]
> As mensagens `‘constructor’, ‘render’, ‘componentDidMount’, ‘shouldComponentUpdate’, ‘render’ e ‘componentDidUpdate’` são exibidas no console do navegador


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

![[imgconstrutor3.webp]]
>Imagem que mostra as mensagens `‘constructor’, ‘render’, ‘componentDidMount’, ‘shouldComponentUpdate’, ‘componentDidUpdate’` e os estados no console.

Perceba que o estado só é de fato atualizado quando chega no método `componentDidUpdate`. Por isso, caso seja necessário impedir uma renderização, você deve utilizar o método `shouldComponentUpdate`, que permite comparar os atuais e próximos estados ou props e adicionar a lógica.

## Requisições e componentDidMount

Vamos falar sobre o método `componentDidMount`, que é um dos mais utilizados em componentes `React` de classe.

Como você já deve ter percebido, trabalhar com requisições a APIs é uma prática muito comum no cotidiano de quem desenvolve. Operações assíncronas requerem uma atenção extra e, para que não ocorram problemas, caso sua requisição tenha que retornar algo para ser renderizado logo que a página carregar, é muito importante que você entenda bem a importância dessa etapa do ciclo de vida.

Para entender melhor, usando React, vamos consumir uma API de Rick and Morty, cujo o endpoint é `https://rickandmortyapi.com/api/character`, e exibir na tela os nomes dos personagens e suas respectivas fotos.

Então, o primeiro passo será criar um `App React` com o já familiar `npx create-react-app my-interdimensional-app` e instalar as dependências:

```jsx
npx create-react-app my-interdimensional-app
cd my-interdimensional-app
npm install
```

Caso você queira ver as coisas acontecendo com um pouco mais de estilo, literalmente, é só substituir o conteúdo de `App.css` por:
```css
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

