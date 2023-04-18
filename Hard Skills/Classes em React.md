[[React]]
[[Classes]]

Você pode pensar que uma classe e uma função são exatamente a mesma coisa, afinal, ambas recebem atributos, e nós as chamamos em seguida. Porém, uma classe pode possuir `métodos`, que nada mais são do que ações que toda entidade criada a partir de uma classe pode realizar.

Em `React`, classe é uma das formas de renderizar os componentes na página. Então, quando um componente precisa ser alterado, utilizamos componentes de classe, para que possamos utilizar seus estados para realizar essas alterações.

Podemos atribuir vários `métodos`, os quais podem, inclusive, alterar o próprio estado do objeto. Por enquanto, só precisamos saber que `métodos` existem e não precisamos nos preocupar, pois veremos com detalhes os `métodos de classe` mais adiante em `React`, junto com `estado da aplicação`.

A principal diferença entre o uso de componentes por classe e o uso de componentes por função reside no fato de aqueles gerados por classe terem acesso a métodos e ao estado próprios de qualquer componente React gerado via classe, como o método `render()`, que te permite renderizar todo o conteúdo criado na tela, os quais são acessíveis somente por componentes criados por classe na maior parte das versões do React. A sintaxe para criar um componente com classes é a seguinte:

```jsx
import React from 'react';

class ReactClass extends React.Component {
  render() {
    return (
      <h1>My first React Class Component!</h1>
    )
  }
}
```

***Reparou que o nome do componente começa com letra maiúscula? Essa é uma convenção importante do React, para diferenciar os componentes dos elementos HTML.**

