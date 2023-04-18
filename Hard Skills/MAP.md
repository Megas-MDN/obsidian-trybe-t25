[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]

O método `map` executa a função recebida por parâmetro para cada elemento de um array e retorna o resultado em um novo array, sem modificar o original.

Veja a diferença entre fazer uma mesma função usando `for` e em seguida usando `map`:
```js
const persons = [
  { firstName: 'Maria', lastName: 'Ferreira' },
  { firstName: 'João', lastName: 'Silva' },
  { firstName: 'Antonio', lastName: 'Cabral' },
];

const fullNames = [];

for (let index = 0; index < persons.length; index += 1) {
  fullNames.push(`${persons[index].firstName} ${persons[index].lastName}`);
}

console.log(fullNames);

```

Agora com a função `map`:
```js
const persons = [
  { firstName: 'Maria', lastName: 'Ferreira' },
  { firstName: 'João', lastName: 'Silva' },
  { firstName: 'Antonio', lastName: 'Cabral' },
];

const fullNames = persons.map((person) => `${person.firstName} ${person.lastName}`);

console.log(fullNames); // [ 'Maria Ferreira', 'João Silva', 'Antonio Cabral' ]
0
```

O `for` foi substituído por apenas uma linha de código.

A função juntou o primeiro nome com o sobrenome de cada pessoa e retornou um array novo com cada um dos valores. Observe que o tamanho dos arrays `persons` e `fullNames` é o mesmo (3 elementos).

Outro exemplo é o de realizar um cálculo utilizando os valores dos elementos e retornar um array novo sem alterar o anterior.

Na animação abaixo, podemos observar que o método `map` está invocando uma função callback que multiplica cada elemento do array `listaNumeros` por dois. O retorno do `map` é um novo array (`dobro`) que contém o resultado da multiplicação de cada elemento do array `listaNumeros` por dois. Perceba que o array retornado tem exatamente a mesma quantidade de itens que o array original, que não sofreu nenhuma modificação!

![[MAP.gif]]
>GIF método map

Vamos praticar um outro exemplo numérico, para fixar bem o que o `map` faz. Suponha que é preciso transformar todos os números em negativos e passá-los para um array novo.

```js
const numbers = [1, 2, 3, 4, -5];

const negativeNumbers = numbers.map((number) => ((number > 0) ? number * (-1) : number));

console.log(negativeNumbers); // [ -1, -2, -3, -4, -5 ]
console.log(numbers); // [ 1, 2, 3, 4, -5 ]

```

E como seria apenas com `for`?
```js
const numbers = [1, 2, 3, 4, -5];

const negativeNumbers = [];
for (let index = 0; index < numbers.length; index += 1) {
  if (numbers[index] > 0) {
    negativeNumbers.push(numbers[index] * -1);
  } else {
    negativeNumbers.push(numbers[index]);
  }
}

console.log(negativeNumbers); // [ -1, -2, -3, -4, -5 ]
console.log(numbers); // [ 1, 2, 3, 4, -5 ]

```

Outras formas de usar o `.map` é unir dois arrays para criar um novo. Considere que você possui duas listas: o preço do primeiro produto (`Arroz`) é o primeiro elemento da lista `prices` (`2.99`), e assim por diante:
```js
const products = ['Arroz', 'Feijão', 'Alface', 'Tomate'];
const prices = [2.99, 3.99, 1.5, 2];

```

Deseja-se juntá-las em apenas uma lista de objetos que fique dessa forma:
```js
const listProducts = [{ Arroz: 2.99 },...]

```

Tente criar uma função que resolva esse problema. Funções passadas para as _HOFs_ podem receber vários parâmetros, não só o `elemento` sobre o qual ela está sendo iterada! Use isso em seu favor. Caso tenha dúvidas, olhe a solução logo abaixo.
```js
const products = ['Arroz', 'Feijao', 'Alface', 'Tomate'];

const prices = [2.99, 3.99, 1.5, 2];

const updateProducts = (listProducts, listPrices) => listProducts.map((product, index) => (
  { [product]: listPrices[index] }
));

const listProducts = updateProducts(products, prices);
console.log(listProducts);
// => [
//   { Arroz: 2.99 },
//   { Feijao: 3.99 },
//   { Alface: 1.5 },
//   { Tomate: 2 },
// ]

```

Qual a diferença, afinal, de `map` para `forEach`? São duas principais:

-   A função `map` aplica sobre os elementos de um array uma função e retorna um array novo, sem modificar o original;
    
-   A função `forEach` não tem tal restrição. Ela pode modificar o array original e retornar nada por padrão - ela pode criar um array novo a partir de um antigo, pode simplesmente buscar por um elemento e retorná-lo, pode não retornar nada, enfim! Ela é _genérica_ e pode fazer diversas coisas.
    

