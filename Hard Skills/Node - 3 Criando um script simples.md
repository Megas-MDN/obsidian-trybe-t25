[[Node]]


Agora que chegamos até aqui, vamos criar o famoso Hello World em Node.js. Vem com a gente!

## Criando o pacote Node.js

Vamos começar criando uma nova pasta, chamada `hello-world`, na qual escreveremos nosso código.

Uma vez dentro dessa pasta, execute o comando `npm init`.

> Lembre-se de deixar todas as perguntas com o valor padrão, a não ser o nome da pessoa autora (`author:`), onde você colocará seu nome.

Pronto! Nosso pacote está criado. Abra a pasta `hello-world` no VSCode e vamos começar a criar nosso script.

## Criando o código do Hello, world!

Dentro da pasta `hello-world`, crie um arquivo chamado `index.js`. Por padrão, esse é o arquivo principal de qualquer aplicação Node.js e é comum darmos esse nome ao arquivo que deve ser executado para iniciar nosso programa.

> Sendo assim, por convenção, **todo pacote Node.js deve ter um arquivo index.js**, salvo exceções, que devem ser documentadas no README do repositório.

Dentro do `index.js`, adicione o seguinte código:

```js
console.log('Hello, world!');
```

Pronto, nosso script de “Hello, world!” está criado! Mas nosso pacote ainda não está pronto. Vamos criar um script `start` para estarmos aderentes às convenções do Node.js.

## Criando o script `start`

Como você viu anteriormente, para criar um script precisamos alterar o `package.json` da nossa aplicação. Sendo assim, abra o `package.json` da pasta `hello-world` e altere a linha destacada para criar o script start dessa forma:

```json
// {
//   "name": "hello-world",
//   "version": "1.0.0",
//   "description": "",
//   "main": "index.js",
//   "scripts": {
//     "test": "echo \"Error: no test specified\" && exit 1",
       "start": "node index.js"
//   },
//   "author": "Seu nome",
//   "license": "ISC"
// }
```

## Executando o script

Agora que temos tudo criado e configurado, chegou a hora de executar nosso Hello, world! Para isso, navegue até a pasta `hello-world` no terminal e execute `npm start`.

Pronto! Temos nosso primeiro “Hello, world!” sendo executado com Node.js!

Mas, cá entre nós, você não acha que essa coisa de “Hello, world!” simples um pouco repetitiva para quem já está no módulo de Back-end!?🤔

Vamos dar uma incrementada nesse script, adicionando o nome e sobrenome da pessoa que chamou nosso script!

## Lendo input do terminal

Para podermos ler o nome e sobrenome da pessoa que executou o script, vamos utilizar um pacote de terceiros: o [`readline-sync`](https://www.npmjs.com/package/readline-sync).

-   Por tratar-se de um módulo de terceiros, precisamos primeiro instalar o `readline-sync` pra podermos utilizá-lo no código.

Para fazer isso, basta executarmos o comando `npm i --save-exact readline-sync@1.4.10` dentro da pasta `hello-world`.

Anota aí 🖊: A letra `i` do comando acima é um atalho para `install`. Ela também funciona com a flag `-D` para `devDependencies`, e sem parâmetro nenhum, para instalar as dependências listadas no `package.json`.

Uma vez instalado o pacote, podemos utilizá-lo em nosso script. Para isso, precisamos, primeiro, importá-lo desse jeito:

```js
const readline = require('readline-sync');

// console.log('Hello, world!');
```

Perceba que, apesar do pacote chamar-se `readline-sync`, podemos dar qualquer nome para a `const` que usamos para importá-lo.

Agora, com o pacote em mãos, podemos utilizar as funções `question` e `questionInt` disponibilizadas por ele para perguntar à pessoa usuária seu nome e idade:

```js
// const readline = require('readline-sync');

const name = readline.question('Qual seu nome? ');
const age = readline.questionInt('Qual sua idade? ');

// console.log('Hello, world!');
```

A função `question` interpreta a resposta como uma string comum, ao passo que a função `questionInt` converte a resposta para número utilizando o `parseInt` e retorna um erro caso a pessoa tente inserir algo que não seja um número válido.

Pronto, agora o último passo é utilizarmos essas novas variáveis para compor nossa mensagem de olá. Bora fazer isso então:

```js
// const readline = require('readline-sync');

// const name = readline.question('What is your name? ');
// const age = readline.questionInt('How old are you? ');

console.log(`Hello, ${name}! You are ${age} years old!`);
```

Se executarmos novamente, veremos o resultado: perguntamos qual o nome e idade da pessoa e depois exibimos uma mensagem personalizada.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/1f6bf65e-2ceb-4663-a4be-92619e46c887)