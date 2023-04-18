[[Node]]

## Contexto/ História

Vamos começar a abordar esse assunto por um exemplo.

Vamos imaginar que você está trabalhando em um projeto particular que faz coisas sensacionais, e agiliza muito sua vida. Inicialmente, você não tem a intenção de tirá-lo de da sua máquina.

Logo, poderia colocar alguns dados como:  

```
// imaginem que esse é seu cpf
const cpf = '000.000.000-00';
// e esse é seu cartão de crédito
const creditCard = '9999999999999999';
```

Se meu projeto não for sair da sua máquina, tudo bem (melhor ainda seria se a máquina estivesse desconectada da internet 🤣). E sempre que seu cartão expira, você deve procurar no seu código esse campo e atualizá-lo (mas isso é moleza, por você conhece de o código como "a palma da sua mão").

Mas, e se tivesse que subir esse código para uma pessoa de sua maior confiança, para ela também poder aproveitar dos benefícios dessa aplicação? Poderíamos enviar do jeito que está (lembre-se que essa pessoa é uma das que você mais confia, e com razão). Quando ela fosse utilizar teria que trocar os dados seus dados pelos dela.  

```
// const cpf = '000.000.000-00';
// imaginem que esse é o cpf dela
const cpf = '111.111.111-11' ;

//const creditCard = '9999999999999999';
// e esse é o cartão de crédito dela
const creditCard = '8888888888888888';
```

Até aqui também tudo bem.

Agora vamos pensar que essa aplicação é tão boa que necessita de de várias outras configurações padrões que não necessitam de alteração, mas terminam de certa forma dificultando acharmos esses valores que necessitam ser trocados.

Isso já começa a incomodar, não a você, pois sabe exatamente onde alterar esse valor, porém as pessoas de sua confiança que receberam uma cópia desse código não vão "gostar" tanto desse trabalho,né?!