Em caso de dúvidas, pense neste exemplo:
```js
const numeros = [1, 2, 3, 4, 5, 6];
console.log(numeros.map((numero) => numero * 2)); // Retorno: [2, 4, 6, 8, 10, 12]

const paresMenoresQueCinco = [];
numeros.forEach((numero) => {
  if (numero < 5 && numero % 2 === 0) {
    paresMenoresQueCinco.push(numero);
  }
});
console.log(paresMenoresQueCinco); // Retorno: [2, 4]

```

Pense sempre que o `forEach` faz com arrays o que as outras _HOFs_ não conseguem fazer. Ele é genérico!

Vamos ver como é possível usar as outras _HOFs_ junto com o `map`. Para os exemplos a seguir, será usado um array com os dados de estudantes de um colégio.

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
      { name: 'Matemática', nota: '59' },
      { name: 'Português', nota: '80' },
      { name: 'Química', nota: '78' },
      { name: 'Biologia', nota: '92' },
    ],
  },
  {
    nome: 'Jorge',
    sobrenome: 'Santos',
    idade: 15,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: '76' },
      { name: 'Português', nota: '90' },
      { name: 'Química', nota: '70' },
      { name: 'Biologia', nota: '80' },
    ],
  },
  {
    nome: 'Maria',
    sobrenome: 'Silveira',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: '91' },
      { name: 'Português', nota: '85' },
      { name: 'Química', nota: '92' },
      { name: 'Biologia', nota: '90' },
    ],
  },
  {
    nome: 'Natalia',
    sobrenome: 'Castro',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: '70' },
      { name: 'Português', nota: '70' },
      { name: 'Química', nota: '60' },
      { name: 'Biologia', nota: '50' },
    ],
  },
  {
    nome: 'Wilson',
    sobrenome: 'Martins',
    idade: 14,
    turno: 'Manhã',
    materias: [
      { name: 'Matemática', nota: '80' },
      { name: 'Português', nota: '82' },
      { name: 'Química', nota: '79' },
      { name: 'Biologia', nota: '75' },
    ],
  },
];
```

Abaixo temos alguns exemplos de funções apenas usando `for` e, em seguida, como **refatorá-las** para quem usem _HOFs_.

-   Função para buscar e imprimir o nome completo de todos os estudantes que estudam no turno da manhã.
```js
const allNameStudents = [];

for (let index = 0; index < estudantes.length; index += 1 ) {
  if(estudantes[index].turno === 'Manhã') {
    allNameStudents.push(`${estudantes[index].nome} ${estudantes[index].sobrenome}`)
  }
}

console.log(allNameStudents);
```

-   Com `map` e [[Filter]].
```js
const allNameStudents = estudantes.filter((estudante) => (
  estudante.turno === 'Manhã')).map((estudante) => `${estudante.nome} ${estudante.sobrenome}`);

console.log(allNameStudents);

```

O que foi feito? Primeiro usou-se o `filter` para filtrar todas as pessoas que estudam no período da manhã. Como o retorno do `filter` é um array de elementos, você pode usar o `map` logo em seguida para retornar os nomes completos de estudantes presentes nesse novo array. O `map` nesse caso é usado apenas para retornar as informações pedidas, o nome completo, enquanto o `filter` é usado para filtrar o array.

Vamos ver como é possível usar um [[find]] junto com o `map`. Para os exemplos a seguir será usado um array com os dados de estudantes de um colégio.

-   Buscar um estudante pelo nome e retornar a situação dele em cada matéria:
-   Apenas com `for`:

```js
const findStudent = (name, students) => {
  for (let index = 0; index < students.length; index += 1) {
    if (students[index].nome === name) {
      return students[index];
    }
  }
};

const reportStatus = (name, students) => {
  const getStudent = findStudent(name, students);
  const report = [];
  for (let index = 0; index < getStudent.materias.length; index += 1) {
    if (getStudent.materias[index].nota >= 60) {
      report.push(`${getStudent.materias[index].name} Aprovado`);
    } else {
      report.push(`${getStudent.materias[index].name} Reprovado`);
    }
  }
  return report;
};

console.log(reportStatus('Natalia', estudantes));

```

Com [[find]] e `map`:

```js
const reportStatus = (name, students) => {
  const studentInfo = students.find((student) => student.nome === name);
  return studentInfo.materias.map((materia) => (
    `${materia.name} ${(materia.nota >= 60) ? 'Aprovado' : 'Reprovado'}`
  ));
};

console.log(reportStatus('Natalia', estudantes));

```

O código teve uma redução drástica no número de linhas! Primeiro, fizemos um `find` para buscar e retornar os dados do estudante. O objeto foi retornado e salvo na variável `studentsInfo`, depois o `map` foi usado para percorrer as `matérias` do objeto retornado e salvar o que se queria em um array da forma desejada.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/d353b4e6-3ea2-44e7-880b-13b38bdf307e/lesson/d661b9f9-cdf3-47db-a226-70aabbdb67bf)
