[[Array]]
[[For]]
[[JavaScript]]
[[HOF's]]

O `forEach` percorre o array e executa a função passada para cada um dos seus valores. O `forEach` **não retorna nenhum valor**.

Vamos usar o `forEach`, para realizar a tabuada do 2. Veja o exemplo abaixo:

```js
const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

const multipliesFor2 = (element) => {
  console.log(`${element} * 2: ${element * 2}`);
};

numbers.forEach(multipliesFor2);
```

No exemplo acima, foi executada, para cada elemento do array, a função `multipliesFor2`, que imprime o parâmetro `element` * 2 no console.

Agora estamos tratando de uma _HOF_, sendo assim é possível utilizar também os demais parâmetros para resolver um problema. Como se pode fazer isso? Veja este exemplo abaixo com o uso de `index` no `forEach`:
```js
const names = ['Bianca', 'Camila', 'Fernando', 'Ana Roberta'];

const convertToUpperCase = (name, index) => {
  names[index] = name.toUpperCase();
};

names.forEach(convertToUpperCase);
console.log(names); // [ 'BIANCA', 'CAMILA', 'FERNANDO', 'ANA ROBERTA' ]
```



## Para fixar

-   Use o método forEach chamando a callback **showEmailList** para apresentar os emails

```js
const emailListInData = [
  'roberta@email.com',
  'paulo@email.com',
  'anaroberta@email.com',
  'fabiano@email.com',
];

const showEmailList = (email) => {
  console.log(`O email ${email} esta cadastrado em nosso banco de dados!`);
};

// Adicione seu código aqui
```


Resolução:
```js
const emailListInData = [
  'roberta@email.com',
  'paulo@email.com',
  'anaroberta@email.com',
  'fabiano@email.com',
];

const showEmailList = (email) => {
  console.log(`O email ${email} esta cadastrado em nosso banco de dados!`);
};

// Adicione seu código aqui
emailListInData.forEach(showEmailList);
```

Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/c4b18c18-c696-46c7-b80b-d810716018ee/lesson/214b9b6e-b15a-4061-864b-f106bbe40dc8)
