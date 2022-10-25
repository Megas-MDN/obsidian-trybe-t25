[[React]]

## Single Page Application

Antes de começar a falar sobre `React Router`, é preciso entender um tipo de aplicação chamado `Single Page Application` (`SPA`), haja visto que aplicações em `React Router` são `SPA`s.


### props.children

Children é uma ótima ferramenta para reutilização de componentes. A utilização é bem simples, veja abaixo:
```jsx
class App extends Component {
  render() {
    return (
      <div className='main'>
        <ComponentePai>
          <p>SUPIMPA</p>
        </ComponentePai>
      </div>
    )
  }
}
```

E dessa forma podemos acessar e exibir na tela o valor `SUPIMPA` no `ComponentePai`:
```jsx
const ComponentePai = (props) => {
  return (
    <div>
      {props.children}
    </div>
  )
}
```

Nesse exemplo utilizamos uma tag `p`, mas note que poderia ser um ou vários elementos de qualquer natureza, seja uma tag, ou até um componente. Ainda sim, ela é acessada da mesma forma dentro de `ComponentePai`. É importante perceber que, no caso acima, `props.children` é um **objeto** por ser apenas um elemento. Caso o `ComponentePai` esteja com mais de um elemento dentro como no exemplo abaixo, `props.children` se torna um **array de objetos**, com as informações de cada filho.
```jsx
class App extends Component {
  render() {
    return (
      <div className='main'>
        <ComponentePai>
          <p>SUPIMPA</p>
          <h1>BACANA</h1>
          <span>INCRÍVEL</span>
        </ComponentePai>
      </div>
    )
  }
}
```

### Instalação React Router Dom

Para poder fazer uso de `React Router`, é preciso que se instale em uma aplicação **_React_** o pacote [react-router-dom:](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom)
```bash
1npm install react-router-dom@v5
```

Recentemente foi lançada uma atualização para o pacote `react-router-dom` que trouxe _breaking changes_, ou seja, mudanças que não são compatíveis com as versões anteriores.

#### `BrowserRouter`

`BrowserRouter` é o componente que encapsula a sua aplicação, de forma a te possibilitar fazer uso de navegação.

-   Você pode encapsular os componentes diretamente no `App.js`:
```jsx
// ./src/App.js
import { BrowserRouter } from 'react-router-dom';
// ...
<BrowserRouter>
  <Home />
  <About />
</BrowserRouter>
// ...
```

-   Outra forma é encapsulando o próprio componente `<App />`, no arquivo `index.js`. Assim, todos os componentes renderizados por `App` poderão fazer uso da navegação:
```jsx
// ./src/index.js
import { BrowserRouter } from 'react-router-dom';
// ...
<BrowserRouter>
  <App />
</BrowserRouter>
// ...
```

Em muitos casos não faz diferença onde você coloca o `<BrowserRouter />` - se no App.js ou no index.js. Entretanto, se sua aplicação possui testes, é comum adicionar o `<BrowserRouter />` no index.js para que sua aplicação possa ser testada de forma mais eficiente. Mas isso será melhor aprofundado quando formos estudar testes.


#### O componente `Route`

`Route` é o componente fundamental em `React Router`, que estabelece o mapeamento entre o caminho de _URL_ declarado com o componente. Tal mapeamento, no que diz respeito à correspondência entre o caminho da _URL_ atual e a presente no componente, pode ser feito das seguintes formas, ilustradas pelos seguintes exemplos:

-   O caminho da _URL_ atual do navegador _começa_ com o caminho `/about`, declarado na prop `path` no componente `Route`. Dessa forma, se o caminho da _URL_ for `/about`, o componente `About` será renderizado:
```jsx
<Route path="/about" component={ About } />
```

Entretanto, se a _URL_ atual for `/about/me`, por exemplo, também existirá correspondência, e o componente `About` continuará sendo renderizado. Nesse caso, o parâmetro **exact** pode entrar em ação:
```jsx
<Route exact path="/about" component={ About } />
```

Se houver uma correspondência **exata** entre o caminho da _URL_ atual e o caminho `/about` declarado em `Route`, o componente será renderizado. Por outro lado, se o caminho da _URL_ atual for `/about/me`, não haverá correspondência exata, logo o componente `About` não será renderizado.

