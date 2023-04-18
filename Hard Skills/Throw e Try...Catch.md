[[Arrow Functions]]
[[IF...Else]]
[[JavaScript]]


Para entender melhor este conteúdo, vamos utilizar `arrow function`:
```js
const sum = (value1, value2) => value1 + value2;
```

A função acima é bastante simples: recebe dois parâmetros e retorna a soma entre eles. Copie o código e chame a função com dois parâmetros numéricos (por exemplo, 2 e 3). Não se esqueça do `console.log` para que seja possível ver o retorno.
```js
const sum = (value1, value2) => value1 + value2;

console.log(sum(2, 3));
```

Tudo funciona perfeitamente quando você tem o controle do código, certo? Mas digamos que você está desenvolvendo uma aplicação onde uma pessoa vai fornecer os valores. Sabemos que pessoas cometem erros e podem, por exemplo, tentar somar o número 2 com a string ‘3’. O que aconteceria nesse caso?
```js
const sum = (value1, value2) => value1 + value2;

console.log(sum(2, '3')); // resultado: 23
```

2 + ‘3’ = 23?? Uma interação bastante inusitada, concorda? O que aconteceu foi que a sua função, ao perceber que estava fazendo uma operação com parâmetros de tipos distintos, tentou adaptá-los para que o código não quebrasse - no caso, o primeiro parâmetro foi convertido para uma `string`, e a operação realizada foi uma concatenação de strings através do sinal de `+`.

Esse comportamento ocorre porque considera-se o JavaScript como uma linguagem [dinâmica](https://developer.mozilla.org/pt-BR/docs/Glossary/Dynamic_programming_language). Ou seja, quando se declara uma variável, não é necessário que ela seja atrelada a nenhum tipo, o que permite inclusive que ela mude de tipo ao longo da execução do código.

Por mais que esse aspecto traga alguma flexibilidade, ele também produz comportamentos inesperados, que podem ser difíceis de identificar. Por isso, você, enquanto boa pessoa programadora, deve ser capaz de prever esses comportamentos e evitar que eles ocorram. 😉

Vamos adicionar uma condicional que impede a pessoa usuária de quebrar a sua calculadora.
```js
const sum = (value1, value2) => {
  if (typeof value1 !== 'number' || typeof value2 !== 'number') {
    return 'Os valores devem ser numéricos';
  }
  return value1 + value2;
};

console.log(sum(2, '3'));
```

Pronto, agora o seu código avisa para a pessoa usuária que a função `sum` só aceita números. Aparentemente está tudo funcionando como deveria, mas essa ainda não é a melhor forma de se tratar um erro em `JavaScript`. Na prática, a função `sum` está retornando uma string, e esse não é o objetivo de uma função que soma dois números, certo? Você precisa indicar de alguma forma que ocorreu um erro.

Para isso existe o fluxo de exceção: quando um erro acontece em Javascript, devemos lançar uma exceção, que vai interromper o funcionamento do código. Essa é a função do `throw`:
```js
1const sum = (value1, value2) => {
2  if (typeof value1 !== 'number' || typeof value2 !== 'number') {
3    throw new Error('Os valores devem ser numéricos');
4  }
5  return value1 + value2;
6};
7
8console.log(sum(2, '3'));
```

Percebeu a diferença? Agora a execução da função `sum` foi interrompida, e temos uma mensagem de erro no console, bem como uma indicação da linha onde esse erro ocorre.
![[Pasted image 20221024000357.png]]
> Exemplo de erro lançado com throw.

Mas vamos detalhar por partes o que foi feito:

-   A palavra reservada `throw` serve para lançar uma exceção criada por você. No caso, definimos que não seria aceito um parâmetro que não fosse do tipo `number`, então criamos esse “erro customizado”. Caso contrário, a função `sum` apresentaria um comportamento incorreto. Se quiser saber mais detalhes, [consulte a documentação](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/throw).
    
-   O operador `new` serve para **criar** um objeto personalizado ou nativo do `JavaScript`. Mais sobre o `new` [aqui](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/new).
    
-   A palavra `Error` é um objeto nativo do `JavaScript` que representa um erro. Quando você o chama com o operador `new`, você cria uma cópia desse objeto, que será lançada como uma exceção no seu código. Veja mais sobre `Error` [na documentação oficial](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Error).
    

Você programou o código para lançar uma exceção caso aconteça um erro, mas o fluxo do código ainda pode ser melhorado. Você precisa, por exemplo, capturar esse erro para melhor tratá-lo. É aí que entra o bloco `try/catch`. Enquanto o `try` tenta executar o código com sucesso, o `catch` é chamado caso ocorra um erro.

Aproveitando a ocasião, seria uma ótima ideia refatorar a função `sum` para que ela não tenha funcionalidades demais.
```js
const verifyIsNumber = (value1, value2) => {
  if (typeof value1 !== 'number' || typeof value2 !== 'number') {
    throw new Error('Os valores devem ser numéricos');
  }
};

const sum = (value1, value2) => {
  try {
    verifyIsNumber(value1, value2);
    return value1 + value2;
  } catch (error) {
    return error.message;
  }
};

console.log(sum(2, '3'));
```

Agora sim! Você criou um fluxo para quando nosso código é executado com sucesso, representado pelo bloco `try`, que tenta fazer a soma de dois valores. Esse bloco chama a função recém-criada `verifyIsNumber`, que verifica se os parâmetros passados são números. Quando se depara com um valor que não é um número, o código lança um erro com o `throw`, que é capturado pelo `catch` no fluxo de exceção, através da variável `error` (aqui podemos usar qualquer nome). Dentro do `catch`, retornamos a chave `error.message`, uma propriedade do objeto nativo `Error` que contém a mensagem de erro criada anteriormente.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/131a8311-a3d9-4404-ae50-2ea6c971f5d8/day/bf2a9b74-bf09-450e-ada4-e3a87d20eb72/lesson/c798fae2-0072-411f-9cc9-16351893142b)
