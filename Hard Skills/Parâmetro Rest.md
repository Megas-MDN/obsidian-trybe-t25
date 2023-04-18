[[Funções]]
[[Array]]

O parâmetro `rest` é uma `feature` do ES6 que permite que você crie funções que recebam um número variável de argumentos. Assim, suas funções ficam mais flexíveis. Os argumentos que serão passados como parâmetro são salvos em um array que pode ser acessado de dentro da função. Por isso, podemos passar _qualquer_ tipo de parâmetro quando usamos o `rest`. Todos eles serão colocados dentro de um array, o que te permite usar métodos como o `.length`. Acompanhe o exemplo abaixo para entender melhor essa ideia:

```js
function quantosParams(...args) {
  console.log('parâmetros:', args);
  return `Você passou ${args.length} parâmetros para a função.`;
}

console.log(quantosParams(0, 1, 2)); // Você passou 3 parâmetros para a função.
console.log(quantosParams('string', null, [1, 2, 3], { })); // Você passou 4 parâmetros para a função.

```

Observe no segundo `console.log` que passamos diferentes tipos de argumentos para a função `quantosParams`, e que todos foram colocados em um array. Quer ver mais um exemplo onde o `rest` é muito útil? Acompanhe!

```js
const sum = (...args) => args.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum(4, 7, 8, 9, 60)); // 88
```

No exemplo acima, a função `sum` calcula a soma de todos os argumentos passados a ela - independente do número. Como o parâmetro `rest` “empacota” todos os argumentos em um array, podemos utilizar o [[Reduce]] para somar tudo o que estiver dentro desse array. Experimente passar mais números como argumento para a função `sum`. Você verá que, independente do número de argumentos passados, a função vai executar a soma. Sua função é muito mais flexível quando queremos passar múltiplos parâmetros com o `rest`, pois você não precisa especificar quantos argumentos a função irá receber!

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/9f13f306-fdc8-4208-94a8-a1e20101cd21/lesson/232ca066-76d0-4786-82a7-1b2013d6cf9c)