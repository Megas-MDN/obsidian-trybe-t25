[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]

  
A função `sort` permite ordenar um array de acordo com algum critério estabelecido. Veja este exemplo com um array de strings:
```js
const food = ['arroz', 'feijão', 'farofa', 'chocolate', 'doce de leite'];
food.sort();
console.log(food);
// [ 'arroz', 'chocolate', 'doce de leite', 'farofa', 'feijão' ]
```

Funcionou bem com um array de strings, não é mesmo? Portanto, caso queira ordenar de forma alfabética, basta chamar `sort`, sem parâmetro algum na função. Agora, veja este exemplo com um array de números:
```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
numbers.sort();
console.log(numbers); // [1, 10, 2, 3, 4, 5, 6, 7, 8, 9]
```

😮 O que aconteceu com essa ordenação?

Como pode notar, a forma como ela organiza os elementos do array não é tão intuitiva. Isso ocorre, pois ela distribui sempre **por ordem alfabética**. No caso, quando há elementos como números, a `sort` coloca de acordo com a ordem alfabética dos códigos desse elemento na tabela de caracteres unicode!

Agora, se deseja ordenar de forma numérica crescente, é necessário passar a função a seguir:
```js
const points = [40, 100, 1, 5, 25, 10];
points.sort((a, b) => a - b);
console.log(points); // [1, 5, 10, 25, 40, 100]
```

A lógica é a seguinte: a função recebe, da `sort`, todos os elementos do array, em pares `(elemento1, elemento2)`, e vai comparando-os. O formato é `meuArray.sort((elemento1, elemento2) => /* logica da função */)`. Ou seja: para o array `[1, 2, 3, 4]`, a função receberá `(2, 1)`, `(3, 2)`, `(4, 3)` como parâmetros e ordenará o array com base em seu resultado. Se a operação de `elemento1` com `elemento2` der resultado negativo, `elemento1` vai para trás. Caso contrário, vai para frente, para, de forma decrescente, só inverter `elemento1 - elemento2` para `elemento2 - elemento1`. Novamente, o [artigo do MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) é uma excelente fonte de informação para entender melhor.

Agora se realizarmos uma simples modificação no retorno da função que ordena os números, veja o que acontece:
```js
const points = [40, 100, 1, 5, 25, 10];
points.sort((a, b) => b - a);
console.log(points); // [ 100, 40, 25, 10, 5, 1 ]
```

## Para fixar

-   Utilize o `sort` para ordenar o array pela **idade** das pessoas em ordem **crescente**.
```js
const people = [
  { name: 'Mateus', age: 18 },
  { name: 'José', age: 16 },
  { name: 'Ana', age: 23 },
  { name: 'Cláudia', age: 20 },
  { name: 'Bruna', age: 19 },
];

// Adicione se código aqui

console.log(people);
```

-   Modifique o `sort` do exercício anterior para que ordene o array pela **idade** das pessoas em ordem **decrescente**.

### **Solução:**

-   Utilize a `sort` para ordenar o array pela **idade** das pessoas em ordem crescente.
```js
const people = [
  { name: 'Mateus', age: 18 },
  { name: 'José', age: 16 },
  { name: 'Ana', age: 23 },
  { name: 'Cláudia', age: 20 },
  { name: 'Bruna', age: 19 },
];

// Adicione se código aqui
people.sort((personA, personB) => personA.age - personB.age);

console.log(people);
```

-   Modifique o `sort` do exercício anterior para que ordene o array pela **idade** das pessoas em ordem **decrescente**.

Se para colocar em ordem crescente utilizamos a subtração do primeiro parâmetro pelo segundo, para ordem decrescente subtraímos do segundo parâmetro o primeiro.

```js
const people = [
  { name: 'Mateus', age: 18 },
  { name: 'José', age: 16 },
  { name: 'Ana', age: 23 },
  { name: 'Cláudia', age: 20 },
  { name: 'Bruna', age: 19 },
];

// Adicione se código aqui
people.sort((personA, personB) => personB.age - personA.age);

console.log(people);
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/c4b18c18-c696-46c7-b80b-d810716018ee/lesson/9dd28942-5b5e-4ad4-bb7a-0d1c6813f3d8)
