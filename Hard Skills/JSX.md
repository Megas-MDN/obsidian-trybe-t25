[[React]]
[[JavaScript]]
[[DOM]]

O JSX, ou `Javascript Syntax Extension`, como o próprio nome sugere, é uma extensão de sintaxe para Javascript. Sua utilização é recomendada pela documentação do React, pois ela demonstra como a interface deverá se comportar, de forma lógica e descritiva.

```jsx
const element = <h1>Hello, world!</h1>;
```

>⚠️ **Atenção** ⚠️
Os códigos com a sintaxe JSX só funcionam dentro do contexto do React, ou seja, não funcionam em JS puro ou rodando diretamente no console do navegador, por exemplo. Você pode brincar com o JSX em exemplos interativos do CodeSandbox que aparecem no conteúdo ou em scripts .js ou .jsx que importam o React em projetos criados pelo comando npx create-react-app.

A construção de um elemento JSX é bem parecida com um elemento HTML, com pequenas diferenças para que não haja conflito do HTML com o JS. Um exemplo disso é a declaração de uma class no HTML, que é substituída por className no JSX, pois haveria conflito de sintaxe com as classes do JS.

Caso fossemos declarar a mesma variável sem o JSX, precisaríamos utilizar funções como o createElement que recebe como parâmetro um componente, um objeto com as props e o conteúdo que será encapsulado por este componente. Seriam necessárias sequências relativamente longas de instruções de código para conseguirmos montar e manipular uma árvore de componentes. Para visualizarmos essa complexidade, vamos refazer o código acima sem o JSX:

```jsx
const element = React.createElement('h1', null, 'Hello, world')
```

Agora imagine uma aplicação inteira sendo construída dessa forma. Ficaria muito mais difícil de ser compreendida, certo? O JSX encaixa-se perfeitamente para resolver este dilema.

É importante frisar que o uso do JSX em aplicações React não é obrigatório, mas a complexidade da construção de uma aplicação fica menor e o código fica mais intuitivo quando o utilizamos.

### Incorporando expressões no JSX

Por ser um código Javascript, o JSX permite injeções de algoritmos dentro da estrutura HTML. Portanto, é possível que se aplique diretamente na estrutura da aplicação códigos que renderizarão outras diversas expressões, por exemplo:

```jsx
const nome = 'Jorge Maravilha';
const element = <h1>Hello, {nome}</h1>;
```

E se aprofundarmos um pouco mais chamando uma função na nossa constante element?

```jsx
function nomeCompleto (nome, sobrenome) {
  return `${nome} ${sobrenome}`;
}

const element = <h1>Hello, {nomeCompleto('Jorge', 'Maravilha')}</h1>;
```

Agora, vamos incorporar a nossa constante element na função helloWorld, retornar um código JSX e encapsulá-la em uma div:

```jsx
function helloWorld (nome, sobrenome) {
  return <h1>Hello, {`${nome} ${sobrenome}`}</h1>;
}

const element = helloWorld('Jorge', 'Maravilha');
const container = <div>{element}</div>;
```

No JSX é necessário substituir class por className, para evitar conflitos entre o Javascript e o HTML, mas também podemos utilizar expressões Javascript para atribuir valor à este atributo.

```jsx
const nome = 'Jorge Maravilha';
const classe = 'hello-class';
const element = <h1 className={classe}>Hello, {nome}</h1>;
```

