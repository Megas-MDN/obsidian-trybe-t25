[[Objeto]]
[[JavaScript]]
[[React]]

Você certamente já precisou extrair valores de um objeto em Javascript. No exemplo abaixo, como você faria para imprimir o valor de cada propriedade do objeto `product`?


```js
const product = {
  name: 'Smart TV Crystal UHD',
  price: '1899.05',
  seller: 'Casas de Minas',
};

```

Uma forma seria acessar os valores utilizando a notação de objeto, como `console.log(product.name)`, e repetir para cada propriedade. Essa tarefa é repetitiva e verbosa… quando lidamos com objetos mais complexos, ela seria até mesmo impraticável. Para a nossa alegria, o ES6 introduz mais um recurso para tornar atividades corriqueiras, como acessar os valores de um objeto, mais simples e com menos declarações. Essa `feature` é o que chamamos de desestruturação de objeto, ou `object destructuring`.

E como exatamente funciona a desestruturação de objeto? Vamos voltar ao exemplo do objeto `product`. A sintaxe da desestruturação de objetos pede para passarmos o nome das propriedades que queremos acessar do lado esquerdo, entre chaves, e o objeto do lado direito:
```js
const { name } = product;
console.log(name); // Smart TV Crystal UHD

```

Se quisermos pegar, além do nome, o vendedor do produto, podemos incluir a propriedade `seller` dentro das chaves para acessar o seu valor correspondente:
```js
const { name, seller } = product;
console.log(name); // Smart TV Crystal UHD
console.log(seller); // Casas de Minas

```

Dessa forma, conseguimos extrair o valor da propriedade que precisamos acessar com muito menos código, atribuindo esse valor à variáveis. Vale lembrar também que podemos adicionar quantas propriedades forem necessárias dentro das chaves, basta seguirmos a sintaxe da desestruturação de objetos.

Você deve estar se perguntando: “E se a chave do objeto contiver outro objeto como valor?” Veja o exemplo abaixo e entenda como podemos resolver esse problema:

```js
// definindo o objeto
const character = {
  name: 'Luke SkyWalker',
  age: '53',
  description: {
    specieName: 'Human',
    jedi: true,
  },
  homeWorld: {
    name: 'Tatooine',
    population: '200000',
  },
};
```

Queremos extrair o nome do personagem, a idade, o nome do planeta e verificar se ele é um Jedi. Depois de feito, precisamos imprimir essas informações no `console.log()`. Para isso, vamos utilizar a desestruturação de objetos:

```js
// definindo o objeto
const character = {
  name: 'Luke SkyWalker',
  age: '53',
  description: {
    specieName: 'Human',
    jedi: true,
  },
  homeWorld: {
    name: 'Tatooine',
    population: '200000',
  },
};

// desestruturando o objeto:
const { name, age, homeWorld: { name: planetName }, description: { jedi } } = character;

// imprimindo os valores:
console.log(`Esse é o ${name}, ele tem ${age} anos, mora no planeta ${planetName} e, por incrível que possa parecer, ele ${jedi ? 'é um Jedi' : 'não é um Jedi'}.`);
```

Como foi mostrado, para desconstruir uma chave que contém um objeto como valor, precisamos utilizar o nome da chave seguido por `:`. Segue a sintaxe: `homeWorld: { name: planetName }`. Agora `planetName` é uma variável que recebe o valor da propriedade `name` do objeto `homeWorld`.

Podemos também usar a desestruturação de objetos em conjunto com o [[Spread Operator]], veja abaixo:
```js

const daysOfWeek = {
  workDays: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'],
  weekend: ['Saturday', 'Sunday'],
};

```

Temos um objeto `daysOfWeek` que contém as chaves `workDays` e `weekend`. Precisamos agora extrair os valores dessas chaves e, para isso, vamos utilizar a desestruturação de objetos:
```js

const daysOfWeek = {
  workDays: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'],
  weekend: ['Saturday', 'Sunday'],
};

const { workDays, weekend } = daysOfWeek;
console.log(workDays); // ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
console.log(weekend); // ['Saturday', 'Sunday']

```

Feita a desestruturação, podemos utilizar o `spread operator` para juntar os valores do array `workDays` com os do array `weekend`, colocando-os em um novo array chamado `weekdays`.
```js

const daysOfWeek = {
  workDays: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'],
  weekend: ['Saturday', 'Sunday'],
};

const { workDays, weekend } = daysOfWeek;
console.log(workDays); // ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
console.log(weekend); // ['Saturday', 'Sunday']

const weekdays = [...workDays, ...weekend];
console.log(weekdays); // ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']

```