-   Outra maneira de renderização de componente com `Route` é fazendo uso do elemento `children`. Ou seja, se o seu código estiver assim: `<Route path="/about" component={About} />`, você também poderá fazer da seguinte forma:
```jsx
  <Route path="/about" >
    <About />
  </Route>
```

#### Componentes renderizados

Se houver vários componentes apresentando correspondência entre seu caminho de _URL_ e o caminho atual da aplicação, **todos os componentes apresentando correspondência serão renderizados**. Ou seja, suponha que houvesse a seguinte lista de componentes do tipo `Route`:
```jsx
<Route path="/about" component={ About } />
<Route path="/contact" component={ Contact } />
<Route path="/" component={ Home } />
```

Se o caminho atual da _URL_ da aplicação for `/`, **todos** esses componentes serão renderizados, haja vista que nenhuma rota faz correspondência exata entre o caminho da _URL_, definido via prop `path`. Assim, `path="/"` faz correspondência com qualquer caminho de _URL_.

Agora, se o caminho atual da _URL_ da aplicação for `/contact`, os componentes `Contact` e `Home` serão renderizados. Isso pode ser um problema, e uma forma de atacá-lo é organizar essas rotas via componente `Switch`, que você verá com mais detalhes em instantes. 😉

### Componente `Link`

`Link` é o componente a ser usado no lugar de elementos com a tag `a`, de forma a disponibilizar navegação por _URL_ na sua aplicação `SPA` sem o recarregamento de página que a tag `a` exige. Ou seja, se você quiser definir um link que leve quem usa sua aplicação para a _URL_ com o caminho `/about`, você poderia chamar o componente `Link` da seguinte forma:
```jsx
<Link to="/about" > About </Link>
```

E lembre-se: palavras, imagens, até mesmo outros componentes podem ser componentes filhos do `Link`! Ser filho do `Link` significa que, se você clicar neste filho, irá para onde o `Link` te direciona!

### Componentes `Route` com passagem de props

Sobre o componente `Route`, podemos aprender:

-   No que diz respeito ao componente `Route`, você pode associar um componente com o caminho da _URL_ via `children`, `component` **ou** `render`;
    
-   Faz-se uso da prop `component` de `Route` quando **não é necessário** passar informações adicionais via props para o componente a ser mapeado. Ou seja, se você tem um componente `About` que não precisa de props setadas para ser chamado, e você precisa mapeá-lo para o caminho de _URL_ `/about`, você poderia criar uma rota da seguinte forma: `<Route path="/about" component={About} />`;
    
-   Já a prop `render` de `Route` é usada quando **é necessário** passar informações adicionais via props para o componente a ser mapeado. Ou seja, se você tem um componente `Movies` que precisa receber uma lista de filmes via props `movies`, e você precisa mapeá-lo para o caminho de _URL_ `/movies`, você poderia criar uma rota da seguinte forma: `<Route path="/movies" render={(props) => <Movies {...props} movies={['Cars', 'Toy Story', 'The Hobbit']} />} />`;
    
-   Tanto `component` quanto `render` permitem que você tenha acesso a informações de rota (`match`, `location` e `history`) via props do componente que você está mapeando. Ou seja, se você tem a rota `<Route path="/about" component={About} />`, `About` terá `match`, `location` e `history` setadas via props.
    

### Componentes `Route` com passagem de parâmetro (rotas dinâmicas)

O interessante em rotas dinâmicas é que podemos utilizar o mesmo componente para renderizar vários caminhos diferentes. Para fazer uso de parâmetro de _URL_ em `Route`, é preciso fazer uso da sintaxe `:nome_do_parametro` dentro da propriedade `path`. Ou seja, `<Route path="/movies/:movieId" component={Movie} />` vai definir um parâmetro chamado `movieID`, e o componente `Movie` é mapeado a qualquer um dos seguintes caminhos de _URL_:

-   `/movies/1`;
-   `/movies/2`;
-   `/movies/thor`.

### Componente `Switch`

