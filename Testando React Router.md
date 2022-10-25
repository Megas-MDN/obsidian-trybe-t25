[[History - Histórico]]
[[Mocks Functions]]
[[React Router (Rotas)]]
[[React Testing Library - RTL]]
[[React]]
[[Teste Assincrono]]
[[Testes com Jest]]


1.  A biblioteca `history` nos permite acessar a sessão de histórico do navegador e também a localização atual (URL). 
    
    -   Para os nossos testes, os métodos mais utilizados serão o `push`, que permite mudar de rota dentro do **ambiente de testes**, e o `location.pathname`, que retorna a URL exata em que você está.
        
    -   Dentro da biblioteca, você também importará a `createMemoryHistory`, que é feita para ser utilizada em ambientes que não possuem DOM, como em testes automatizados. O intuito dessa função é criar um novo histórico de navegação para ser utilizado durante o teste. Essa biblioteca é bastante utilizada nesses casos, como veremos no próximo tópico.
        
2.  A função `renderWithRouter` é uma função customizada para fazer testes com rotas, uma vez que a função `render` normal da RTL não dá suporte ao `router`. Ela usa o `createMemoryHistory` para embutir a lógica de _histórico de navegação_ no seu componente renderizado, para uso nos testes.

Agora, vamos praticar o que aprendemos.

Siga os passos abaixo para criar e testar uma aplicação usando _React Router_:

-   Primeiro, utilize o `create-react-app` com o nome que desejar.
-   Depois disso, vamos instalar as dependências que utilizaremos nesse projeto: a `react-router-dom`, `history` e a `@testing-library/react`, com o comando abaixo.
```jsx
npm i react-router-dom@v5
```

-   Por último, vamos copiar esse código para dentro do nosso arquivo `App.js` apagando tudo o que já estiver lá.
```jsx
import React from 'react';
import { Switch, Route, Link } from 'react-router-dom';

export const About = () => <h1>Você está na página Sobre</h1>;
export const Home = () => <h1>Você está na página Início</h1>;
export const NoMatch = () => <h1>Página não encontrada</h1>;

export default function App() {
  return (
    <div>
      <Link to="/">Início</Link>
      <br />
      <Link to="/about">Sobre</Link>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route component={NoMatch} />
      </Switch>
    </div>
  );
};
```

Repare que, para efeito de aprendizado, temos mais de um componente dentro do arquivo `App.js`, por isso o `export default` no componente `App`. Os outros componentes, que estão sendo exportados acima do component `App`, também terão os seus respectivos `exports`. Lembrando que isso **não é uma boa prática**. Estamos fazendo dessa forma para diminuirmos a complexidade da aplicação, com o intuito de facilitar o entendimento.

Outro ponto de atenção é que, quando utilizamos o `export default` e o `export`, a maneira de importar os componentes sofre uma pequena alteração - que veremos na hora de realizar os testes.

Ao terminar de instalar, vamos nos deparar com um problema! A nossa página dará o seguinte erro:
```jsx
You should not use <Link> outside a <Router>
```

Esse erro acontece porque o `BrowserRouter` deve encapsular todos os itens chamados pelo `react-router-dom`, e, no nosso caso, existem dois `<Link>` no `App.js`, o que nos leva a esse erro. Vamos resolver isso colocando a tag `<BrowserRouter>` no arquivo `index.js`, deixando ele da seguinte forma:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

Agora sim! Vamos ao navegador entender o que esse código está fazendo. Basicamente, o nosso código cria um router básico com duas páginas, a **Home** e a **About**, além de criar uma página de **Not Found** para quando a pessoa digitar uma _URL_ que não existe.

Após isso, vamos usar a função `renderWithRouter`, que é uma função _helper_ ou assistente. Uma função _helper_ executa uma tarefa específica e não depende de outras funções.