Copie o código acima e teste em seu VSCode.

Outro truque legal dessa `feature` é que você pode reatribuir o nome da propriedade que deseja acessar ao declará-la como uma variável. Acompanhe o exemplo abaixo:
```js
const student = {
  a: 'Maria',
  b: 'Turma B',
  c: 'Matematica',
};

```

As propriedades do objeto `student` não são nada descritivas, não é mesmo? Se fôssemos desestruturar esse objeto, as variáveis que seriam criadas ao extrair as propriedades de `students` teriam nomes sem significado… pensando nisso, podemos trocar o nome da variável ao fazermos a desestruturação:
```js
const student = {
  a: 'Maria',
  b: 'Turma B',
  c: 'Matematica',
};

const { a: name, b: classAssigned, c: subject } = student;

console.log(name); // Maria
console.log(classAssigned); // Turma B
console.log(subject); // Matemática

```

Nesse exemplo, informamos qual a propriedade que gostaríamos de acessar e a declaramos em uma nova variável seguindo a sintaxe: `{ propriedade:nomeVariável } = objeto`. Essa forma de acessar um valor de um objeto e atribuí-lo a uma variável é equivalente ao que temos abaixo:
```js
const student = {
  a: 'Maria',
  b: 'Turma B',
  c: 'Matematica',
};
const name = student.a;
console.log(name); // Maria

```

Você deve estar se perguntando: o que acontece quando tento acessar um campo inexistente? Experimente fazer esse teste! Como sabemos, o Javascript não vai conseguir fazer essa associação porque esse campo não existe, e a variável receberá o valor `undefined`.

Por fim, uma outra situação em que podemos usar a desestruturação de objetos é quando queremos passar os valores de um objeto como parâmetros para uma função, como no exemplo abaixo:
```js
const product = {
  name: 'Smart TV Crystal UHD',
  price: '1899.05',
  seller: 'Casas de Minas',
};

const printProductDetails = ({ name, price, seller }) => {
  console.log(`Promoção! ${name} por apenas ${price} é só aqui: ${seller}`);
};

printProductDetails(product); // Promoção! Smart TV Crystal UHD por apenas 1899.05 é só aqui: Casas de Minas

```


## Para Fixar

-   Crie um terceiro objeto, que terá os dados pessoais e os dados de cargo juntos.

Existem dois objetos referentes a uma pessoa usuária, um com informações pessoais e outro com informações referentes ao seu cargo na empresa **trappistEnterprise**. Você precisa criar um terceiro objeto, que terá os dados pessoais e os dados de cargo juntos. Para isso, utilize o `spread operator`.

```js

const user = {
  name: 'Maria',
  age: 21,
  nationality: 'Brazilian',
};

const jobInfos = {
  profession: 'Software engineer',
  squad: 'Rocket Landing Logic',
  squadInitials: 'RLL',
};

```

-   Imprima no console uma frase utilizando os dados do objeto criado anteriormente. Para isso, utilize a desestruturação de objetos em conjunto com `template literals`.

Exemplo `"Hi, my name is Maria, I'm 21 years old and I'm Brazilian. I work as a Software engineer and my squad is RLL-Rocket Landing Logic"`

#### **Solução:**

-   Crie um terceiro objeto, que terá os dados pessoais e os dados de cargo juntos.

```js
const user = {
  name: 'Maria',
  age: 21,
  nationality: 'Brazilian',
};

const jobInfos = {
  profession: 'Software engineer',
  squad: 'Rocket Landing Logic',
  squadInitials: 'RLL',
};

const userInfos = {
  ...user,
  ...jobInfos,
};
```

-   Imprima no console uma frase utilizando os dados do objeto criado anteriormente. Para isso, utilize a desestruturação de objetos em conjunto com [[Template Literals]].
```js
const user = {
  name: 'Maria',
  age: 21,
  nationality: 'Brazilian',
};

const jobInfos = {
  profession: 'Software engineer',
  squad: 'Rocket Landing Logic',
  squadInitials: 'RLL',
};

const userInfos = {
  ...user,
  ...jobInfos,
};

// Aqui podemos desestruturar as chaves do objeto `userInfo` e então criar nossa mensagem diretamente pelas chaves desestruturadas.
const { name, age, nationality, profession, squad, squadInitials } = userInfos;

console.log(`Hi, my name is ${name}, I'm ${age} years old and I'm ${nationality}. I work as a ${profession} and my squad is ${squadInitials}-${squad}`);
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/9f13f306-fdc8-4208-94a8-a1e20101cd21/lesson/7f84996a-8de0-4e20-995b-7a5d69a24158)
