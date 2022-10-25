[[Array]]
[[HOF's]]
[[For]]
[[JavaScript]]

A função `find` é utilizada para achar o primeiro elemento que satisfaça a condição passada. Então a função que deverá ser passada precisa retornar true ou false.

A animação abaixo nos mostra como o `find` pode ser utilizado para encontrar o primeiro item do array `listaNumeros` maior do que vinte. Essa condição (item > 20) é implementada na função (callback), que será executada para cada elemento de `listaNumeros`. Quando o primeiro item do array `listaNumeros` for maior que vinte, a função (callback) retornará `true` e o `find` vai retornar este elemento que satisfaz a condição passada. Observe que o retorno do método `find` é um único elemento: o primeiro item de `listaNumeros` maior do que 20.

![[GIF ilustrando o método find.gif]]
> GIF ilustrando o método .find()

Olhe o exemplo abaixo:
```js
const numbers = [19, 21, 30, 3, 45, 22, 15];

const verifyEven = (number) => number % 2 === 0;

const isEven = numbers.find(verifyEven);

console.log(isEven); // 30

console.log(verifyEven(9)); // False
console.log(verifyEven(14)); // True

// Outra forma de ser realizada sem a necessidade de criar uma nova função.
const isEven2 = numbers.find((number) => number % 2 === 0);

console.log(isEven2); // 30
```

Esse exemplo mostra duas formas de resolver o mesmo problema, que é retornar o primeiro número par do array.

Primeiro observe a função `verifyEven`. Ela verifica se o número recebido é par. Se sim, seu retorno será true; caso contrário, seu retorno é false.

Quando a passamos como _`callback`_, o find executará a função para cada um dos elementos do array e retornará o primeiro elemento quando o retorno da função for `true`.

## Para fixar

-   Utilize o `find` para retornar o primeiro número do array que é divisível por **3** e **5**, caso ele exista:

```js
const numbers = [19, 21, 30, 3, 45, 22, 15];

const findDivisibleBy3And5 = () => {
  // Adiciona seu código aqui
};

console.log(findDivisibleBy3And5());
```

-   Utilize o `find` para encontrar o primeiro nome com cinco letras, caso ele exista:

```js
const names = ['João', 'Irene', 'Fernando', 'Maria'];

const findNameWithFiveLetters = () => {
  // Adicione seu código aqui:
};

console.log(findNameWithFiveLetters());
```

-   Utilize o `find` para encontrar a música com **id** igual a **31031685**, caso ela exista:


```js
const musicas = [
  { id: '31031685', title: 'Partita in C moll BWV 997' },
  { id: '31031686', title: 'Toccata and Fugue, BWV 565' },
  { id: '31031687', title: 'Chaconne, Partita No. 2 BWV 1004' },
];

function findMusic(id) {
  // Adicione seu código aqui
};

console.log(findMusic('31031685'));
```

#### **Solução:**

Utilizamos o método `find`sobre o array names e verificamos a cada iteração se o nome tem cinco caracteres. Isso retornará `Irene`, que é o primeiro caso de sucesso.

```js
const names = ['João', 'Irene', 'Fernando', 'Maria'];
const findNameWithFiveLetters = () => {
  // Adicione seu código aqui:
  return names.find((name) => name.length === 5);
};
console.log(findNameWithFiveLetters());
```

-   Utilize o `find` para encontrar a música com **id** igual a **31031685**, caso ela exista:

```js
const musicas = [
  { id: '31031685', title: 'Partita in C moll BWV 997' },
  { id: '31031686', title: 'Toccata and Fugue, BWV 565' },
  { id: '31031687', title: 'Chaconne, Partita No. 2 BWV 1004' },
];

function findMusic(id) {
  // Adicione seu código aqui
};

console.log(findMusic('31031685'));
```

Utilizamos o método find e verificamos a cada iteração se a chave `id` da musica corresponde com o id que passamos como parâmetro. Esse método voltará a resposta correta, já que quando trabalhamos com `ids`, estamos trabalhando com chaves únicas.


```js
const musicas = [
  { id: '31031685', title: 'Partita in C moll BWV 997' },
  { id: '31031686', title: 'Toccata and Fugue, BWV 565' },
  { id: '31031687', title: 'Chaconne, Partita No. 2 BWV 1004' },
];

function findMusic(id) {
  // Adicione seu código aqui
  return musicas.find((musica) => musica.id === id);
}

console.log(findMusic('31031685'));
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/c4b18c18-c696-46c7-b80b-d810716018ee/lesson/15b2021d-0a04-4dc5-88ac-cf7e2a2c08dd)
