[[JavaScript]]

A declaração **`do...while`** cria um laço que executa uma declaração até que o teste da condição for falsa (false). A condição é avaliada depois que o bloco de código é executado, resultando que uma declaração seja executada pelo menos uma vez.

## Sintaxe
```js
do
   declarações
while (condition);
```

`Declarações`

A declaração é executada pelo menos uma vez e re-executada cada vez que a condição (`condition`) for avaliada como verdadeira (true). Para executar múltiplas declarações dentro do laço, use um `block` declaração (`{ ... }`) ao grupo dessas declarações.

`condição`

Uma expressão é validade depois de cada passagem pelo laço. Se a condição `(condition)` é avaliada como verdadeira (true) o bloco de código é executado novamente. Quando a condição `(condition)` é avaliada como falsa (false), o controle passa para a instrução seguinte ao laço **do...while**.

## Exemplos

### Usando `do...while`

No exemplo seguinte, o laço **do...while** soma pelo menos uma vez e executa novamente até `i` não ser menor que 5.

```js
var resultado = '';
var i = 0;
do {
   i += 1;
   resultado += i + ' ';
} while (i < 5);
document.getElementById('exemplo').innerHTML = resultado;
```



###### Fonte: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/do...while