O componente `Switch` é usado para encapsular um conjunto de rotas que são definidas via `Route`, conforme podemos observar na imagem abaixo:
![[Pasted image 20221024122456.png]]
> Imagem que mostra o componente Switch envolvendo duas rotas da aplicação

Dada a _URL_ atual da aplicação, o `Switch` procura **de cima para baixo** pelo **primeiro** `Route` que possuir correspondência entre seu caminho definido na prop `path` do componente e a _URL_ atual da aplicação. Ou seja, se tivermos um `Switch` com as rotas abaixo:
```jsx
<Switch>
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
  <Route path="/movies" component={Movies} />
  <Route path="/" component={Home} />
</Switch>
```

Ao mudarmos a _URL_ da aplicação para que seu caminho seja `/contact`, **somente** o componente `Contact` será renderizado.

Todos os filhos de um `Switch` devem ser `Route` ou `Redirect`. Apenas o primeiro filho que corresponder ao local atual será renderizado. Se não houvesse o `Switch` mais de um componente poderia ser renderizado na mesma rota de forma errada.

Em uma comparação direta, é como o `switch case` do `javascript`:

**É apenas uma comparação, não utilize o exemplo abaixo.**
```jsx
  switch (rota) {
    case '/about':
      return <About />;
    case '/contact':
      return <Contact />;
    case '/movies':
      return <Movies />;
    default:
      return <Home />
  }
```

### Componente `Redirect`

Conforme o próprio nome diz, `Redirect` é um componente que permite **ativamente** levar quem usa a aplicação para diferentes locais dela. Um caso de uso bastante comum de `Redirect` é autenticação: a pessoa só pode acessar informações sensíveis (tipo conta bancária) de uma aplicação _se_ ela já estiver autenticada; caso contrário, ela é _redirecionada_ para uma página de login. Veja um exemplo de utilização abaixo:
```jsx
  <Switch>
    <Route path="/dashboard" component={Dashboard} />
    <Route exact path="/">
      {logado ? <Redirect to="/dashboard" /> : <Login />}
    </Route>
  </Switch>
```

Caso a aplicação tenha o caminho `/` será feita uma verificação na variável `logado`, no caso de `true` a página será redirecionada para o caminho `/dashboard` e então renderizará o componente `Dashboard`, caso contrário, renderizará o componente `Login`.

Dê sempre **prioridade** para a utilização de `Redirect` para redirecionar, uma vez que, ele é criado para isso.

Para que você tenha um pouco mais de contexto, observe a imagem abaixo que compara o `Link` e o `Redirect`:

![[Pasted image 20221024122554.png]]
> Imagem que exemplifica o uso do Link e Redirect.

### Utilizando o `history.push()`

Uma outra forma de alternarmos entre as rotas da nossa aplicação é utilizando outra função do `react-router-dom`, o `history.push`. Quando chamada, ela altera a rota da página de acordo com o que passarmos como parâmetro.

O `history` é um objeto que possui o histórico contendo diversas informações das rotas que utilizamos na aplicação. Podemos acessá-lo por meio das _props_ dos nossos componentes. Executando a função `history.push('/nome-da-rota')` podemos direcionar a pessoa usuária para qualquer rota que desejarmos.

Vamos entender o funcionamento do `history.push` na prática! Crie uma nova aplicação _React_ com o comando `npx create-react-app exemplo-history` e instale o Router com o comando `npm install react-router-dom@v5`.

Crie um diretório `pages` com dois arquivos:

-   `Home.jsx`

```jsx
import React from 'react';

class Home extends React.Component {
  render() {
    return (
      <h1>Home Page</h1>
    );
  }
}

export default Home;

```

-   `Welcome.jsx`

```jsx
import React from 'react';

class Welcome extends React.Component {
  render() {
    return (
      <h1>Boas vindas</h1>
    );
  }
}

export default Welcome;

```

Por fim, modifique o componente `<App />` para que fique assim:
```jsx
import React from 'react';
import { BrowserRouter, Route, Switch } from 'react-router-dom';
import Welcome from './pages/Welcome';
import Home from './pages/Home';

class App extends React.Component {
  render() {
    return (
      <BrowserRouter>
        <Switch>
          <Route exact path="/" component={ Home } />
          <Route path="/welcome" component={ Welcome } />
        </Switch>
      </BrowserRouter>
    );
  }
}

export default App;

```

