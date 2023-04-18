[[Funções]]
[[JavaScript]]


Vamos entender o que é o parâmetro `default`. Imagine que você queira executar a função `greeting` abaixo, que imprime uma saudação para a pessoa usuária. O que acontece quando você chama a função sem passar o argumento que ela espera? Faça esse teste com o exemplo no seu editor de códigos!
```js
const greeting = (user) => console.log(`Welcome ${user}!`);

greeting(); // Welcome undefined!

```

Você verá que a função retornará `undefined`. Você consegue pensar em uma forma de corrigir esse problema? Afinal, podemos esquecer de chamar a função com o nome da pessoa usuária. Uma solução seria:
```js
const greeting = (user) => {
  const userDisplay = typeof user === 'undefined' ? 'pessoa usuária' : user;
  console.log(`Welcome ${userDisplay}!`);
};

greeting(); // Welcome pessoa usuária!
```

Essa solução não parece muito elegante, não é mesmo? Afinal, precisamos incluir uma linha para checar se o parâmetro é indefinido. Se sim, definimos que `user` será `'pessoa usuária'`. Caso contrário, a função irá imprimir a mensagem com o nome da pessoa usuária passado como argumento.

Com o ES6, podemos pré-definir um parâmetro padrão para a função. Assim, podemos reescrever o exemplo anterior da seguinte forma:
```js
const greeting = (user = 'pessoa usuária') => console.log(`Welcome ${user}!`);
greeting(); // // Welcome pessoa usuária!

```

Simples assim! Passar um parâmetro como `default` é um pequeno detalhe que torna o seu código muito mais semântico. Assim, o `default` será utilizado caso nenhum argumento seja fornecido à função. Você pode adicionar mais de um parâmetro `default` caso a sua função receba vários argumentos, se achar necessário.

## Para Fixar

Para praticar, escreva uma função `multiply` que multiplique dois números passados como argumentos. Atribua como `default` o valor 1, caso não seja passado nenhum valor como segundo parâmetro.
```js
const multiply = (number, value) => {
  // Escreva aqui a sua função
};

console.log(multiply(8));
```

#### **Solução**
```js
1// Caso não seja passado um valor para value ele agora assumirá o valor padrão de 1.
2const multiply = (number, value = 1) => number * value;
3
4console.log(multiply(8));
```

Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/9f13f306-fdc8-4208-94a8-a1e20101cd21/lesson/61313cfb-67f2-49ec-a021-c917fedb2abc)
