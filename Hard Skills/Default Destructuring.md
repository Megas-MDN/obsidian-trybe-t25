[[Objeto]]
[[Array]]


Agora você já sabe como aplicar desestruturação em objetos e arrays. Você se lembra do que acontece quando tentamos acessar:
-   uma propriedade que não existe em um objeto?
-   um valor em uma posição inexistente em um array?

Ou seja:

```js
const person = {
  name: 'João',
  lastName: 'Jr',
  age: 34,
};

const { nationality } = person;
```

Essa desestruturação funciona? E se funciona, qual o valor que aparece se fizer `console.log(nationality)`? Copie esse código e teste você mesmo. 😉

Quando tentamos acessar uma propriedade que não existe, o valor retornado é `undefined`. E se você quisesse dar um valor padrão para alguma chave, caso essa propriedade não exista no objeto? Você consegue atribuir esse valor padrão utilizando `default destructuring`, que é mais um recurso do ES6:
```js
const person = {
  name: 'João',
  lastName: 'Jr',
  age: 34,
};

const { nationality = 'Brazilian' } = person;
console.log(nationality); // Brazilian

```

Analogamente, o mesmo pode ser feito na hora de desestruturar um array:
```js
const position2d = [1.0, 2.0];
const [x, y, z = 0] = position2d;

console.log(x); // 1
console.log(y); // 2
console.log(z); // 0

```

## Para Fixar

Do jeito que está, quando `person` é passado para a função `getNationality` o retorno é `João is undefined`. Ajuste a função `getNationality` para que a chamada `getNationality(person)` retorne `João is Brazilian`.
```js
const getNationality = ({ firstName, nationality }) => `${firstName} is ${nationality}`;

const person = {
  firstName: 'João',
  lastName: 'Jr II',
};

const otherPerson = {
  firstName: 'Ivan',
  lastName: 'Ivanovich',
  nationality: 'Russian',
};

console.log(getNationality(otherPerson)); // Ivan is Russian
console.log(getNationality(person));
```

#### **Solução**
```js
// Passando um valor default para a desestruturação de `nationality` sendo "Brazilian" então todo objeto que passarmos terá esse valor, caso não seja passado algum outro.
const getNationality = ({ firstName, nationality = 'Brazilian' }) => `${firstName} is ${nationality}`;

const person = {
  firstName: 'João',
  lastName: 'Jr II',
};

const otherPerson = {
  firstName: 'Ivan',
  lastName: 'Ivanovich',
  nationality: 'Russian',
};

console.log(getNationality(otherPerson)); // Ivan is Russian
console.log(getNationality(person)); // João is Brazilian
```

Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/9f13f306-fdc8-4208-94a8-a1e20101cd21/lesson/6bf6a9bc-d4e2-4e3a-b149-9716ac4fd139)