No nosso caso, a _helper_ criará um histórico e renderizará o componente que iremos testar. Para não ficarmos sem contexto de onde essa função veio, ela foi tirada da documentação oficial da **Testing Library**, que você pode encontrar [aqui.](https://testing-library.com/docs/example-react-router#reducing-boilerplate) Vamos salvar a _helper_ em um arquivo `src/renderWithRouter.js` e entendê-la antes de escrevermos os testes:
```jsx
// src/renderWithRouter.js
import React from 'react';
import { Router } from 'react-router-dom';
import { createMemoryHistory } from 'history';
import { render } from '@testing-library/react';

const renderWithRouter = (component) => {
  const history = createMemoryHistory();
  return ({
    ...render(<Router history={ history }>{component}</Router>), history,
  });
};
export default renderWithRouter;
```

Vamos entender o que está acontecendo em nossa função _helper_:

1.  Fazemos as importações necessárias:
    
    -   Vamos importar o `React` para podermos trabalhar com a criação de componentes em JSX;
        
    -   Vamos importar o `Router` que servirá para termos acesso ao histórico criado pelo `createMemoryHistory`;
        
    -   Vamos importar o `createMemoryHistory` que irá criar nosso histórico em memória durante os testes; e
        
    -   Vamos importar o `render`, assim teremos acesso a todos os seletores que ele possui como `getByText` ou `getByRole`.
        
2.  Feitas as importações, vamos criar nossa função _helper_ chamada `renderWithRouter` e exportá-la como `default`;
    
3.  Recebemos em nossa função `renderWithRouter` um parâmetro `component`, que é o componente que desejamos renderizar em nossos testes;
    
4.  Utilizamos a função `createMemoryHistory` para criar uma variável `history` que armazenará nosso histórico;
    
5.  Por último, retornamos um objeto com as informações necessárias para o teste:
    

-   Todas as propriedades retornadas pelo método `render` também serão retornadas em nosso objeto, pois estamos usando a [Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax). Além disso, também é retornada a nossa constante `history`.
    
-   Repare que a função `render` recebe como parâmetro o componente `<Router />`.
    
-   O `<Router />`, por sua vez, recebe como _props_ `history` a variável que também se chama `history` criada no passo 4.
    
-   Além disso o parâmetro recebido `component` é passado como _children_ para o `<Router />`. Dessa forma, conseguimos renderizar em nossos testes o componente desejado encapsulado pelo `<Router />`.
    

Existe uma forma de fazer sem o `helper`, mas ela implica escrever bem mais código. [Esse link](https://testing-library.com/docs/example-react-router) tem um exemplo muito parecido com o que estamos fazendo, a grande diferença é que lá eles não utilizam uma função auxiliar. Repare que a sintaxe que utilizaremos será bem parecida com a do site, com a diferença de verbosidade que no exemplo do link acima será bem maior.

-   Com a ajuda desta função, vamos escrever muito menos código na hora de testar, porque precisamos apenas chamar a `renderWithRouter`. Não podemos esquecer que devemos colocar o `<BrowserRouter />` encapsulando o componente `<App />` inteiro.
    
-   Para fazermos isso, devemos colocá-lo no `index.js`. Isto é necessário porque queremos ter controle sobre o `BrowserRouter` nos testes. Se ele estiver dentro do componente que vamos testar, nós perderemos o controle sobre ele.
    
-   Uma outra característica dessa função é que ela retorna tanto o componente que passamos como parâmetro, já encapsulado no router, quanto o histórico que geramos, o que também serve para nos levar a outras páginas com facilidade.
    

### Escrevendo os testes da Aplicação

Agora que vimos o App que vamos testar e entendemos a função que vamos utilizar, vamos escrever os testes dentro do arquivo `src/App.test.js`:
```jsx
import React from 'react';
import { screen } from '@testing-library/react';
import renderWithRouter from './renderWithRouter';
import App from './App';

it('deve renderizar o componente App', () => {
  renderWithRouter(<App />);

  const homeTitle = screen.getByRole('heading', {
    name: 'Você está na página Início',
  });
  expect(homeTitle).toBeInTheDocument();
});
```

-   Aqui, fizemos os imports necessários: o próprio `react`, a _helper_ e o _componente_ que vamos testar.
    
-   Importamos o teste em si, que chama a _helper_ passando o _componente_ a ser renderizado. Nesse primeiro caso, mostraremos como renderizar a aplicação toda, fazendo um teste geral, depois vamos ver como renderizar um componente específico.
    
-   Continuando os testes, vamos clicar no link `About` em nossa aplicação e verificar se estamos na página correta.
```jsx
// import React from 'react';
// import { screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
// import renderWithRouter from './renderWithRouter';
// import App from './App';

// it('deve renderizar o componente App', () => {
//   renderWithRouter(<App />);

//   const homeTitle = screen.getByRole('heading', {
//     name: 'Você está na página Início',
//   });
//   expect(homeTitle).toBeInTheDocument();
// });

it('deve renderizar o componente Sobre', () => {
  const { history } = renderWithRouter(<App />);

  const aboutLink = screen.getByRole('link', { name: 'Sobre' });
  expect(aboutLink).toBeInTheDocument();
  userEvent.click(aboutLink);

  const { pathname } = history.location;
  expect(pathname).toBe('/about');

  const aboutTitle = screen.getByRole('heading',
    { name: 'Você está na página Sobre' });
  expect(aboutTitle).toBeInTheDocument();
});
```

-   Com o `userEvent` (que deve ser importado da `@testing-library/user-event`), podemos interagir com os elementos da tela (nesse caso, vamos clicar no link `Sobre`). Depois disso, utilizaremos o `history.location.pathname` para verificar se estamos na página correta e, por último, checamos se o texto que aparece quando clicamos nesse link no navegador foi encontrado.
    
-   Agora que temos mais um caso de uso, é interessante colocar o describe; ele ajudará bastante na hora de separar os testes, e, numa eventual falha, saberemos qual teste falhou. Vamos colocá-lo abaixo:
```jsx
// import React from 'react';
// import { screen } from '@testing-library/react';
// import userEvent from '@testing-library/user-event';
// import renderWithRouter from './renderWithRouter';
// import App from './App';

describe('teste da aplicação toda', () => {
  // it('deve renderizar o componente App', () => {
  //   renderWithRouter(<App />);

  //   const homeTitle = screen.getByRole('heading', {
  //     name: 'Você está na página Início',
  //   });
  //   expect(homeTitle).toBeInTheDocument();
  // });

  // it('deve renderizar o componente Sobre', () => {
  //   const { history } = renderWithRouter(<App />);

  //   const aboutLink = screen.getByRole('link', { name: 'Sobre' });
  //   expect(aboutLink).toBeInTheDocument();
  //   userEvent.click(aboutLink);

  //   const { pathname } = history.location;
  //   expect(pathname).toBe('/about');

  //   const aboutTitle = screen.getByRole('heading',
  //     { name: 'Você está na página Sobre' });
  //   expect(aboutTitle).toBeInTheDocument();
  // });
});
```

-   Encerrando esse teste de aplicação total, vamos testar a página que deveria aparecer ao digitar na barra de endereços uma página que não existe:

```jsx
// import React from 'react';
import { screen, act } from '@testing-library/react';
// import userEvent from '@testing-library/user-event';
// import renderWithRouter from './renderWithRouter';
// import App from './App';

// describe('teste da aplicação toda', () => {
//   it('deve renderizar o componente App', () => {
//     renderWithRouter(<App />);

//     const homeTitle = screen.getByRole('heading', {
//       name: 'Você está na página Início',
//     });
//     expect(homeTitle).toBeInTheDocument();
//   });

//   it('deve renderizar o componente Sobre', () => {
//     const { history } = renderWithRouter(<App />);

//     const aboutLink = screen.getByRole('link', { name: 'Sobre' });
//     expect(aboutLink).toBeInTheDocument();
//     userEvent.click(aboutLink);

//     const { pathname } = history.location;
//     expect(pathname).toBe('/about');

//     const aboutTitle = screen.getByRole('heading',
//       { name: 'Você está na página Sobre' });
//     expect(aboutTitle).toBeInTheDocument();
//   });

  it('deve testar um caminho não existente e a renderização do Not Found', () => {
    const { history } = renderWithRouter(<App />);

    act(() => {
      history.push('/pagina/que-nao-existe/');
    })

    const notFoundTitle = screen.getByRole('heading',
      { name: 'Página não encontrada' });
    expect(notFoundTitle).toBeInTheDocument();
  });
// });
```

-   A diferença nesse caso é que utilizamos a função `history.push()` e passamos como argumento algum link que não existe dentro de nossa aplicação. Depois disso, testamos se ao digitar um caminho para uma página que não existe, o texto que aparece no navegador é encontrado.

Quando utilizamos funções que alteram o estado da aplicação, é recomendado envolvê-las com o `act(() => {...})`. Isso fará com que o teste simule melhor a forma como o _React_ trabalha no seu navegador. Para entender mais sobre `act` você pode consultar a própria [documentação do _React_](https://reactjs.org/docs/test-utils.html#act) e a [documentação do RTL](https://testing-library.com/docs/react-testing-library/api/#act).

#### Testando componentes isoladamente

Até aqui nós aprendemos como testar nossa aplicação renderizando ela por completo. Mas é possível testar os componentes separadamente também. Vamos ver como fazer isso:
```jsx
it('deve renderizar o componente About (apenas componente)', () => {
  renderWithRouter(<About />);

  const aboutTitle = screen.getByRole('heading',
    { name: 'Você está na página Sobre' });
  expect(aboutTitle).toBeInTheDocument();
});
```

-   Você verá que, ao copiar esse test, o `Jest` retornará um erro, dizendo que o componente `About` não foi definido. Isso ocorre porque ele não foi importado nesse arquivo! Altere a linha de import do `App.js` para:
```jsx
  import App, { About } from './App';
```

-   Talvez você esteja se perguntando por que o `App` não foi importado com `{}`, e o `About` foi. Isso aconteceu porque só pode haver um `export default` por arquivo (que faz o componente ser importável sem as chaves `{}`), e o `App` tomou esse espaço, então os outros componentes exportados ficam em “segundo plano”. Por isso, para serem importados corretamente, necessitam do `{}`.
    
-   Para ver a diferença entre a renderização da aplicação inteira e de apenas um componente, cause um erro nos testes, alterando o que é esperado no `getByRole` dos testes. Você verá que, ao importar apenas o componente, toda a estrutura ao redor dele não é renderizada. No nosso caso de exemplo, os links do topo não são renderizados.
