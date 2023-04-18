[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]


O método `every()` testa se todos os elementos do array passam pelo teste implementado pela função fornecida. Este método retorna um valor booleano.

## Sintaxe

arr.every(callback[, thisArg])

### Parâmetros

`callback`

Função que testa cada elemento, recebe três parametros:

`currentValue` (obrigatório)

O elemento atual sendo processado na array.

`index` (opcional)

O índice do elemento atual sendo processado na array.

`array` (opcional)

O array de origem.

`thisArg`

Opcional. Valor a ser usado como `this` quando o `callback` é executado.

### Valor de retorno

**true** se a função de callback retorna um valor [truthy](https://developer.mozilla.org/pt-BR/docs/Glossary/Truthy) para cada um dos elementos do array; caso contrário, **false**.

## Descrição

O método `every` executa a função `callback` fornecida uma vez para cada elemento presente no array, até encontrar algum elemento em que a função retorne um valor false (valor que se torna false quando convertido para boolean). Se esse elemento é encontrado, o método `every` imediatamente retorna false. Caso contrário, se a função `callback` retornar true para todos elementos, o método retorna true. A função `callback` é chamada apenas para os elementos do array original que tiverem valores atribuídos; os elementos que tiverem sido removidos ou os que nunca tiveram valores atribuídos não serão considerados.

A função `callback` é chamada com três argumentos: o valor do elemento corrente, o índice do elemento corrente e o array original que está sendo percorrido.

Se o parâmetro `thisArg` foi passado para o método `every`, ele será repassado para a função `callback` no momento da chamada para ser utilizado como o `this`. Caso contrário, o valor `undefined` será repassado para uso como o _`this`_. O valor do `this` a ser repassado para o `callback` é determinado de acordo com as [regras usuais para determinar o this visto por uma função](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/this).

O método `every`não modifica o array original.

A lista de elementos que serão processados pelo `every` é montada antes da primeira chamada da função `callback`. Se um elemento for acrescentado ao array original após a chamada ao `every` , ele não será visível para o callback. Se os elementos existentes forem modificados, os valores que serão repassados serão os do momento em que o método `every` chamar o `callback`. Elementos removidos não serão considerados.

`every` funciona como o qualificador "for all" em matemática. Particularmente, para um vetor vazio, é retornado true. ([É verdade por vacuidade](https://pt.wikipedia.org/wiki/Verdade_por_vacuidade) que todos os elementos do [conjunto vazio](https://pt.wikipedia.org/wiki/Conjunto_vazio) satisfazem qualquer condição.)

## Exemplos

### Testando tamanho de todos os elementos do vetor

O exemplo a seguir testa se todos elementos no array são maiores que 10.

```
function isBigEnough(element, index, array) {
  return element >= 10;
}
[12, 5, 8, 130, 44].every(isBigEnough);   // false
[12, 54, 18, 130, 44].every(isBigEnough); // true
```


### Usando [[Arrow Functions]]

Arrow functions fornecem sintaxe mais curta para o mesmo teste.

```
[12, 5, 8, 130, 44].every(elem => elem >= 10); // false
[12, 54, 18, 130, 44].every(elem => elem >= 10); // true
```

###### Fonte: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/every