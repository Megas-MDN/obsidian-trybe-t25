[[React]]
[[MAP]]
[[Array]]

Suponha que você precise implementar um componente que renderiza uma lista de compras. Entretanto, você não sabe de antemão os elementos desta lista. Como você renderizaria dinamicamente esta lista de compras?

Imagine que temos a seguinte lista a ser renderizada de maneira dinâmica:

```jsx
const shoppingList = ['leite', 'arroz', 'feijão', 'banana', 'carne'];
```

O primeiro passo é criar uma coleção de elementos. Para isso, iteramos sobre `shoppingList` com uma **HOF** que retorne, **em um novo array**, cada item da lista envolvido por um elemento `<li>`. A seguir, atribuímos o array resultante para a variável `items`.

```jsx
// o console log foi adicionado para facilitar a compreensão
const items = shoppingList.map((item) => {
  console.log('item: ', item);
  return (<li>{ item }</li>);
});
```

Agora, só nos resta renderizar a lista que acabamos de criar! Para isso, dentro do escopo do `return`, devemos fazer o uso das chaves `{ }` e utilizar, dentro dela, a constante de elementos criada anteriormente.

> É por meio das chaves que o React irá diferenciar o que é código a ser executado e o que deve ser apenas impresso para leitura:

```jsx
1import React from 'react';
2
3class App extends React.Component {
4  render() {
5    const shoppingList = ['leite', 'arroz', 'feijão', 'banana', 'carne'];
6    const items = shoppingList.map((item) => {
7      console.log('item: ', item);
8      return (<li>{ item }</li>);
9    });
10
11    return (
12      <div>
13        <h2>Lista de compras</h2>
14        <ul>
15          { items }
16        </ul>
17      </div>
18    );
19  }
20}
21
22export default App;
```

Pronto! Agora já podemos renderizar múltiplos componentes de forma dinâmica, sem quaisquer problemas, certo? Quase!

Ao executar o código acima, receberemos, pelo `console`, um alerta de que uma `key` deve ser definida para cada item renderizado. Essas `keys` são importantes para o **React** identificar, com precisão, quais itens foram adicionados, removidos ou alterados.

Como atribuímos e quais devem ser os valores dessas `keys`? 
Resposta: O melhor valor para uma `key` é um que seja único para cada item da lista, como, por exemplo, um `ID`. No entanto, nem sempre dispomos de um `ID` estável em mãos, tal qual o caso do nosso código acima.

Para solucionarmos esse problema, podemos utilizar o índice gerado no segundo parâmetro da nossa **HOF**. Para atribuirmos a `key`, adicionamos na própria `<li>` o atributo `key` com um valor que seja único, exemplo:

```jsx
const items = shoppingList.map((item, index) => (
  <li key={ index }>{ item }</li>
));
```

Vale ressaltar que não é recomendado o uso de índices como `keys` em listas que possibilitam a **alteração na ordem dos itens**, pois podem impactar negativamente o desempenho da aplicação ou gerar problemas relacionados ao estado do componente.