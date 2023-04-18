[[JavaScript]]
[[DOM]]
[[--HTML e CSS]]

O `React` é uma biblioteca `JavaScript` criada pelo Facebook para o desenvolvimento de aplicações front-end. Ele é baseado em componentes, o que permite o reaproveitamento de código e facilita a manutenção. No padrão de arquitetura MVC — Model View Control — ou Modelo Visão Controle, em português, ele é comparado ao desenvolvimento da camada View, que é a interface com o usuário (UI).

## Sintaxe do React:

A sintaxe do React utiliza o conceito de JSX (conceito que será abordado ao decorrer do artigo), mas, ele é basicamente uma mistura de JavaScript com HTML, fornecendo uma estrutura similar ao XML. Ela pode assustar algumas pessoas desenvolvedoras iniciantes, mas, com o tempo, essa estrutura fica mais nítida em nossa mente. Vejamos um exemplo dessa sintaxe:

```jsx
function HelloWorld() {
    
    return (
       <div>
         <h1>olá mundo!!</h1>
      </div>
   )
}
export default HelloWorld;
```

Por meio dessa função HelloWorld, retornamos o valor entre as tags `<h1>` e exportamos essa função para ser utilizada em algum outro componente ou até mesmo no componente principal.

## Quais as principais aplicações do React?

#### Single Page Applications (SPA)
- Single Page Applications seriam aplicações que possuem páginas únicas. Elas utilizam o padrão REST para atualizar o conteúdo com requisições AJAX.

- Seu objetivo é facilitar o desenvolvimento front-end por meio de componentes reutilizáveis, tanto para a web quanto para aplicações em dispositivos móveis.

#### Criação de páginas dinâmicas, como blogs e sites institucionais;
- O React, além de poder ser utilizado para páginas estáticas, também pode ser utilizado para o desenvolvimento de páginas dinâmicas, como blogs, sites institucionais e todo tipo de site que necessitará de uma atualização constante de suas informações. 

#### Criação de dispositivos móveis (aplicativos)
- O React Native é utilizado para criar aplicações em dispositivos móveis para Android e iOS. A grande vantagem da biblioteca é que apenas uma codificação pode ser utilizada nas duas plataformas, garantindo mais produtividade no desenvolvimento para aplicativos móveis. 

- Assim como na versão do React para web, o React Native também trabalha com a utilização de componentes e utiliza a sintaxe JSX para o desenvolvimento da aplicação. Para permitir a renderização conforme a plataforma, a biblioteca utiliza APIs em Swift, necessárias para o iOS, e em Kotlin para serem utilizadas no Android.

#### Utilização com backend
- A biblioteca pode ser utilizada com qualquer tipo de linguagem de back-end, ou seja, a aplicação pode ser em PHP, Java, etc. 

#### Utilização com bibliotecas de front-end
- Além disso, ela funciona em conjunto com outras bibliotecas ou frameworks JavaScript, como Bootstrap, jQuery e Tailwind.


## **Como funciona o React? Principais características!**

O React tem algumas funcionalidades que o tornam uma biblioteca eficiente para o desenvolvimento de aplicações front-end com elementos interativos. Confira, a seguir, algumas de suas características.

### Virtual DOM
Para entender como o React funciona é preciso conhecer a estrutura de uma página HTML e de que forma ela é manipulada. A página HTML é formada por uma série de tags que representam cada elemento de um conteúdo. Já o DOM — Document Object Model — é uma representação estruturada de todos os elementos da página e é utilizado para facilitar as alterações nesses elementos.

O React cria um DOM Virtual para permitir a manipulação dos elementos da página. Basicamente, ele realiza uma cópia do DOM em memória, faz as alterações necessárias conforme a determinação das instruções programadas e atualiza o navegador de forma inteligente. Esse processo oferece mais agilidade na manipulação das páginas.

### O que é o React router DOM?
O React.Router DOM é a biblioteca responsável pela criação de rotas dinâmicas em sua aplicação e também pelo funcionamento das mesmas. Para instalar essa biblioteca em nosso projeto, devemos executar o seguinte comando:

```JSX
npm install react-router-dom
```

