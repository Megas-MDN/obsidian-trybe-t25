[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]


O `reduce` é diferente das outras _HOFs_: ele recebe dois parâmetros sendo o primeiro uma callback e o segundo um valor inicial, que é opcional. Como o próprio nome diz o `reduce` busca reduzir um array. Isto é, iterando em elementos de um array, ao final ele gera um valor único de qualquer tipo, como, por exemplo, a soma de todos os elementos de tal array. Como principais vantagens do uso do método `reduce` podemos destacar:

-   escrita de código mais limpo;
-   maior facilidade ao implementar a lógica com a qual se quer trabalhar;
-   melhor manutenção de código.

Veja abaixo a estrutura completa do `reduce`:
```js
reduce((accumulator, currentValue, currentIndex, array) => { /* ... */ }, initialValue )
```

A callback, que é o primeiro parâmetro do reduce, também pode receber até quatro parâmetros. Desses quatro parâmetros apenas dois deles devem existir obrigatoriamente, sendo eles o `acc` e o `curr`. Temos então que `acc` abreviatura de `accumulator` ou `acumulador`, deve obrigatoriamente ser o primeiro parâmetro da callback e o `curr`, abreviatura de `currentValue` ou `valor atual` também obrigatório, deve ser o segundo parâmetro da callback. Sendo assim, para trabalhar com uma função de reduce você deve ter algo parecido com o código abaixo:
```js
array.reduce((acc, curr) => {
      // escopo de execução da função
}, valorInicial)
```

Lembrando que `initialValue` ou `valorInicial` não é um parâmetro obrigatório do `reduce` e que a callback pode receber até quatro parâmetros, mas aqui vamos abordar os obrigatórios, o `acc` e o `curr`.

O que então faz o `acumulador` ou `acc`? A função do `acumulador` é guardar o retorno da callback, a cada iteração, tendo como ponto de partida o `valorInicial` quando estabelecido. Quando não estabelecido, automaticamente o `acc` assume o valor do primeiro elemento do array que está iterando. Confira o código abaixo onde vamos calcular a soma total dos elementos de um array:
```js
const numbers = [1, 32, 44, 2, 3];
const iteracoesDoReduce = numbers.reduce((acc, curr) => {
  console.log(`valor atual é ${curr}`);
  // Antes da primeira iteração o valor de início do `acc` é o valor no index 0 do array, e o valor de início de `curr` é o valor no index 1 do array.
      // Iteração 1: valor do acc é 1 e o de curr é 32;
 // Após a primeira iteração, o valor de `acc` muda e passa a acumular agora o resultado do retorno da callback (acc + curr).
     // Iteração 2: valor do acc é 33 e o de curr é 44;
// Acontece então uma segunda iteração, e `curr` agora assume o valor do index na sequência do array, no caso o valor do segundo index e `acc` segue armazenando os retornos.
    // Iteração 3: valor do acc é 77 e o de curr é 2;
    // Iteração 4: valor do acc é 79 e o de curr é 3;
    // Valor final de `acc`é 82 e `curr` para no 3.
  return acc +  curr // Ao fim das iterações podemos ver que o `acc` armazenou o resultado total do retorno da função.
});
console.log(`O resultado final é ${iteracoesDoReduce}`);
  // por fim, esse console.log imprime o retorno final da nossa função.
```

Ao observar o código acima identificamos também o papel do `curr`, que sempre armazena o valor do elemento atual, ou seja, o elemento do array que está sendo iterado no momento.

Passando um valor para o `acc`:

Confuso 🤔? Vamos a outro exemplo! Imagine que novamente você queira somar todos os valores de um array. Mas agora teremos um valor inicial já estipulado para o `acc`. Antes de conhecer o `reduce`, você faria algo parecido com o código abaixo, correto?

```js
const numbers = [1, 32, 44, 2, 3];
let sumNumbers = 30;
// A variável `sumNumbers` tem um valor inicial de 30 e vai acumulando, a cada iteração do for, o resultado da operação feita em seu escopo!
for (let index = 0; index < numbers.length; index += 1) {
  sumNumbers += numbers[index];
}
console.log(sumNumbers); // 112
```

