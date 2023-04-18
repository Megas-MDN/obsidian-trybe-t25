[[JavaScript]]
[[React]]


De modo geral, função é um "subprograma" que pode ser _chamado_ por código externo (ou interno no caso de recursão) à função. Assim como o programa em si, uma função é composta por uma sequência de instruções chamada _corpo da função_. Valores podem ser _passados_ para uma função e ela vai _retornar_ um valor.

Em JavaScript, funções são objetos de primeira classe, pois elas podem ter propriedades e métodos como qualquer outro objeto. O que as difere de outros objetos é que as funções podem ser chamados. Em resumo, elas são objetos [`Function`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Function).

## Descrição

Toda função em JavaScript é um objeto `Function`. Veja `Function` para informação das propriedades e métodos dos objetos `Function`.

Funções não são como procedimentos (_procedure_). Uma função sempre retorna um valor, mas um procedimento pode ou não retornar um valor.

Para retornar um valor diferente do padrão, uma função deve ter uma instrução [return](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/return) que específica o valor a ser retornado. Uma função sem um `return` retornará um valor padrão. No caso de um [método construtor](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) chamado com a palavra reservada [`new`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/new), o valor padrão é o valor do parâmetro `this`. Para todas as outras funções, o valor padrão de retorno é `undefined`.

Os parâmetros de uma função são chamados de argumentos da função. Argumentos são passados para a função _por valor_. Se uma função muda o valor de um argumento, esta mudança não é refletida globalmente ou na chamada da função. Contudo, referência de objetos são valores também, e eles são especiais: se a função muda as propriedades do objeto referenciado, estas mudanças são visíveis fora da função, como é mostrado no exemplo a seguir:

```js
/* Declare a função 'minhaFunção' */
function minhaFuncao(objeto) {
   objeto.marca = "Toyota";
 }

 /*
  * Declare a variável 'meucarro';
  * crie e inicialize um novo Objeto;
  * atribua referência para 'meucarro'
  */
 var meucarro = {
   marca: "Honda",
   modelo: "Accord",
   ano: 1998
 };

 /* Exibe 'Honda' */
 console.log(meucarro.marca);

 /* Passe a referência do objeto para a função */
 minhaFuncao(meucarro);

 /*
  * Exibe 'Toyota' como valor para a propriedade 'marca'
  * do objeto, mudado pela função.
  */
 console.log(meucarro.marca);
```

A palavra reservada [`this`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/this) não se refere a função sendo executada no momento, então você deve referenciar um objeto `Function` pelo nome, mesmo dentro do corpo da função.

## Definindo funções

Há várias maneiras de definir funções:

### Declaração de função (Instrução `function`)

```js
function nome([param[, param[, ... param]]]) {
   instruções
}
```

`nome`

O nome da função.

`param`

O nome de um argumento a ser passado para a função.

`instruções`

As instruções que formam o corpo da função.

### A expressão function (Operador `function`)
```js
function [nome]([param] [, param] [..., param]) {
   instruções
}
```

`nome`

O nome da função. Pode ser omitido, e neste caso a função é conhecida como função anônima.

`param`

O nome de um argumento a ser passado para a função.

`instruções`

As instruções que formam o corpo da função.


### O construtor `Function`

**Nota:** O uso do construtor Function para criar funções não é recomendado uma vez que é requerido o corpo da função como string, o que pode impedir algumas otimizações por parte do motor JS e pode também causar outros problemas.

Como todos os outros objetos, objetos [`Function`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Function) podem ser criados usando o operador new:

new Function (arg1, arg2, ... argN, corpoDaFuncao)

`arg1, arg2, ... argN`

Nenhum ou mais nomes para serem usados pela função como nomes formais de argumentos. Cada um deve ser uma string em conformidade com as regras para um identificador JavaScript válido ou uma lista com tais strings separadas por vírgula; por exemplo "x", "oValor", ou "a, b".

_corpoDaFuncao_

Uma string contento as instruções JavaScript correspondendo a definição da função.

Invocar o construtor Function como uma função (sem usar o operador new) the o mesmo efeito de invocá-lo como um construtor comum.

###### Fonte: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Functions