Nessa biblioteca, encontramos alguns componentes, os seguintes:

#### BrowserRouter:
**Função raiz dessa biblioteca,** ou seja, todas as rotas precisam estar dentro desse escopo, senão, não serão acessadas. 

#### Route:
**Faz a renderização de uma página ou componente**, quando o caminho dela (que chamamos **path**), for igual ao esperado. 

#### Switch:
**Utilizado para quando há várias rotas.** Seu funcionamento é similar a estrutura switch case existente em algumas linguagens de programação, pois, a partir de um momento que uma rota é encontrada, a busca é encerrada. 

#### Link:
**Permite navegação entre as páginas de um jeito mais eficiente, sem a mesma ter um reload,** como é feito com a tag <a href=”#”></a> no HTML;


## **Componentes React**

A principal característica do React é permitir a criação de componentes que podem ser reutilizados em diversas páginas. Na prática, são blocos de códigos reutilizáveis que agregam funcionalidades e que retornam ao código HTML após a renderização pelo navegador.

Os objetos em uma página podem ser dinâmicos, quando seus dados são alterados, ou estáticos, que mantêm seu conteúdo inalterado. Por exemplo, é possível declarar um título `<h1>` com um determinado conteúdo. Se ele for dinâmico, significa que é manipulado por uma função responsável por alterar o valor atribuído inicialmente a ele.

No React, o estado dos elementos da página pode ser acessado em um componente. Basicamente, existem dois tipos de componentes, que tratam esse estado de forma diferenciada. O componente que não monitora o estado dos elementos é chamado de Stateless. Desse modo, ele conta com um objeto de propriedade em que é atribuído o seu valor fixo.

Já o modelo Stateful tem um objeto de propriedade para a atribuição de seu valor original e um objeto de estado, responsável pelas mudanças que ocorrem no conteúdo desse componente.

### [[Props]]

**As props seriam as propriedades que um componente possui e que podem ser uma ou várias.** Imagine esse componente declarado por você, no caso a função produto, que retorna uma frase com a tag h2:

```jsx
function Produto() {
    return <h2>Olá, {props.nome}, você comprou o produto {props.produto}, pelo preço de {props.preco}</h2>
}
function App() {
    return (
        <div>
            <Produto nome="Luis" produto="Feijão" preco="R$ 4,22" />
            <Produto nome="Fernanda" produto="Farinha de mandioca" preco="R$ 3,29" />
            <Produto nome="Hernandes" produto="Fubá mimoso" preco="R$ 2,99" />
        </div>
    );
}
export default App;
```

Ao invocar o componente, você está passando algumas propriedades a ele, tais como: 

-   **nome**: nome do(a) comprador(a); 
-   **produto**: nome do produto; 
-   **preco**: preço do produto.

Essas propriedades que você está passando ao componente são valores que não podem ser alterados pela pessoa usuária, independentemente da ação que ele fizer, pois, esses valores são imutáveis, similares com variáveis constantes declaradas.

### [[State]]

**O state seria o estado da aplicação e, ele é gerenciado com as variáveis utilizando o hook useState. Nesse caso, os valores podem ser alterados mediante a ação da pessoa usuária,** diferentemente das props. 

O exemplo para esse caso seria um contador simples. Quando você clicar no botão “Incrementar”, ele vai somar o item inicial (que seria o 0 + 1, depois somará 1 + 1 e ficará 2) e assim por diante. 

A mesma coisa ocorre com o botão “Decrementar”, mas ele, ao invés de somar 1, vai diminuir 1. Ou seja, há a alteração dos números na tela mediante a uma ação do usuário, que seriam os cliques no botão do contador. Vejamos o código abaixo:

```jsx
import React, { useState } from 'react'
function App() {
  const [contador, setContador] = useState(0);
  const handleIncrement = () => {
    setContador(contador + 1);
  }
  const handleDecrement = () => {
    setContador(contador - 1);
  }
  return (
    <div>
      <button onClick={handleIncrement}>Incrementar</button>
      <p>{contador}</p>
      <button onClick={handleDecrement}>Decrementar</button>
    </div>
  )
}
export default App;
```

###### Fonte: https://blog.betrybe.com/react/