Veja o mesmo feito com `reduce`:
```js
const numbers = [1, 32, 44, 2, 3];
const totalSum = numbers.reduce((acc, curr) => {
  console.log(`valor do acc é ${acc} e o de curr é ${curr}`);
   // Iteração 1: valor do acc é 30 e o de curr é 1
   // Iteração 2:valor do acc é 31 e o de curr é 32
   // Iteração 3: valor do acc é 63 e o de curr é 44
   // Iteração 4: valor do acc é 107 e o de curr é 2
   // Iteração 5: valor do acc é 107 e o de curr é 3
   // Valor final de `acc`é 112 e `curr` para no 3
  return acc + curr;
}, 30); // O `valorInicial` é 30, ou seja, `acc` antes de executar a primeira iteração já está armazenando esse valor.

console.log(`valor final do acc é ${totalSum}`);
  // por fim, esse `console.log` imprime o retorno da nossa função, que é o valor final de `acc` após cada uma das 5 iterações, tendo iniciado com valor 30.
```

Pode parecer estranho definir um valor fixo para o `acumulador`, mas isso porque estamos trabalhando com números. O `reduce` é uma ferramenta poderosa e em um código mais complexo ele poderia receber um valor dinâmico, através de uma variável ou até mesmo qualquer valor que não seja um número.

