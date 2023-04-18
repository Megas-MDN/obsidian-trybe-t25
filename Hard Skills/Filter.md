[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]

O `filter` retornará outro array com todos os elementos que satisfaçam à condição verificada pela função. A animação abaixo nos mostra como o `filter` pode ser utilizado para filtrar os valores maiores que vinte do array `listaNumeros`. Observe que o retorno da função é um novo array (`maiorVinte`) contendo os números que passaram pelo filtro.
![[Filter.gif]]
> GIF método filter

Veja o exemplo abaixo.
```js
const numbers = [19, 21, 30, 3, 45, 22, 15];

const verifyEven = (number) => number % 2 === 0;

const isEven = numbers.filter(verifyEven);

console.log(isEven); // [ 30, 22 ]

// Outra forma de ser realizada sem a necessidade de criar uma nova função.
const isEven2 = numbers.filter((number) => number % 2 === 0);

console.log(isEven2); // [ 30, 22 ]
```

Verifique que o retorno é um novo array com os dois números pares vindos do array `numbers`.

Observe este outro exemplo que busca os elementos através da condição do `filter`. Neste caso, como resultado teremos pessoas que possuem idade menor que 18 anos, ou seja, que ainda não podem dirigir:
```js
const objPeople = [
  { name: 'José', age: 21 },
  { name: 'Lucas', age: 19 },
  { name: 'Maria', age: 16 },
  { name: 'Gilberto', age: 18 },
  { name: 'Vitor', age: 15 },
];

const verifyAgeDrive = (arrayOfPeople) => (
  arrayOfPeople.filter((people) => (people.age < 18))
);

console.log(verifyAgeDrive(objPeople));
// [ { name: 'Maria', age: 16 }, { name: 'Vitor', age: 15 } ]
```

Outra forma de se usar o `filter` é retornar um array sem o elemento desejado. É preciso remover o `Ricardo` do objeto agora, já que ele não é mais um estudante.
```js
const arrayMyStudents = ['Maria', 'Manuela', 'Jorge', 'Ricardo', 'Wilson'];

const removeStudentByName = (name, listStudents) =>
  listStudents.filter((student) => student !== name);
  // Filtra todos os estudantes que não têm o nome 'Ricardo' e retorna um array com eles. Na prática, remove o Ricardo do array.

const newListStudents = removeStudentByName('Ricardo', arrayMyStudents);
console.log(newListStudents); // [ 'Maria', 'Manuela', 'Jorge', 'Wilson' ]
```

Observe que o `filter` foi usado dentro de uma função que recebe dois parâmetros, o array de valores e uma string, o que será removido. A condição de dentro do `filter` é para retornar sempre que o elemento for diferente do `name` passado. Se tiver ficado confuso, rode esse código por conta própria e altere um pouco o seu funcionamento! Isso ajudará muito.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/d353b4e6-3ea2-44e7-880b-13b38bdf307e/lesson/662475f2-ca1a-4a6a-8ed4-78853f08109b)