Essa é uma aplicação simples contendo duas páginas. Agora vamos criar um botão na página `Home` que fará com que a pessoa usuária, ao clicar nesse botão, seja direcionada para a página `/welcome`. Para isso, utilizaremos o `history.push`.
```jsx
import React from 'react';

class Home extends React.Component {
  render() {
    const { history } = this.props;
    return (
      <>
        <h1>Home Page</h1>
        <button
          type="button"
          onClick={ () => history.push('/welcome') }
        >
          Acesse a página de Boas-Vindas
        </button>
      </>
    );
  }
}

export default Home;

```

Passando o parâmetro `/welcome` ao `history.push()` fará com que, ao ser clicado, o botão direcione a pessoa usuária para a página `welcome`.

Uma das vantagens de se utilizar essa função é que, com ela, é possível transferirmos informações entre as rotas. Por exemplo, poderíamos transferir as informações do estado de um componente para outro. Para isso, basta adicionarmos um segundo parâmetro à função.

Mas atenção aqui: se você estiver usando muito a estratégia de “passar informações” no segundo argumento do `history.push`, isso pode ser sinal de que sua aplicação não está bem estruturada. Uma estratégia melhor talvez seja a de [[elevar o estado]](https://pt-br.reactjs.org/docs/lifting-state-up.html).

Mas vamos ao exemplo.
```jsx
import React from 'react';

class Home extends React.Component {
  constructor() {
    super();
    this.state = {
      userName: 'Tryber',
      role: 'Admin',
    };
  }

  render() {
    const { history } = this.props;
    return (
      <>
        <h1>Home Page</h1>
        <button
          type="button"
          onClick={ () => history.push('/welcome', this.state) }
        >
          Acesse a página de Boas-Vindas
        </button>
      </>
    );
  }
}

export default Home;

```

Dessa forma, ao clicar no botão, a pessoa usuária será direcionada para a página `/welcome` e, ainda, teremos acesso ao `this.state` do componente `Home`.

Para acessar esse valor no componente `Welcome`, podemos buscar a chave `location.state`, do `history`.
```jsx
import React from 'react';

class Welcome extends React.Component {
  render() {
    const { history } = this.props;
    const { location } = history;
    return (
      <>
        <h1>Boas vindas,</h1>
        <h2>
          {
            location.state ? location.state.userName : 'Pessoa desconhecida'
          }
        </h2>
        <button
          type="button"
          onClick={ () => console.log(history) }
        >
          History
        </button>
      </>
    );
  }
}

export default Welcome;

```

No exemplo acima, o componente busca a chave `location.state` do `history`. Se essa chave possuir algum valor, ele irá renderizar `location.state.userName`, que é um valor presente no estado do componente `Home`.

Experimente remover o segundo parâmetro do `history.push()` no componente `Home`. Se você fizer isso, irá reparar que o componente `Welcome` não possuirá a informação do estado do componente `Home` e irá renderizar `Pessoa desconhecida`.

O `history` possui diversas informações. Clique no botão `History` contendo o `console.log(history)` e analise o seu `console` 👀.

Outra chave bastante utilizada do `history` é `location.pathname`. Essa chave irá retornar a rota que a pessoa usuária está acessando. No exemplo acima, altere o código do botão para `console.log(location.pathname)` e veja o retorno no seu `console`. Essa informação pode ser muito valiosa para montar algumas lógicas nas suas aplicações 😉.

### Entendendo o fluxo dos componentes do React Router

Para deixar explícito o comportamento do React Router, deixamos o mapa mental a seguir. Use com moderação. 😉

![Mapa mental de React Router](https://content-assets.betrybe.com/prod/Mapa%20mental%20de%20React%20Router.png)

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/1c36f886-88d1-424c-b7b4-d8350620a118/day/6bfa2e2e-4802-4b72-8aeb-b7b55ad63189/lesson/690c6596-3602-4827-a0c7-0dae3598caeb)