Vale lembrar também que você aprendeu a usar o `reduce` com seus dois primeiros parâmetros, mas embora pouco utilizados, existem mais dois parâmetros opcionais: `index` e `array`. Veja exemplos utilizando todos os quatro parâmetros do `reduce` acessando sua [documentação](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

Dissecando as funções:

Basicamente o reduce funciona como o funil no gif abaixo:
![[Reduce.gif]]

E na prática, qual a vantagem de se usar o `reduce` 🤔? Vamos dissecar a diferença ao usar o `for` e ao usar o `reduce`:

Método `for`:

-   Necessidade de criar uma variável para acumular o resultado de cada iteração do `for`, a soma de cada resultado - `let sumNumbers`;
-   Necessidade de setar um valor inicial para variável - `sumNumbers = 30`;

Método `.reduce`:

-   A função callback passada por parâmetro recebe dois parâmetros, o acumulador `acc` e o elemento do array de cada iteração, `curr`;
    -   Como a função é uma _arrow function_ que possui apenas uma linha, o retorno de cada iteração será: `acc + curr`;
    -   O retorno é salvo no primeiro parâmetro , `acc`. É como se você estivesse fazendo igual à primeira função, `sumNumbers = sumNumbers + numbers[index]`, mas nesse caso seria `acc = acc + curr`;

Organizando para simplificar:

Veja também que ao invés de passar a lógica direto dentro da callback do `reduce`, você pode criar uma função externa e chamá-la como sendo o parâmetro callback:
```js
const numbers = [1, 32, 44, 2, 3];
const sumNumbers =  (acc, curr) => acc + curr;
const totalSum = numbers.reduce(sumNumbers, 30);
console.log(totalSum); //112
```

Dessa maneira seu código fica mais organizado e você poderá reutilizar a função `sumNumbers` caso seja necessário.

> **Anota aí ✍️ :** acc e curr são apenas nomes costumeiros, você pode dar o nome que quiser para o seu código, sendo uma boa opção escolher nomes semânticos, de acordo com o que é executado pela função em questão.

Outros exemplos de uso do `reduce`:

Hora de olhar outro exemplo para fixar e mostrar outras formas de se usar o `reduce`. Neste exemplo, serão comparados valores para buscar o maior valor em um array. Tente criar essa função apenas com `for` e depois tente com `reduce`. Caso não consiga, olhe a solução abaixo:
```js
const numbers = [50, 85, -30, 3, 15];

const getBigger = (bigger, number) => ((bigger > number) ? bigger : number);

const bigger = numbers.reduce(getBigger, 0);
console.log(bigger); // 85

```

A função passada agora pode possuir dois tipos de retorno:

-   O retorno do próprio acumulador `bigger` (no caso `true` do ternário), o que significa que ele não será modificado; ou
    
-   O valor do elemento do array, `number`, que indica que possui um valor maior que `bigger`.
    

Modifique o segundo parâmetro passado, o `0`, no reduce para `100` e execute o programa. O retorno agora é `100`, já que nenhum número de dentro do array é maior que o valor inicial passado. Então veja: a cada iteração, o `reduce` mantém o valor do acumulador igual ou o atualiza de acordo com a comparação que é feita. Ao final, você tem o maior valor do array. Adicione um `console.log` à função do `reduce` para ver isso acontecendo em detalhes, se quiser!

Para fixar ainda mais o conceito de `reduce`, faça uma função que some todos os números pares do array:
```js
const numbers = [18, 19, 23, 53, 4, 5, 76, 23, 54];

```

A solução é esta a seguir, mas tente realizar a função sem vê-la. Tente criar uma solução usando `reduce` e `filter`, e outra apenas usando `reduce`.

Solução usando `filter` e `reduce`:
```js
const numbers = [18, 19, 23, 53, 4, 5, 76, 23, 54];

const getEven = (number) => number % 2 === 0;
const sumPair = (accumulator, number) => accumulator + number;

const sumNumbers = (array) => array.filter(getEven).reduce(sumPair); // Olhe que código pequeno e conciso!

console.log(sumNumbers(numbers)); // 152

```

Solução usando apenas `reduce`:
```js
const numbers = [18, 19, 23, 53, 4, 5, 76, 23, 54];

const sumPair = (accumulator, number) => (
  (number % 2 === 0) ? accumulator + number : accumulator
);

const sumNumbers = (array) => array.reduce(sumPair, 0);

console.log(sumNumbers(numbers)); // 152

```

Agora crie uma função usando os dados dos estudantes, para mostrar na tela um relatório que diz em qual matéria o estudante foi melhor. Você usará tanto o `map` quanto, dentro dele, o `reduce`!
```js
const estudantes = [
  {
    nome: 'Jorge',
    sobrenome: 'Silva',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: 67 },
      { name: 'Português', nota: 79 },
      { name: 'Química', nota: 70 },
      { name: 'Biologia', nota: 65 },
    ],
  },
  {
    nome: 'Mario',
    sobrenome: 'Ferreira',
    idade: 15,
    turno: 'Tarde',
    materias: [
      { name: 'Matemática', nota: 59 },
      { name: 'Português', nota: 80 },
      { name: 'Química', nota: 78 },
      { name: 'Biologia', nota: 92 },
    ],
  },
  {
    nome: 'Jorge',
    sobrenome: 'Santos',
    idade: 15,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: 76 },
      { name: 'Português', nota: 90 },
      { name: 'Química', nota: 70 },
      { name: 'Biologia', nota: 80 },
    ],
  },
  {
    nome: 'Maria',
    sobrenome: 'Silveira',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: 91 },
      { name: 'Português', nota: 85 },
      { name: 'Química', nota: 92 },
      { name: 'Biologia', nota: 90 },
    ],
  },
  {
    nome: 'Natalia',
    sobrenome: 'Castro',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: 70 },
      { name: 'Português', nota: 70 },
      { name: 'Química', nota: 60 },
      { name: 'Biologia', nota: 50 },
    ],
  },
  {
    nome: 'Wilson',
    sobrenome: 'Martins',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: 80 },
      { name: 'Português', nota: 82 },
      { name: 'Química', nota: 79 },
      { name: 'Biologia', nota: 75 },
    ],
  },
];
```

Resultado esperado:
```js
[
  { name: 'Jorge', materia: 'Português' },
  { name: 'Mario', materia: 'Biologia' },
  { name: 'Jorge', materia: 'Português' },
  { name: 'Maria', materia: 'Química' },
  { name: 'Natalia', materia: 'Português' },
  { name: 'Wilson', materia: 'Português' },
]

```

#### Solução:
```js
const getBestClass = (acc, materia) => {
  if (acc.nota > materia.nota) return acc;
  return materia;
};

const reportBetter = (students) => students.map((student) => ({
  name: student.nome,
  materia: student.materias.reduce(getBestClass).name,
}));

console.log(reportBetter(estudantes));
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/86b3675d-8fae-4c56-8758-d19924b4293a/lesson/5098c3a9-517b-4502-adca-8b2d41e7e146)
