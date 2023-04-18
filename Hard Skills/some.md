[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]

O método **`some()`** testa se ao menos um dos elementos no array passa no teste implementado pela função atribuída e retorna um valor **`true`** ou **`false`**.

## Sintaxe
```js
arr.some(callback[, thisArg])
```

### Parâmetros

`callback`

Função para testar cada elemento, recebendo três argumentos:

`currentValue`

O valor atual do elemento sendo processado no array.

`index`

O índice do elemento atual sendo processado no array.

`array`

O array onde o método `some()` foi chamado.

`thisArg`

Opcional. Valor para usar como _`this`_ durante a execução do `callback`.

### Valor de retorno

Esta função retorna **`true`** se a função callback retornar **`true`** para qualquer elemento do array; caso contrário, **`false`**.

## Descrição

`some()` executa a função callback uma vez para cada elemento presente no array até achar um onde o `callback` retorne um valor _true_. Se em qualquer dos elementos o valor for encontrado, `some()` imediatamente retorna `true`. Caso contrario, `some()` retorna `false`. `callback` é invocado somente para índices do array que contenham valor definido; não é invocado para índices que foram deletados ou os quais nunca tiveram valor definido.

`callback` é invocado com três argumentos: o valor do elemento, o índice do elemento, e o array onde a função foi chamada.

Se o parâmetro `thisArg` foi passado ao `some()`, ele sera passado ao `callback` quando o mesmo for invocado, para ser usado como o valor de `this` internamente na função callback. Caso contrario, o valor [`undefined`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/undefined) será passado para uso como `this`. O valor `this` observado pela `callback` é determinado de acordo com as regras usuais para determinar o que é visto por uma função.

`some()` não altera o array dentro do qual ele é chamado.

O intervalo de elementos processado por `some()` é definido antes da primeira invocação da `callback`. Elementos contidos no array antes da chamada `some()` ser iniciada não serão testados pela _callback_. Se algum elemento pertencente ao array for alterado pela `callback`, o valor passado para a `callback` será o valor do momento em que a função `some()` encontra o índice daquele elemento. Elementos deletados não são testados.

## Exemplos

### Testando valores de elementos de um array

O exemplo a seguir testa se algum elemento de um array é maior que 10.

```js
function isBiggerThan10(element, index, array) {
  return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```


### Testando valores de elementos de um array usando arrow functions

[[Arrow Functions]] fornece uma sintaxe mais curta para o mesmo teste.

```jsx
[2, 5, 8, 1, 4].some(elem => elem > 10);  // false
[12, 5, 8, 1, 4].some(elem => elem > 10); // true
```

###### Fonte: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/some