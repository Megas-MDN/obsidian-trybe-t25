[[JavaScript]]
[[React]]
[[API]]


Operações em JavaScript são tradicionalmente síncronas, ou seja, para que uma cadeia de operações seja realizada é necessário que uma operação termine para que outra comece. Em uma linha de produção de automóveis, por exemplo, várias etapas de produção são codependentes. Podemos relacionar essas etapas de produção às operações síncronas em JavaScript. Observe o exemplo abaixo para que essa analogia fique mais nítida:
```JavaScript
console.log('1 - Receber roda');
console.log('2 - Encaixar parafusos');
console.log('3 - Fixar roda no carro');
```

Note que existe uma ordem específica de etapas que não pode ser quebrada, pois uma afeta diretamente a outra. Sem roda, não adianta encaixar parafusos; sem encaixar parafusos, fixar a roda não é possível.

Agora, imagine que o nosso estoque de parafusos está chegando ao fim, e que é necessário que façamos uma reposição para que a linha de produção não pare. No entanto, nossa operação não cobre esse tipo de situação e nossa linha de produção para enquanto uma pessoa funcionária irá comprar os parafusos e repor o estoque.
```js
console.log('1 - Comprar parafusos');
console.log('2 - Adicionar ao estoque');
console.log('3 - Receber roda');
console.log('4 - Encaixar parafusos');
console.log('5 - Fixar roda no carro');
```

Observe que estamos trabalhando de forma ineficiente e adicionando etapas desnecessárias à nossa produção, pois, se tivermos parafusos suficientes em estoque, não precisaremos parar a montagem para que mais parafusos sejam comprados e repostos. Assim como na nossa linha de produção, existem operações que não têm essa codependência em JavaScript e com o objetivo de cobrir justamente esse tipo de situação surgem as **operações assíncronas**.

```js
// linhaDeProducao.js

const TWO_SECONDS = 2000;

setTimeout(() => {
  console.log('Comprar parafusos'); // Comprar parafusos
  console.log('Adicionar ao estoque'); // Adicionar ao estoque
}, TWO_SECONDS);

console.log('1 - Receber roda'); // 1 - Receber roda
console.log('2 - Encaixar parafusos'); // 2 - Encaixar parafusos
console.log('3 - Fixar roda no carro'); // 3 - Fixar roda no carro

// Saída:
// 1 - Receber roda
// 2 - Encaixar parafusos
// 3 - Fixar roda no carro
// Comprar parafusos
// Adicionar ao estoque
```

Note que `console.log('Comprar parafusos')` e `console.log('Adicionar ao estoque')` foram declarados antes das etapas `1`, `2` e `3`, e mesmo assim o retorno das chamadas só ocorre ao final, isso acontece porque utilizamos a função `setTimeout`. É muito comum que essa função seja utilizada para simular comportamentos assíncronos.

Na prática, vivenciaremos situações em que nossa aplicação depende de uma informação externa, como, por exemplo, solicitar uma informação a um banco de dados. É aí que o conceito de assincronicidade entra a nosso favor para que nossa aplicação não perca eficiência.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/8ac6fde1-3393-44aa-908d-7cee814f89db/day/698331ce-d7b0-4d92-8c92-7281f556f1bf/lesson/d4986e25-8fa0-4c10-bf90-7efdcb8d1818)