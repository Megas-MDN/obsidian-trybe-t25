[[React Testing Library - RTL]]
[[React Router (Rotas)]]


O termo “`history`” e “ `history` objeto” nesta documentação se refere ao pacote `history`, que é uma das 2 maiores dependências do React Router (além do próprio React), e que fornece várias implementações diferentes para gerenciar o histórico de sessões em JavaScript em vários ambientes.

Os seguintes termos também são usados:

-   “histórico do navegador” - Uma implementação específica do DOM, útil em navegadores da Web que suportam a API de histórico HTML5
-   “histórico de hash” - Uma implementação específica do DOM para navegadores da web legados
-   “memory history” - Uma implementação de histórico na memória, útil em testes e ambientes não DOM como React Native

`historyobjetos` normalmente têm as seguintes propriedades e métodos:

-   `length`- (number) O número de entradas na pilha de histórico
-   `action`- (string) A ação atual ( `PUSH`, `REPLACE`, ou `POP`)
-   `location`- (objeto) A localização atual. Pode ter as seguintes propriedades:
    -   `pathname`- (string) O caminho do URL
    -   `search`- (string) A string de consulta do URL
    -   `hash`- (string) O fragmento de hash de URL
    -   `state`- (objeto) estado específico do local que foi fornecido, por exemplo `push(path, state)`, quando esse local foi colocado na pilha. Disponível apenas no histórico do navegador e da memória.
-   `push(path, [state])`- (função) Empurra uma nova entrada para a pilha de histórico
-   `replace(path, [state])`- (função) Substitui a entrada atual na pilha de histórico
-   `go(n)`- (função) Move o ponteiro na pilha de histórico por `n`entradas
-   `goBack()`- (função) Equivalente a`go(-1)`
-   `goForward()`- (função) Equivalente a`go(1)`
-   `block(prompt)`- (função) Impede a navegação.


## A história é mutável

