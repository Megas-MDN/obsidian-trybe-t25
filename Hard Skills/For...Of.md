[[For]]
[[JavaScript]]
[[Array]]


O loop `for...of` percorre objetos iterativos (incluindo Array, Map, Set), chamando uma função personalizada com instruções a serem executadas para o valor de cada objeto distinto.
_________________

## Sintaxe

>`for` (variavel `of` iteravel) {
 > declaração
>}

### **variável**
A cada iteração, um valor de uma propriedade diferente é atribuido à variável.

### **iteravel**
Objeto cujos atributos serão iterados.
___________
## EX:

```JavaScript
let iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}
// 10
// 20
// 30
```
