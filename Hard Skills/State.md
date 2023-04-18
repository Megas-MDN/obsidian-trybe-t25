[[React]]
[[Componentes]]
[[Eventos via DOM]]
[[Props]]


Um estado representa um momento de um componente dinâmico. Se o seu componente é um relógio, o _estado atual_ dele é a hora atual. Se o seu componente é uma tabela cujo conteúdo muda de acordo com o que o usuário clica na página, o estado dele contém o conteúdo da tabela. Se o seu componente fosse um jogo de videogame, o estado seria o momento em que você está no jogo, a sua quantidade de vidas, a sua munição, seus itens etc. Estado é, então, um _momento_ de algo _que pode mudar ao longo do tempo (dinâmico)_. É uma **informação** que você quer preservar enquanto o componente está interagindo com quem usa.

Eventos no React são como os `eventListeners` do JavaScript: você os associa aos elementos que exibirá na tela, e eles nortearão como cada componente reage a uma ação de quem usa.

```jsx
1import React from 'react';
2import './App.css';
3
4class App extends React.Component {
5  constructor() {
6    super();
7    /* Para definir um estado inicial ao componente, a ser definido
8    no momento em que o componente for colocado na tela, faça uma atribuição
9    de um objeto à chave `state` do `this`, ou seja, ao `this.state` */
10    this.state = {
11      numeroDeCliques: 0,
12    };
13    this.handleClick = this.handleClick.bind(this);
14  }
15  handleClick() {
16    /* Você **NUNCA** deve fazer atribuições diretamente a `this.state`. Deve,
17    ao invés disso, SEMPRE utilizar a função `this.setState(novoEstado)` do
18    React */
19    this.setState({
20      numeroDeCliques: 1,
21    });
22  }
23  render() {
24    /* Para LER o estado, você pode usar `this.state.chaveDoMeuEstado` */
25    const { numeroDeCliques } = this.state;
26    return (
27      <button
28        type="button"
29        onClick={ this.handleClick }
30      >
31        { numeroDeCliques }
32      </button>
33    );
34  }
35}
36export default App;
```


Você **NUNCA** deve atribuir valores ao estado diretamente com `this.state`. O estado é atualizado de forma assíncrona pelo React, para garantir performance, e o React não garante a ordem em que as atualizações ocorrerão. Se você fizer uma atribuição direta, terá problemas! Faça-o sempre através da função `this.setState(meuNovoObjetoQueRepresentaOEstado)`. **NÃO** se esqueça disso! 😃

Mas se a a atualização do estado não ocorre em ordem, vocês perguntam, _“como eu atualizo meu estado com base no estado anterior? Se tudo ocorre fora de ordem, como eu sei que uma conta de `novoEstado = estadoAtual + 1` não dará problemas?”_

Pois bem! Lembre-se de que, com Promises, para garantir que algum código executasse somente após o retorno da Promise, que é assíncrona, você tinha que colocá-lo dentro da função `.then`. Aqui a lógica é da mesma natureza:

```jsx
import React from 'react';
2import './App.css';
3
4class App extends React.Component {
5  constructor() {
6    super();
7    this.state = {
8      numeroDeCliques: 0,
9    };
10    this.handleClick = this.handleClick.bind(this);
11  }
12
13  handleClick() {
14    /* Passando uma callback à função setState, que recebe de parâmetros
15    o estado anterior e as props do componente, você garante que as atualizações
16    do estado acontecerão uma depois da outra! */
17    this.setState((estadoAnterior, _props) => ({
18      numeroDeCliques: estadoAnterior.numeroDeCliques + 1,
19    }));
20  }
21
22  render() {
23    const { numeroDeCliques } = this.state;
24    return (
25      <button
26        type="button"
27        onClick={ this.handleClick }
28      >
29        { numeroDeCliques }
30      </button>
31    );
32  }
33}
34
35export default App;
```

#### Definindo o estado inicial através de Public Class Fields

Até agora vimos que podemos definir o estado inicial através do `constructor`. Uma outra maneira de definir o estado inicial de seus componentes é utilizando a sintaxe `Public Class Fields`. É uma forma mais simples e menos verbosa de definirmos nosso estado. Utilizando essa sintaxe, podemos fazer esta declaração fora de nosso `constructor`. Vamos ver nosso exemplo acima com essa sintaxe:
```jsx
import React from 'react';
2import './App.css';
3
4class App extends React.Component {
5  constructor() {
6    super();
7    // Removemos a declaração do estado de dentro do construtor
8    // this.state = {
9    //   numeroDeCliques: 0,
10    // };
11
12    this.handleClick = this.handleClick.bind(this);
13  }
14
15  // Fazemos a definição do estado utilizando a sintaxe Public Class Field
16  state = {
17    numeroDeCliques: 0,
18  };
19
20  handleClick() {
21    this.setState((estadoAnterior, _props) => ({
22      numeroDeCliques: estadoAnterior.numeroDeCliques + 1,
23    }));
24  }
25
26  render() {
27    const { numeroDeCliques } = this.state;
28    return (
29      <button type="button" onClick={ this.handleClick }>
30        { numeroDeCliques }
31      </button>
32    );
33  }
34}
35
36export default App;
```

💡 _Se você quisesse chamar, no elemento, um evento passando um parâmetro, você deveria trocar a sintaxe `<button onClick{this.minhaFuncao} ...>` por `<button onClick={() => this.minhaFuncao('meu parametro')}`. Basicamente, substitua a função do evento por uma chamada à mesma feita via [[Callback]]!


## State vs Props

Você pode entender a diferença `props` vs `state` da seguinte forma:

-   `props` são uma forma de passar dados de pai para filho.
-   `state` é reservado para dados que seu componente controla.

O conceito é: `state`, ou estado do componente, deve servir para guardar valores do **Componente** que mudam com o uso dele. As props são valores fixos que um componente recebe e não altera.

Pelos princípios do `React`, você **nunca** deve tentar alterar o que um componente recebe como `props`, como no exemplo abaixo:

Copiar

```jsx
this.props.name = 'novo nome';
```