[![achando dados no código](https://res.cloudinary.com/practicaldev/image/fetch/s--rDKzbWgv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i5s63wr2u4kelws5zstn.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--rDKzbWgv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i5s63wr2u4kelws5zstn.png)

Vamos ser mais criativos, e imaginar que uma dessas pessoas perdeu seu código em uma convenção de fraude de cartões de crédito, que para seu azar contou com a presença de várias pessoas que "vivem" disso para algumas apresentações.

E agora, como você fica? Com desespero, angustia ou raiva?

[![Desespero](https://res.cloudinary.com/practicaldev/image/fetch/s--6ttySNJ1--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/es8ewy6fg9ppw6xpqt7q.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--6ttySNJ1--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/es8ewy6fg9ppw6xpqt7q.png)

Será que isso poderia ter sido evitado de alguma forma?

Essas situações temos algumas em comuns: todas envolvem dados:

-   Sensíveis 🤐;
-   Expiráveis ⌛;
-   Personalizáveis 😎 😇 😁;
-   E de certa forma catastróficos se perdidos 🤯.

## [](https://dev.to/pauloricardoz/usando-variaveis-de-ambiente-em-nodejs-env--4ioi#vamos-para-a-solu%C3%A7%C3%A3o)Vamos para a solução

Então como deveriamos ter procedido nesse caso?

Poderiamos ter configurado nosso ambiente de trabalho para que ele, e somente ele soubesse os valores desses dados.

Mas como fazer isso, você deve estar se perguntando:

Utilizando NodeJS podemos fazer isso de 2 formas fáceis.  
1️⃣ A primeira seria passando os valores que queremos dentro do código direto no terminal. Vamos ver como ficaria para passar o CPF para dentro da aplicação.  

```
CPF=111.111.111-11 node appMaravilha.js
```

Dentro da nossa aplicação esse valor vai ficar "conectado" ao processo da aplicação maravilhosa que foi desenvolvida. Logo, dentro do código você pode acessar da seguinte forma:  

```

const cpf = process.env.CPF ;
// Esse ainda é seu cartão de crédito
const creditCard = '9999999999999999';
```

Notem que haveria a necessidade de colocar as aspas para delimitarmos onde o valor começa e termina quando tiver caracteres que podem fazer o terminal achar que estamos fazendo outro comando (como espaço, <, >, e outros).

2️⃣ A segunda seria criando uma arquivo para guardar essas variáveis que você quer no seu ambiente/máquina (em inglês: environment variables). E o nome desse arquivo é `.env`, dessa forma ele fica escondido de pessoas desavisadas por causa do `.`(ponto) no começo do nome e o `env` representa o enviroment (ambiente).

E como fica a criação do desse arquivo? Simples, vamos dar uma olhada.  

```
CPF=111.111.111-11
CREDIT_CARD =9999999999999999
```

Nesse caso não se deve colocar `aspas` para passar qualquer tipo de valor. Tudo dentro do arquivo `.env` é considerado como string.

E para capturar esse valor no código deve-se fazer a adição de um pacote chamada `dotenv` (em inglês, dot=ponto / env=ambiente).  

```
require('dotenv').config();
// outra forma possível de usar esse pacote
// require('dotenv/config') ;

const cpf = process.env.CPF ;
const creditCard = process.env.CREDIT_CARD;
```

Um ponto importante é que geralmente colocamos esse arquivo `.env` na pasta raiz do projeto, pois a função `config` busca na pasta do arquivo que a executou, e posteriormente nas pastas "pais". Existe a possibilidade de termos mais de 1 arquivo _.env_, mas isso é fortemente desaconselhado.😱

## [](https://dev.to/pauloricardoz/usando-variaveis-de-ambiente-em-nodejs-env--4ioi#uma-forma-melhor-que-a-outra)Uma forma melhor que a outra?

Como na vida, não existe uma solução perfeita. Tendo uma boa justificativa e um código bem construído, ambas tem vantagens.

Seja por velocidade em alternar entre os valores, agilidade para passar/definir uma grande quantidade de variáveis de uma única vez e/ou facilidade de repetir o processo atribuição desses dados.

## [](https://dev.to/pauloricardoz/usando-variaveis-de-ambiente-em-nodejs-env--4ioi#boas-pr%C3%A1ticas)Boas práticas

🧐 É importante resaltar que _NÃO HÁ PADRÃO OFICIAL_ de como escrever os nomes das variáveis de ambiente, mas é quase um consenso de utilizar em SNAKE_CASE em caixa alta (palavras maiúsculas separadas por underscore). _Logo, se utilizar alguma forma diferente dessa existe a chance de te olharem da mesma forma que olham para pessoas desenvolvedoras que usam tema claro na IDE para codarem 🤣_.

✨ Quando construir seu código coloque valores padrões para caso alguém rode seu código não receba erros porque usa lógica não estava esperando um valor `undefined`. Nosso código ficaria assim:  

```
require('dotenv').config();

const cpf = process.env.CPF || '555.555.555-55';
const creditCard = process.env.CREDIT_CARD || '5555555555555555';
```

🔨 Quando achar viável, desconstrua as variáveis atribuindo valores padrões.  

```
require('dotenv').config();

const {
   cpf = '555.555.555-55', 
   creditCard = '5555555555555555'
} = process.env;
```


## Resumo técnico

### Passando direto no terminal

Não há necessidade de pacotes adicionais.  
No terminal:  

```
NOME_DA_VARIAVEL=VALOR_QUE_SERA_UMA_STRING node app.js
```

No código:  

```
const NOME_DA_VARIAVEL = process.env.NOME_DA_VARIAVEL;
```

### Passando através de um arquivo `.env`

Necessitamos do dotenv.  
No arquivo .env:  

```
NOME_DA_VARIAVEL=VALOR_QUE_SERA_UMA_STRING
```

No código:  

```
require('dotenv/config')
const NOME_DA_VARIAVEL = process.env.NOME_DA_VARIAVEL;
```

###### Fonte: [https://dev.to/pauloricardoz](https://dev.to/pauloricardoz/usando-variaveis-de-ambiente-em-nodejs-env--4ioi)
