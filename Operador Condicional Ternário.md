[[JavaScript]]
[[React]]
[[IF...Else]]
[[DOM]]
[[ReactDOM]]
[[Switch...Case]]

Além dos condicionais `if`/`else` e `switch`/`case`, o JavaScript ES6 trouxe consigo uma ferramenta que permite fazer operações condicionais mais simples, que só tenham duas possibilidades de resposta (**x** se _verdadeiro_, **y** se _falso_), com uma sintaxe simplificada e legível: o **operador ternário**. Ele funciona muito bem com as outras sintaxes simplificadas, como as `arrow functions`, por exemplo! Para entendê-lo melhor, observe a seguinte lógica:
```jsx
// A sintaxe básica do operador ternário é muito simples:
`expressão verdadeira ou falsa` ? `retorno se verdadeira` : `retorno se falsa`;

// Assim, por exemplo, podemos ter expressões com a seguinte estrutura:
const trueExpression = (1 + 1 === 2) ? `isso é verdade` : `isso é mentira`;
console.log(trueExpression); // isso é verdade

const falseExpression = (2 + 2 === 3) ? `isso é verdade` : `isso é mentira`;
console.log(falseExpression); // isso é mentira
```

Como você pode ver, a sintaxe do operador ternário é bem simples: `x ? y : z`.

-   O `x` é uma condição que será avaliada como verdadeira ou falsa;
-   O `y` é o retorno se a condição for verdadeira;
-   O `z` é o retorno se a condição for falsa.

A vantagem do operador ternário é que ele é fácil de entender quando se pega o jeito e é muito mais sucinto do que escrever um bloco condicional com `if/else` ou switch, gerando um código mais limpo e simples.

Por outro lado, é bom saber que o operador ternário **_não substitui_** as expressões condicionais tradicionais! Em qualquer situação onde exista mais de uma condição a ser avaliada, gerando três ou mais resultados possíveis, o mais simples será utilizar as opções já aprendidas anteriormente:
```jsx
// Situação em que é mais simples usar o operador ternário:
const checkIfElse = (age) => {
  if (age >= 18) {
    return `Você tem idade para dirigir!`;
  } else {
    return `Você ainda não tem idade para dirigir...`;
  }
};

const checkTernary = (age) => (
  age >= 18 ? `Você tem idade para dirigir!` : `Você ainda não tem idade para dirigir...`;
);

// ------------------------

// Situação em que usar o operador ternário não faz muito sentido:
const checkIfElse = (fruit) => {
  if (fruit === `maçã`) {
    return `Essa fruta é vermelha`;
  } else if (fruit === `banana`) {
    return `Esta fruta é amarela`;
  } else {
    return `Não sei a cor`;
  }
};

const checkTernary = (fruit === `maçã`) ? `Essa fruta é vermelha` 
  : ((fruit === `banana`) ? `Esta fruta é amarela` : `Não sei a cor`);

// Aninhar operadores  ternários, como no exemplo acima, não é uma boa prática,
// pois torna o seu código truncado e difícil de ler, tirando todo o sentido de um
// operador cujo objetivo é facilitar a sua vida e a da pessoa que lerá seu código
// no futuro!
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/131a8311-a3d9-4404-ae50-2ea6c971f5d8/day/3ff84b4e-d7c4-4e82-8e0d-ceb79321b834/lesson/7e0a973a-24a5-46c5-8e62-abf0e87aba05)