O objeto histórico é mutável. Portanto, é recomendável acessar a `location` partir das props de renderização de [`<Route>`](https://v5.reactrouter.com/web/api/Route), não de `history.location`. Isso garante que suas suposições sobre o React estejam corretas nos ganchos do ciclo de vida. Por exemplo:

```jsx
class Comp extends React.Component {
  componentDidUpdate(prevProps) {
    // will be true
    const locationChanged =
      this.props.location !== prevProps.location;

    // INCORRECT, will *always* be false because history is mutable.
    const locationChanged =
      this.props.history.location !== prevProps.history.location;
  }
}

<Route component={Comp} />;
```

# Localização

Os locais representam onde o aplicativo está agora, para onde você quer que ele vá ou até mesmo onde estava. Se parece com isso:

```js
{
  key: 'ac3df4', // not with HashHistory!
  pathname: '/somewhere',
  search: '?some=search-string',
  hash: '#howdy',
  state: {
    [userDefined]: true
  }
}
```

O roteador fornecerá um objeto de localização em alguns lugares:

- Route component as this.props.location
- Route render as ({ location }) => ()
- Route children as ({ location }) => ()
- withRouter as this.props.location

Também é encontrado, `history.location` mas você não deve usá-lo porque é mutável. Você pode ler mais sobre isso no documento de [história](https://v5.reactrouter.com/web/api/history) .

Um objeto de localização nunca é modificado para que você possa usá-lo nos ganchos do ciclo de vida para determinar quando a navegação acontece, isso é realmente útil para busca de dados e animação.

```js
componentWillReceiveProps(nextProps) {
  if (nextProps.location !== this.props.location) {
    // navigated!
  }
}
```

Você pode fornecer locais em vez de strings para os vários lugares que navegam:

-   [Link](https://v5.reactrouter.com/web/api/Link/to) da Web para[](https://v5.reactrouter.com/web/api/Link/to)
-   [Link](https://v5.reactrouter.com/native/api/Link/to) nativo para[](https://v5.reactrouter.com/native/api/Link/to)
-   [Redirecionar para](https://v5.reactrouter.com/web/api/Redirect/to)
-   [histórico.push](https://v5.reactrouter.com/web/api/history/push)
-   [histórico.substituir](https://v5.reactrouter.com/web/api/history/push)

Normalmente, você usa apenas uma string, mas se precisar adicionar algum “estado de localização” que estará disponível sempre que o aplicativo retornar a esse local específico, poderá usar um objeto de localização. Isso é útil se você deseja ramificar a interface do usuário com base no histórico de navegação em vez de apenas caminhos (como modais).

```jsx
// usually all you need
<Link to="/somewhere"/>

// but you can use a location instead
const location = {
  pathname: '/somewhere',
  state: { fromDashboard: true }
}

<Link to={location}/>
<Redirect to={location}/>
history.push(location)
history.replace(location)
```

Por fim, você pode passar um local para os seguintes componentes:

-   [Rota](https://v5.reactrouter.com/web/api/Route/location)
-   [Trocar](https://v5.reactrouter.com/web/api/Switch/location)

Isso impedirá que eles usem a localização real no estado do roteador. Isso é útil para animação e navegação pendente, ou sempre que você quiser enganar um componente para renderizar em um local diferente do real.

# [Combine](https://v5.reactrouter.com/web/api/match)

Um `match`objeto contém informações sobre como `<Route path>`correspondeu ao URL. `match`objetos contêm as seguintes propriedades:

-   `params`- (objeto) Pares de chave/valor analisados ​​a partir da URL correspondente aos segmentos dinâmicos do caminho
-   `isExact`- (booleano) `true`se o URL inteiro foi correspondido (sem caracteres à direita)
-   `path`- (string) O padrão de caminho usado para corresponder. `<Route>`Útil para construir s aninhados
-   `url`- (string) A parte correspondente do URL. `<Link>`Útil para construir s aninhados

Você terá acesso a `match`objetos em vários lugares:

-   [Componente de rota](https://v5.reactrouter.com/web/api/Route/component) como`this.props.match`
-   [Rota renderizada](https://v5.reactrouter.com/web/api/Route/render-func) como`({ match }) => ()`
-   [Encaminhar crianças](https://v5.reactrouter.com/web/api/Route/children-func) como`({ match }) => ()`
-   [com roteador](https://v5.reactrouter.com/web/api/withRouter) como`this.props.match`
-   [matchPath](https://v5.reactrouter.com/web/api/matchPath) como o valor de retorno
-   [useRouteMatch](https://v5.reactrouter.com/web/api/hooks/useroutematch) como o valor de retorno

Se uma rota não tiver um `path`e, portanto, sempre corresponder, você obterá a correspondência principal mais próxima. O mesmo vale para `withRouter`.

## [correspondências nulas](https://v5.reactrouter.com/web/api/match/null-matches)

Um `<Route>`que usa o `children`prop chamará sua `children`função mesmo quando a rota `path`não corresponder à localização atual. Quando este for o caso, o `match`será `null`. Ser capaz de renderizar `<Route>`o conteúdo de um 's quando ele corresponde pode ser útil, mas alguns desafios surgem dessa situação.

A maneira padrão de “resolver” URLs é unir a `match.url`string ao caminho “relativo”.

```js
let path = `${match.url}/relative-path`;
```

Se você tentar fazer isso quando a partida for `null`, você terminará com um `TypeError`. Isso significa que é considerado inseguro tentar unir caminhos “relativos” dentro de a `<Route>`ao usar o `children`prop.

Uma situação semelhante, mas mais sutil, ocorre quando você usa um pathless `<Route>`dentro de um `<Route>`que gera um `null`objeto de correspondência.

```js
// location.pathname = '/matches'
<Route path="/does-not-match"
  children={({ match }) => (
    // match === null
    <Route
      render={({ match: pathlessMatch }) => (
        // pathlessMatch === ???
      )}
    />
  )}
/>
```

Pathless `<Route>`s herdam seu `match`objeto de seu pai. Se o pai `match`for `null`, a correspondência também será `null`. Isso significa que a) quaisquer rotas/links filhos terão que ser absolutos porque não há pai para resolver e b) uma rota sem caminho cujo pai `match`possa ser `null`precisará usar o `children`prop para renderizar.

# [matchPath](https://v5.reactrouter.com/web/api/matchPath)

Isso permite que você use o mesmo código de correspondência `<Route>`usado, exceto fora do ciclo de renderização normal, como reunir dependências de dados antes de renderizar no servidor.

```js
import { matchPath } from "react-router";

const match = matchPath("/users/123", {
  path: "/users/:id",
  exact: true,
  strict: false
});
```

## [nome do caminho](https://v5.reactrouter.com/web/api/matchPath/pathname)

O primeiro argumento é o nome do caminho que você deseja corresponder. Se você estiver usando isso no servidor com Node.js, seria `req.path`.

## [adereços](https://v5.reactrouter.com/web/api/matchPath/props)

O segundo argumento são os adereços a serem comparados, eles são idênticos aos adereços de correspondência aceitos `Route`. Também pode ser uma string ou uma matriz de strings como atalho para `{ path }`:

```js
{
  path, // like /users/:id; either a single string or an array of strings
  strict, // optional, defaults to false
  exact, // optional, defaults to false
}
```

## [retorna](https://v5.reactrouter.com/web/api/matchPath/returns)

Ele retorna um objeto quando o nome do caminho fornecido corresponde a `path`prop.

```js
matchPath("/users/2", {
  path: "/users/:id",
  exact: true,
  strict: true
});

//  {
//    isExact: true
//    params: {
//        id: "2"
//    }
//    path: "/users/:id"
//    url: "/users/2"
//  }
```

Ele retorna `null`quando o nome do caminho fornecido não corresponde a `path`prop.

```js
matchPath("/users", {
  path: "/users/:id",
  exact: true,
  strict: true
});

//  null
```

# [com Roteador](https://v5.reactrouter.com/web/api/withRouter)

Você pode obter acesso às [`history`](https://v5.reactrouter.com/web/api/history)propriedades do objeto e aos [`<Route>`](https://v5.reactrouter.com/web/api/Route)'s mais próximos [`match`](https://v5.reactrouter.com/web/api/match)por meio do `withRouter`componente de ordem superior. `withRouter`passará atualizados `match`, `location`e `history`props para o componente encapsulado sempre que renderizar.

```jsx
import React from "react";
import PropTypes from "prop-types";
import { withRouter } from "react-router";

// A simple component that shows the pathname of the current location
class ShowTheLocation extends React.Component {
  static propTypes = {
    match: PropTypes.object.isRequired,
    location: PropTypes.object.isRequired,
    history: PropTypes.object.isRequired
  };

  render() {
    const { match, location, history } = this.props;

    return <div>You are now at {location.pathname}</div>;
  }
}

// Create a new component that is "connected" (to borrow redux
// terminology) to the router.
const ShowTheLocationWithRouter = withRouter(ShowTheLocation);
```

#### Nota importante

`withRouter`não assina mudanças de localização como o React Redux `connect`faz para mudanças de estado. Em vez disso, renderiza novamente após as alterações de local se propagarem para fora do `<Router>`componente. Isso significa que `withRouter`não _é_ renderizado novamente em transições de rota, a menos que seu componente pai seja renderizado novamente.

#### Métodos estáticos e propriedades

Todos os métodos e propriedades estáticos específicos que não reagem do componente encapsulado são copiados automaticamente para o componente "conectado".

## [Component.WrappedComponent](https://v5.reactrouter.com/web/api/withRouter/componentwrappedcomponent)

O componente encapsulado é exposto como propriedade estática `WrappedComponent`no componente retornado, que pode ser usado para testar o componente isoladamente, entre outras coisas.

```jsx
// MyComponent.js
export default withRouter(MyComponent)

// MyComponent.test.js
import MyComponent from './MyComponent'
render(<MyComponent.WrappedComponent location={{...}} ... />)
```

## [wrapedComponentRef: func](https://v5.reactrouter.com/web/api/withRouter/wrappedcomponentref-func)

Uma função que será passada como `ref`prop para o componente encapsulado.

```jsx
class Container extends React.Component {
  componentDidMount() {
    this.component.doSomething();
  }

  render() {
    return (
      <MyComponent wrappedComponentRef={c => (this.component = c)} />
    );
  }
}
```

###### Fonte: https://v5.reactrouter.com/web/api/history
