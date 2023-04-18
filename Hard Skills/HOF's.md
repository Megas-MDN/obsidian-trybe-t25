[[For]]
[[forEach]]
[[find]]
[[some]]
[[every]]
[[sort]]
[[MAP]]
[[Filter]]
[[Reduce]]
[[Spread Operator]]
[[Parametro Rest]]
[[Default Destructuring]]


![[Pasted image 20221024091044.png]]
> HOFs com bichos

As _Higher Order Functions_ ou **HOFs** são funções que usam outras funções em suas operações, devendo aceitá-las como parâmetro e/ou retorná-las. Veja este exemplo:
```jsx
const button = document.querySelector('#signup-button');

const registerUser = () => {
  console.log('Registrado com sucesso!');
};

button.addEventListener('click', registerUser);
```

Construímos uma função que simula o registro de uma nova pessoa e passamos como argumento de uma segunda função. Logo, `addEventListener` é uma HOF.

**Lembre-se:** First-Class Functions é o nome do conceito que define a forma que a linguagem (no nosso caso JavaScript) trata suas funções, permitindo que sejam suportadas em operações que são usadas em outros tipos (atribuição, retorno, parâmetro), e HOF é uma função que atende ao critério de receber como parâmetro e/ou retornar outra função.

Agora que você viu o que são funções de primeira classe e sua aplicação em parâmetros, partiu saber como estruturar suas _HOFs_?

## Estruturando uma HOF

Vamos construir este conceito passo a passo para que você possa compreender e aplicar na sua jornada como pessoa desenvolvedora. Para isto, é extremamente importante ter em mente que as _HOFs_ nos permitem compactar ações e não somente repassar valores. Veja este exemplo:
```jsx
const repeat = (number, action) => {
  for (let count = 0; count <= number; count += 1) {
    action(count);
  }
};

repeat(5, console.log);
```

Construímos essa função para implementar um laço de repetição entre 0 e um número especificado via parâmetro (`number`) e para mostrar no console o valor da variável _count_ de 0 a N (`number`).

Vamos aumentar um pouco o nível de complexidade e visualizar como podemos ir construindo funções mais especializadas e bem definidas. Veja este exemplo:
```jsx
const repeat = (number, action) => {
  for (let count = 0; count <= number; count += 1) {
    action(count);
  }
};

repeat(3, (number) => {
  if (number % 2 === 0) {
    console.log(number, 'is even');
  }
});
```

Pegamos a nossa implementação do exemplo anterior e repassamos dois parâmetros ao chamarmos a função `repeat`, sendo:

**1 -** Um número até que ponto gostaríamos de testar, neste caso `3`;

**2 -** Nossa ação que será executada quando chamada `action(count)` na nossa função `repeat`, neste caso uma função para testar nossos números.

Veja que nosso segundo parâmetro é uma função que recebe o `count` como argumento, proveniente da execução do nosso `action(count)` dentro da função `repeat`. Desse modo, caso o `count` passe pela condição estabelecida para ser um número par, será executada a mensagem com os números que atendem ao critério.

Pense agora que gostaríamos de testar quais números são ímpares. Veja como fica fácil ajustar a implementação:
```js
const repeat = (number, action) => {
  for (let count = 0; count <= number; count += 1) {
    action(count);
  }
};

const isEven = (number) => {
  if (number % 2 === 0) {
    console.log(number, 'is even');
  }
};

const isOdd = (number) => {
  if ((number % 2) > 0) {
    console.log(number, 'is odd');
  }
};

repeat(3, isEven); // Testa quais números serão pares;
repeat(3, isOdd); // Testa quais números serão ímpares;
```

Observe que apenas transportamos e ajustamos a lógica para identificar os números pares e ímpares em duas novas funções chamadas `isEven` e `isOdd`. Após isso, só alteramos o segundo parâmetro ao chamar a função `repeat`.

A função recebida como argumento pela HOF, também é conhecida por `callback`. No exemplo, `repeat` é uma HOF que recebe `isEven` ou `isOdd` como função _callback_.

Veja o exemplo a seguir:

```js
const numberGenerator = () => {
  return Math.random() * 100;
}

console.log(numberGenerator);
```

Ao executar esse código, não recebemos um número aleatório. Isso aconteceu porque na quinta linha do script nós imprimimos apenas a escrita da função. Como não realizamos sua execução, ela não seguiu os procedimentos para retornar um número aleatório. Para executarmos a função, teríamos que inserir `()` na frente do `numberGenerator`.

Essa lógica é a mesma quando usamos _callback_ dentro de outras funções. Lembre-se de que o fato de o JavaScript tratar funções como cidadãs de primeira classe nos permite inseri-las em variáveis. Se você voltar ao primeiro exemplo dessa função, vai ver que a chamada da _callback_ no `addEventListener` funciona de modo similar. Tudo isso é parte de algo maior, são _Higher Order Functions_.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/b92378f4-24bc-4ae2-ada3-99c51cb7fde4/lesson/6403a689-9b92-488c-b3b6-c11e27ef4375)
