[[HOF's]]
[[Funções]]
[[This]]
[[--Parametros]]



As `arrow functions` nada mais são do que uma forma diferente de declarar funções escrevendo menos código. Veja abaixo como ficaria a função `printName` utilizando a sintaxe da `arrow function`:
```js
const printName = () => {
  const myName = 'Lucas';
  return myName;
};

console.log(printName());
```

Quando não há nada no corpo da função além do que será retornado, a sintaxe da `arrow function` nos permite simplificar ainda mais a função `printName` omitindo o `return` e as chaves:
```js
const printName = () => 'Lucas';
console.log(printName());
```

Mas lembre-se de que podemos omitir os parênteses apenas em um cenário:

-   Quando a função recebe apenas um argumento, como podemos ver no exemplo abaixo:
```js
const multiplyByTwo = number => number * 2;
console.log(multiplyByTwo(10));
```

Em funções que recebem mais de um parâmetro, os parênteses não são omitidos:
```js
const multiplication = (number, multi) => number * multi;
console.log(multiplication(8, 2));
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/131a8311-a3d9-4404-ae50-2ea6c971f5d8/day/3ff84b4e-d7c4-4e82-8e0d-ceb79321b834/lesson/9c61d961-587b-4a57-ae18-39e40652da17)


