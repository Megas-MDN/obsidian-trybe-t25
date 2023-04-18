[[React]]


Para começar a usar o React Router em um aplicativo Web, você precisará de um aplicativo Web React. Se você precisar criar um, recomendamos que você experimente [Create React App](https://github.com/facebook/create-react-app) . É uma ferramenta popular que funciona muito bem com o React Router.

Primeiro, instale `create-react-app` e faça um novo projeto com ele.

## 1º Exemplo: Roteamento Básico

Neste exemplo, temos 3 “páginas” tratadas pelo roteador: uma página inicial, uma página sobre e uma página de usuários. Conforme você clica nos diferentes `<Link>`s, o roteador renderiza os arquivos `<Route>`.

Observação: nos bastidores, a `<Link>`renderiza um `<a>`com um real `href`, portanto, as pessoas que usam o teclado para navegação ou leitores de tela ainda poderão usar este aplicativo.

```jsx
import React from "react";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";

export default function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/users">Users</Link>
            </li>
          </ul>
        </nav>

        {/* A <Switch> looks through its children <Route>s and
            renders the first one that matches the current URL. */}
        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/users">
            <Users />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}
```


## 2º Exemplo: Roteamento Aninhado

Este exemplo mostra como o roteamento aninhado funciona. A rota `/topics`carrega o `Topics`componente, que renderiza quaisquer `<Route>`'s adicionais condicionalmente no valor dos caminhos `:id`.

```jsx
import React from "react";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
  useRouteMatch,
  useParams
} from "react-router-dom";

export default function App() {
  return (
    <Router>
      <div>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>

        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/topics">
            <Topics />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Topics() {
  let match = useRouteMatch();

  return (
    <div>
      <h2>Topics</h2>

      <ul>
        <li>
          <Link to={`${match.url}/components`}>Components</Link>
        </li>
        <li>
          <Link to={`${match.url}/props-v-state`}>
            Props v. State
          </Link>
        </li>
      </ul>

      {/* The Topics page has its own <Switch> with more routes
          that build on the /topics URL path. You can think of the
          2nd <Route> here as an "index" page for all topics, or
          the page that is shown when no topic is selected */}
      <Switch>
        <Route path={`${match.path}/:topicId`}>
          <Topic />
        </Route>
        <Route path={match.path}>
          <h3>Please select a topic.</h3>
        </Route>
      </Switch>
    </div>
  );
}

function Topic() {
  let { topicId } = useParams();
  return <h3>Requested topic ID: {topicId}</h3>;
}
```

# Componentes Primários

Existem três categorias principais de componentes no React Router:

-   roteadores, como `<BrowserRouter>`e`<HashRouter>`
-   correspondências de rotas, como `<Route>`e`<Switch>`
-   e navegação, como `<Link>`, `<NavLink>`, e`<Redirect>`

Também gostamos de pensar nos componentes de navegação como “alteradores de rota”.

Todos os componentes que você usa em um aplicativo da Web devem ser importados do `react-router-dom`.

## Roteadores

No núcleo de cada aplicativo React Router deve estar um componente de roteador. Para projetos web, `react-router-dom`provedores `<BrowserRouter>`e `<HashRouter>`roteadores. A principal diferença entre os dois é a maneira como eles armazenam a URL e se comunicam com seu servidor web.

-   A `<BrowserRouter>`usa caminhos de URL regulares. Geralmente, esses são os URLs mais bonitos, mas exigem que seu servidor seja configurado corretamente. Especificamente, seu servidor web precisa servir a mesma página em todas as URLs que são gerenciadas no lado do cliente pelo React Router. O Create React App oferece suporte pronto para o desenvolvimento e vem com instruções sobre como configurar seu servidor de produção também.
-   A `<HashRouter>`armazena a localização atual na parte `hash`da URL, então a URL se parece com `http://example.com/#/your/page`. Como o hash nunca é enviado ao servidor, isso significa que nenhuma configuração especial do servidor é necessária.

Para usar um roteador, apenas certifique-se de que ele seja renderizado na raiz de sua hierarquia de elementos. Normalmente, você envolverá seu `<App>`elemento de nível superior em um roteador, assim:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";

function App() {
  return <h1>Hello React Router</h1>;
}

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

## Correspondentes de rota

Existem dois componentes de correspondência de rota: `Switch`e `Route`. Quando a `<Switch>`é renderizado, ele pesquisa seus `children` `<Route>`elementos para encontrar um que `path`corresponda ao URL atual. Quando encontra um, ele o processa `<Route>`e ignora todos os outros. Isso significa que você deve colocar s com s `<Route>`mais específicos (normalmente mais longos) **antes** dos menos específicos.`path`

Se não houver `<Route>`correspondência, o `<Switch>`renderiza nada ( `null`).

```jsx
import React from "react";
import ReactDOM from "react-dom";
import {
  BrowserRouter as Router,
  Switch,
  Route
} from "react-router-dom";

function App() {
  return (
    <div>
      <Switch>
        {/* If the current URL is /about, this route is rendered
            while the rest are ignored */}
        <Route path="/about">
          <About />
        </Route>

        {/* Note how these two routes are ordered. The more specific
            path="/contact/:id" comes before path="/contact" so that
            route will render when viewing an individual contact */}
        <Route path="/contact/:id">
          <Contact />
        </Route>
        <Route path="/contact">
          <AllContacts />
        </Route>

        {/* If none of the previous routes render anything,
            this route acts as a fallback.

            Important: A route with path="/" will *always* match
            the URL because all URLs begin with a /. So that's
            why we put this one last of all */}
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </div>
  );
}

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById("root")
);
```

Uma coisa importante a notar é que a `<Route path>`corresponde ao **início** da URL, não a tudo. Portanto, a `<Route path="/">`sempre **corresponderá** ao URL. Por causa disso, normalmente colocamos isso por `<Route>`último em nosso arquivo `<Switch>`. Outra solução possível é usar **o**`<Route exact path="/">` que corresponde ao URL inteiro.

Nota: Embora o React Router suporte `<Route>`elementos de renderização fora de um `<Switch>`, a partir da versão 5.1, recomendamos que você use o `useRouteMatch` gancho. Além disso, não recomendamos que você renderize a `<Route>`sem a `path`e, em vez disso, sugerimos que você use um gancho para obter acesso a quaisquer variáveis necessárias.

## Navegação (ou Trocadores de Rota)

O React Router fornece um `<Link>`componente para criar links em seu aplicativo. Onde quer que você renderize um `<Link>`, uma âncora ( `<a>`) será renderizada em seu documento HTML.

```jsx
<Link to="/">Home</Link>
// <a href="/">Home</a>
```

O `<NavLink>`é um tipo especial de `<Link>`que pode se definir como “ativo” quando seu `to`prop corresponde à localização atual.

```jsx
<NavLink to="/react" activeClassName="hurray">
  React
</NavLink>

// When the URL is /react, this renders:
// <a href="/react" className="hurray">React</a>

// When it's something else:
// <a href="/react">React</a>
```

Sempre que quiser forçar a navegação, você pode renderizar um arquivo `<Redirect>`. Quando um `<Redirect>`renderiza, ele navegará usando seu `to`prop.

```jsx
<Redirect to="/login" />
```

# Renderização do servidor

A renderização no servidor é um pouco diferente, pois é tudo sem estado. A ideia básica é que envolvamos o aplicativo em um arquivo stateless `<StaticRouter>` em vez de um arquivo `<BrowserRouter>`. Passamos a url solicitada do servidor para que as rotas possam corresponder e um `context`prop que discutiremos a seguir.

```jsx
// client
<BrowserRouter>
  <App/>
</BrowserRouter>

// server (not the complete story)
<StaticRouter
  location={req.url}
  context={context}
>
  <App/>
</StaticRouter>
```

Quando você renderiza um `<Redirect>` no cliente, o histórico do navegador muda de estado e obtemos a nova tela. Em um ambiente de servidor estático, não podemos alterar o estado do aplicativo. Em vez disso, usamos o `context`prop para descobrir qual foi o resultado da renderização. Se encontrarmos um `context.url`, saberemos que o aplicativo foi redirecionado. Isso nos permite enviar um redirecionamento adequado do servidor.

```jsx
const context = {};
const markup = ReactDOMServer.renderToString(
  <StaticRouter location={req.url} context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // Somewhere a `<Redirect>` was rendered
  redirect(301, context.url);
} else {
  // we're good, send the response
}
```

## Adicionando informações de contexto específicas do aplicativo

O roteador só adiciona `context.url`. Mas você pode querer que alguns redirecionamentos sejam 301 e outros 302. Ou talvez você queira enviar uma resposta 404 se algum branch específico da interface do usuário for renderizado, ou um 401 se eles não forem autorizados. O suporte de contexto é seu, então você pode alterá-lo. Aqui está uma maneira de distinguir entre redirecionamentos 301 e 302:

```jsx
function RedirectWithStatus({ from, to, status }) {
  return (
    <Route
      render={({ staticContext }) => {
        // there is no `staticContext` on the client, so
        // we need to guard against that here
        if (staticContext) staticContext.status = status;
        return <Redirect from={from} to={to} />;
      }}
    />
  );
}

// somewhere in your app
function App() {
  return (
    <Switch>
      {/* some other routes */}
      <RedirectWithStatus status={301} from="/users" to="/profiles" />
      <RedirectWithStatus
        status={302}
        from="/courses"
        to="/dashboard"
      />
    </Switch>
  );
}

// on the server
const context = {};

const markup = ReactDOMServer.renderToString(
  <StaticRouter context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // can use the `context.status` that
  // we added in RedirectWithStatus
  redirect(context.status, context.url);
}
```

## 404, 401 ou qualquer outro status

Podemos fazer a mesma coisa acima. Crie um componente que adicione algum contexto e o renderize em qualquer lugar do aplicativo para obter um código de status diferente.

```jsx
function Status({ code, children }) {
  return (
    <Route
      render={({ staticContext }) => {
        if (staticContext) staticContext.status = code;
        return children;
      }}
    />
  );
}
```

Agora você pode renderizar um `Status`em qualquer lugar do aplicativo ao qual deseja adicionar o código `staticContext`.

```jsx
function NotFound() {
  return (
    <Status code={404}>
      <div>
        <h1>Sorry, can’t find that.</h1>
      </div>
    </Status>
  );
}

function App() {
  return (
    <Switch>
      <Route path="/about" component={About} />
      <Route path="/dashboard" component={Dashboard} />
      <Route component={NotFound} />
    </Switch>
  );
}
```

## Juntando tudo

Este não é um aplicativo real, mas mostra todas as peças gerais que você precisa para juntar tudo.

```jsx
import http from "http";
import React from "react";
import ReactDOMServer from "react-dom/server";
import { StaticRouter } from "react-router-dom";

import App from "./App.js";

http
  .createServer((req, res) => {
    const context = {};

    const html = ReactDOMServer.renderToString(
      <StaticRouter location={req.url} context={context}>
        <App />
      </StaticRouter>
    );

    if (context.url) {
      res.writeHead(301, {
        Location: context.url
      });
      res.end();
    } else {
      res.write(`
      <!doctype html>
      <div id="app">${html}</div>
    `);
      res.end();
    }
  })
  .listen(3000);
```

E então o cliente:

```jsx
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";

import App from "./App.js";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("app")
);
```

## Carregando dados

Há tantas abordagens diferentes para isso e ainda não há uma prática recomendada clara, então procuramos ser combináveis ​​com qualquer abordagem, e não prescrever ou nos inclinar para uma ou outra. Estamos confiantes de que o roteador pode se adequar às restrições de sua aplicação.

A principal restrição é que você deseja carregar dados antes de renderizar. O React Router exporta a `matchPath`função estática que ele usa internamente para combinar locais com rotas. Você pode usar esta função no servidor para ajudar a determinar quais serão suas dependências de dados antes da renderização.

A essência dessa abordagem depende de uma configuração de rota estática usada para renderizar suas rotas e corresponder antes da renderização para determinar as dependências de dados.

```js
const routes = [
  {
    path: "/",
    component: Root,
    loadData: () => getSomeData()
  }
  // etc.
];
```

Em seguida, use esta configuração para renderizar suas rotas no aplicativo:

```jsx
import { routes } from "./routes.js";

function App() {
  return (
    <Switch>
      {routes.map(route => (
        <Route {...route} />
      ))}
    </Switch>
  );
}
```

Então no servidor você teria algo como:

```js
import { matchPath } from "react-router-dom";

// inside a request
const promises = [];
// use `some` to imitate `<Switch>` behavior of selecting only
// the first to match
routes.some(route => {
  // use `matchPath` here
  const match = matchPath(req.path, route);
  if (match) promises.push(route.loadData(match));
  return match;
});

Promise.all(promises).then(data => {
  // do something w/ the data so the client
  // can access it then render the app
});
```

E, finalmente, o cliente precisará pegar os dados. Novamente, não estamos no negócio de prescrever um padrão de carregamento de dados para seu aplicativo, mas esses são os pontos de contato que você precisará implementar.

Você pode estar interessado em nosso pacote [React Router Config](https://github.com/remix-run/react-router/tree/main/packages/react-router-config) para auxiliar no carregamento de dados e renderização do servidor com configurações de rota estática.

# Restauração de rolagem

Nas versões anteriores do React Router, fornecíamos suporte pronto para uso para restauração de rolagem e as pessoas têm pedido por isso desde então. Espero que este documento o ajude a obter o que você precisa da barra de rolagem e do roteamento!

Os navegadores estão começando a lidar com `history.pushState`a restauração de rolagem por conta própria da mesma maneira que lidam com a navegação normal do navegador. Já funciona no chrome e é muito bom. Aqui está a especificação de restauração de rolagem.

Como os navegadores estão começando a lidar com o “caso padrão” e os aplicativos têm necessidades de rolagem variadas (como este site!), não fornecemos o gerenciamento de rolagem padrão. Este guia deve ajudá-lo a implementar quaisquer necessidades de rolagem que você tenha.

## Role para cima

Na maioria das vezes tudo o que você precisa é “rolar até o topo” porque você tem uma página de conteúdo longa, que quando navegada, permanece rolada para baixo. Isso é simples de lidar com um `<ScrollToTop>`componente que rolará a janela para cima em cada navegação:

```jsx
import { useEffect } from "react";
import { useLocation } from "react-router-dom";

export default function ScrollToTop() {
  const { pathname } = useLocation();

  useEffect(() => {
    window.scrollTo(0, 0);
  }, [pathname]);

  return null;
}
```

Se você ainda não está executando o React 16.8, você pode fazer a mesma coisa com uma `React.Component`subclasse:

```jsx
import React from "react";
import { withRouter } from "react-router-dom";

class ScrollToTop extends React.Component {
  componentDidUpdate(prevProps) {
    if (
      this.props.location.pathname !== prevProps.location.pathname
    ) {
      window.scrollTo(0, 0);
    }
  }

  render() {
    return null;
  }
}

export default withRouter(ScrollToTop);
```

Em seguida, renderize-o na parte superior do seu aplicativo, mas abaixo do roteador

```jsx
function App() {
  return (
    <Router>
      <ScrollToTop />
      <App />
    </Router>
  );
}
```

Se você tiver uma interface de guia conectada ao roteador, provavelmente não desejará rolar para o topo quando eles trocarem de guia. Em vez disso, que tal um `<ScrollToTopOnMount>`nos lugares específicos que você precisa?

```jsx
import { useEffect } from "react";

function ScrollToTopOnMount() {
  useEffect(() => {
    window.scrollTo(0, 0);
  }, []);

  return null;
}

// Render this somewhere using:
// <Route path="..." children={<LongContent />} />
function LongContent() {
  return (
    <div>
      <ScrollToTopOnMount />

      <h1>Here is my long content page</h1>
      <p>...</p>
    </div>
  );
}
```

Novamente, se você ainda não estiver executando o React 16.8, você pode fazer a mesma coisa com uma `React.Component`subclasse:

```jsx
import React from "react";

class ScrollToTopOnMount extends React.Component {
  componentDidMount() {
    window.scrollTo(0, 0);
  }

  render() {
    return null;
  }
}

// Render this somewhere using:
// <Route path="..." children={<LongContent />} />
class LongContent extends React.Component {
  render() {
    return (
      <div>
        <ScrollToTopOnMount />

        <h1>Here is my long content page</h1>
        <p>...</p>
      </div>
    );
  }
}
```

## Solução genérica

Para uma solução genérica (e quais navegadores estão começando a implementar nativamente), estamos falando de duas coisas:

1.  Rolar para cima na navegação para não iniciar uma nova tela rolada para baixo
2.  Restaurando as posições de rolagem da janela e elementos de estouro em cliques de “voltar” e “avançar” (mas não cliques de link!)

Em um ponto, estávamos querendo lançar uma API genérica. Aqui está o que estávamos indo para:

```jsx
<Router>
  <ScrollRestoration>
    <div>
      <h1>App</h1>

      <RestoredScroll id="bunny">
        <div style={{ height: "200px", overflow: "auto" }}>
          I will overflow
        </div>
      </RestoredScroll>
    </div>
  </ScrollRestoration>
</Router>
```

Primeiro, `ScrollRestoration`rolaria a janela para cima na navegação. Segundo, ele usaria `location.key`para salvar a posição de rolagem da janela _e_ as posições de rolagem dos `RestoredScroll`componentes em arquivos `sessionStorage`. Então, quando `ScrollRestoration`os `RestoredScroll`componentes forem montados, eles poderão procurar sua posição de `sessionsStorage`.

A parte complicada foi definir uma API “opt-out” para quando você não quer que a rolagem da janela seja gerenciada. Por exemplo, se você tiver alguma navegação de guia flutuando dentro do conteúdo de sua página, provavelmente _não_ deseja rolar para o topo (as guias podem ser roladas para fora da visualização!).

Quando descobrimos que o Chrome gerencia a posição de rolagem para nós agora e percebemos que aplicativos diferentes terão necessidades de rolagem diferentes, meio que perdemos a crença de que precisávamos fornecer algo – especialmente quando as pessoas querem apenas rolar para o topo (o que você viu é fácil de adicionar ao seu aplicativo por conta própria).


Fonte: https://v5.reactrouter.com/web/guides/scroll-restoration