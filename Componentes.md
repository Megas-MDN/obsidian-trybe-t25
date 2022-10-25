[[React]]
[[Classes em React]]

Componentes são a base de toda aplicação **React**. Eles nos permitem segmentar uma página web em blocos de códigos independentes e **reutilizáveis**, além de tornarem o ambiente de desenvolvimento um local mais organizado. Conceitualmente, componentes **React** são **[[Funções]]** ou **[[Classes]]** JavaScript que podem aceitar parâmetros, chamados de [[Props]] (do inglês _properties_), os quais retornam elementos React responsáveis por determinarem o que será renderizado na tela.

Existem duas maneiras de definirmos um componente:
-   com um **Componente de função**
-   com um **Componente de classe**

### Componentes de **função**:
Componentes de função, ou funcionais, são componentes criados apenas com uma função javascript.

```jsx
function Greeting(props) {
  return (
    <h1>Hello, {props.name}</h1>
  );
}

export default Greeting;
```

### Componentes de **classe**:
Componentes de classe são componentes criados através de uma classe que estende a classe `React.Component`.

```jsx
import React from 'react';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

export default Greeting;
```


Analisando o código acima, temos:

1.  A declaração de um componente chamado `Greeting`;
2.  O componente `Greeting` herda da classe `Component` da biblioteca `react`;
3.  O componente `Greeting` descreve **o que vai ser mostrado para quem usar a aplicação**, declarado no método **obrigatório** `render`. Nesse caso, `Greeting` retorna: `<h1>Hello, {this.props.name}</h1>`;
4.  O componente `Greeting` possui como propriedade um **objeto** chamado `props`, que contém todos os dados passados como parâmetro na hora de chamar um componente, ou seja, chamar `<Greeting name="Samuel" />` faz com que o componente tenha uma `prop` igual a `{ name: "Samuel" }`;
5.  Exportamos o componente `Greeting` de forma que ele possa ser reutilizado na aplicação.