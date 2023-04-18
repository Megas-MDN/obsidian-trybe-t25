[[Node]]

- [Linter e Git](#Linter%0de%0dGit)
- [Criando o servidor](#Criando%0do%0dservidor)
- [Ganhando produtividade com o Nodemon](#Ganhando%0dprodutividade%0dcom%0do%0dNodemon)



Pergunta: **como vamos construir uma API no Node.js?**🤔

> Precisamos de uma forma de receber requisições, tratá-las e devolvê-las, e até então não sabemos fazer nada disso! Além disso, precisamos saber nos organizar - caso contrário, na medida em que nossa aplicação crescer, ela vai começar a se tornar uma grande bagunça, fazendo com que as coisas comecem a quebrar!

Resposta: É para isso que surge o _framework Express_! Ele nos ajuda a organizar e construir APIs robustas e flexíveis, nos dando ferramentas que fazem as coisas acontecerem com poucas linhas de código.

> Quando nós abrimos [o site do Express](http://expressjs.com/), a primeira frase que ele nos traz, em tradução livre, é:
> 
> “Express
> 
> Framework web rápido, flexível e minimalista para Node.js”

Você pode estar se perguntando: “Mas o que é um **framework**?” 🤔

Resposta: Pense no framework, do inglês **molde**, como um conjunto de coisas prontas, como se fosse por exemplo um molde para fazer/criar outras coisas.

> Imagine que você vá fazer uma sopa, para isso você precisará seguir alguns processos, tais como: descascar e cozinhar os legumes, acrescentar água com o caldo, deixar ferver e temperar. Você pode optar por ir cortando e descascando os alimentos na medida em que precisa deles, enquanto a água ferve, ou pode cortar tudo antes e só colocá-los na panela juntos depois. Ou seja, há mais de uma forma de se fazer esse prato.

No entanto, se você trabalhasse em um restaurante que serve 500 tigelas de sopa por dia, a instrução seria uma só: descasque e corte tudo com antecedência para que, na hora de preparar o prato, só precise juntar todos os ingredientes e ferver. Você teria todos os potinhos para guardar os ingredientes e a panela de água já no fogo para quando precisasse 🧑‍🍳

Há várias formas de se fazer uma sopa, mas o restaurante propõe usar uma que será melhor pra sua organização e eficiência, e te dá ferramentas para isso. Um framework é a mesma coisa: ele te sugere uma forma específica de construir sua aplicação e te dá ferramentas pra fazer isso mais rápido.

[No site do Express](http://expressjs.com/), ele traz mais algumas informações, como os tópicos:

-   Web Applications
-   APIs
-   Performance
-   Frameworks

De olho na dica 👀: Guarde para ler depois! 😉

Agora, que você já tem uma base do que é um **framework**, bora instalar o Express na sua aplicação. Para isso, execute o comando abaixo:


```bash
npm i express@4.17.1 --save-exact
```

> ⚠️ Aviso: Aqui, vamos usar a `versão 4.17.1`, pois é a mesma versão que iremos usar no projeto deste bloco! Iremos determinar uma versão para todas as nossas dependências para evitarmos comportamentos inesperados.

Após executar o comando acima, um arquivo e um diretório serão criados automaticamente - o `package-lock.json` e o `node_modules`!

-   O arquivo `package-lock.json` serve para gerenciar as dependências de nossas dependências;
-   O diretório (_node_modules_) é onde todas as nossas dependências, e dependências de nossas dependências, serão instaladas. Entendeu ou pareceu um pouco confuso? 🤪

![Ilustração de uma arvore de pacotes node](https://content-assets.betrybe.com/prod/61e782b6-8f46-448f-9dd9-a1362df08ca2-Ilustra%C3%A7%C3%A3o%20de%20uma%20arvore%20de%20pacotes%20node.png)

Ilustração sobre funcionamento de uma instalação de dependências através do npm.

Pense assim: nossa aplicação depende do pacote **Express** para funcionar… O pacote Express, por sua vez, depende de outros pacotes para funcionar! Da mesma forma, cada pacote depende de mais pacotes, e aí já podemos concluir que precisamos de uma forma eficaz de buscar e instalar todos esses pacotes sem erro!

O Node faz isso para nós, de forma que toda vez que instalamos algum pacote em nossa aplicação, o Node “automagicamente” irá instalar as coisas de que esse pacote precisa.

> Se alguma dessas coisas já estiver instalada por causa de outro pacote na sua aplicação, ele apenas a reutiliza, para não ter que instalar nada duas vezes! Inteligente, não?! 🧐

## Linter e Git

Antes de continuar, como nós já sabemos, é fundamental garantir a qualidade de escrita do nosso código! Por isso, vamos instalar e configurar o `ESLint`, com as regras que usamos na Trybe na nossa aplicação. Isso é bem simples e vai agregar demais no seu currículo, hein! Comece executando o comando abaixo:

```bash
npm i eslint@6.8.0 eslint-config-trybe-backend@1.0.1 --save-dev --save-exact
```

Antes de continuar sua configuração, perceba que todos os arquivos que construímos até agora estão dentro do diretório raiz da aplicação: `soccer-team-manager`, e não na pasta `src`.

De olho na dica 👀: O diretório `src` só irá conter arquivos e diretórios referentes ao código fonte da aplicação (código escrito por você)!

É normal encontrarmos repositórios no GitHub com diferentes configurações, mas geralmente mantendo um comportamento comum:

-   na raiz do projeto ficam arquivos de configuração como: `.gitignore`, `.eslintrc.json`, `package.json`, `docker-compose.yml` e outros;
-   o código da aplicação fica em diretórios como: `src`, `app`, ou similar.

Sabendo disso, crie os arquivos referentes a configuração do ESLint na raiz:

```bash
touch .eslintignore .eslintrc.json
```

-   `.eslintignore`: Usado para você dizer ao ESLint que ignore arquivos e diretórios específicos;
-   `.eslintrc.json`: Usado para você sobrescrever regras do ESLint;

Dentro do arquivo `.eslintignore`, vamos ignorar apenas os arquivos que estão dentro do diretório `node_modules`.

> Nesse diretório tem muito código de outras pessoas e não cabe a nós melhorá-lo.

```bash
// .eslintignore

node_modules
```

E dentro do arquivo `.eslintrc.json`, você vai escrever o seguinte trecho de código:

```json
// .eslintrc.json
{
  "env": {
    "es2020": true
  },
  "extends": "trybe-backend",
  "rules": {
    "sonarjs/no-duplicate-string": ["error", 5]
  }
}
```

Aqui, você especifica o padrão de qualidade que pretende usar - as regras de estilo de 2020, estendendo as regras da Trybe para Back-end e acrescentando uma regra em particular que usamos no projeto.

> De olho na dica 👀: Se quiser saber mais sobre estas configurações do ESLint, [acesse a documentação](https://eslint.org/docs/latest/user-guide/configuring/)

Finalize inicializando um repositório git na pasta da aplicação, criando e configurando o arquivo `.gitignore`:

```bash
git init && touch .gitignore
```

```bash
// .gitignore

node_modules
```

Ufa! Configuramos quase tudo. Já faça um commit inicial e, se quiser, crie um repositório remoto no seu GitHub para já fazer alguns _pushes_ 🙌

## Criando o servidor

Configurar seu projeto é um **super** passo!

Quando você entra em uma empresa para trabalhar em algum projeto, você precisa saber como ele está configurado e como ele funciona, para só então continuar seu desenvolvimento! Porém, quando você faz um teste técnico para uma vaga de emprego, geralmente você deve montar uma aplicação do zero. Então, em ambos os casos, você precisa saber lidar com as configurações de um projeto a partir do zero!

De olho na dica 👀: Guarde a referência desse conteúdo para consultar sempre que precisar, pois toda vez que você for configurar uma aplicação do zero há grandes chances de se esquecer de fazer alguma coisa.

Após você ter terminado as configurações iniciais do seu projeto, vamos codar um pouco e ver na prática a criação deste famoso servidor Node.js com Express.

Para começar, vá ao diretório `src` e crie mais dois arquivos: um chamado `app.js` e o outro `server.js`. Como nossa aplicação será pequena, isso basta pra nós por ora. Se precisarmos de mais arquivos, depois refatoramos sem medo! 🔧

Vamos começar pelo arquivo `app.js`:

```js
// src/app.js
const express = require('express');

const app = express();

module.exports = app;
```

Neste arquivo, por ora, você apenas importou o pacote do Express e iniciou ele em seu programa com a função `express()` e o colocou na variável `app`, exportando a variável `app` para poder usá-la no arquivo `server.js`. Tudo que o Express nos dá está dentro dessa variável `app`, é como se ela fosse um “objeto grandão” cheio de funções e informações que serão úteis para nós em um futuro próximo (mais conhecido como o próximo arquivo 😂).

Agora, dentro do arquivo `server.js`, escreva o trecho de código abaixo:

```js
// src/server.js
const app = require('./app');

app.listen(3001, () => console.log('server running on port 3001'));
```

Aqui, novamente, apenas importamos nosso arquivo `app.js` e aí sim, damos _start_ em nosso servidor.

O _start_ é provido pelo trecho `app.listen...` e dentro dele podemos passar até 2 parâmetros:

-   Primeiro parâmetro é o `port` _(ou porta)_: Aqui passamos 3001, mas poderia ser qualquer número não utilizado acima de 1023;
    
-   Segundo parâmetro é uma `função`: Aqui passamos apenas um `console.log` exibindo uma mensagem “que estamos no ar”;
    

Você pode estar se perguntando: “mas por que separamos em dois arquivos?| 🤔

A resposta é: para deixar mais organizado. Isso será útil caso nossa aplicação comece a crescer e para no futuro quando aprendermos testes de unidade/integração no back-end, pois irá facilitar nossa vida na hora de testar nossos testes. 😁

Agora para finalizar…

Calma aí, finalizar o servidor! Ainda vamos continuar a aplicação! 💚 Mas perceba que o servidor é apenas isso: uma importação do `Express` e um `listen`, incrível não?

Para ver o `console.log` na tela, vá no arquivo `package.json` e insira estes 3 scripts, dentro da chave `"scripts"`:

```json
// package.json

"start": "node src/server.js",
"dev": "nodemon src/server.js",
"lint": "eslint --no-inline-config --no-error-on-unmatched-pattern -c .eslintrc.json ."
```

Antes de executar sua aplicação, que tal ver se o que escrevemos até agora está tranquilo para o lint? Para isso, execute o comando `npm run lint` e observe se existe algum problema! Se estiver tudo ok, vamos ver se nosso servidor executa.

> Volte em seu terminal e execute o comando `npm start`. Observe que após o início do servidor, em seu terminal irá aparecer a mensagem **server running on port 3001**, isso quer dizer que está tudo bem. 👍

**Mas o que raios é uma porta?** E o que quer dizer “ouvir”? 🤔

Anota aí 🖊: Em poucas palavras, o sistema operacional da sua máquina determina como todos os programas rodando nele interagem com ele. Cada programa escolhe uma “porta”, identificada por um número, e o sistema operacional garante que todas as requisições de rede direcionadas pra ele e pra porta daquele número serão direcionadas pra esse programa. Dizemos que um programa está “ouvindo”, do inglês “listen”, uma porta quando ele está alocado pelo sistema operacional pra ela. Ou seja: seu programa escolheu pra si uma porta e tudo que chegar com o número dela vai pra ela. Veremos, logo mais, como esse número chega. 😉

Mas calma ai. Colocamos 3 scripts no package.json e só executamos um! E olha só, esse script nomeado como `"dev"` não irá funcionar se você tentar executar, pois observe que no início dele existe um comando chamado `nodemon`. Mas que negócio é esse? 🤔

## Ganhando produtividade com o Nodemon

Imagine que após ter executado o comando `npm start`, você queira alterar a mensagem que esta no console. A mensagem está em inglês, mas agora você quer que ela esteja em português. Para isso, basta ir no arquivo `server.js` e alterar o `console.log` para: _‘Servidor online na porta 3001’_.

Observe que nada mudou em seu console do terminal, pois para refletir as mudanças feitas após subir o servidor, precisamos pará-lo e depois iniciá-lo novamente!

Em seu terminal, pressione `ctrl + c` para derrubar o servidor e após isso execute o comando `npm start` novamente. Observe que a mensagem foi alterada. Mas, e se você quiser mudar a mensagem novamente voltando para inglês… Ou pior, quando tiver mais arquivos em sua aplicação, imagine ter que fazer esse processo de parar/subir o servidor novamente toda vez que mudar alguma linha! Cansativo não? Agora, imagina se esquecermos de fazer isso e ficarmos olhando para um código executado desatualizado! 😱 Totalmente inviável.

Com base nisso, surge o pacote do `nodemon`. Usando o servidor com nodemon, toda vez que você salvar algum arquivo, ele reinicia sua aplicação _automagicamente_! 🪄

![Mágica!](https://content-assets.betrybe.com/prod/61e782b6-8f46-448f-9dd9-a1362df08ca2-M%C3%A1gica!.gif)

Mágica!

Anteriormente, já configuramos a chamada dele no script `"dev"`. Agora, basta instalar o pacote como dependência de desenvolvimento:

```bash
npm i nodemon@2.0.15 --save-dev --save-exact
```

Após a instalação, execute o comando `npm run dev` e observe que toda vez que salvar algum arquivo, o servidor irá reiniciar novamente.

> De olho na dica 👀: Você vai observar que em alguns comandos utilizamos a palavra `run`(exemplo: `npm run dev` ou `npm run lint`) e em outros não! Isso se dá devido a uma configuração do próprio NPM, em que scripts como `start` e `test` já vem pré configurados, enquanto os outros que colocamos a gosto precisam da palavra `run` para serem executados.

E eis que você já aprendeu outra habilidade do dia : “_Utilizar_ o _Nodemon_ para auxiliar no desenvolvimento de APIs _Node.js_ com o _framework_ _Express_“. Se prepara que vai começar a ficar ainda mais legal! 🤩

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/0290ddd3-3a5f-4ce2-aebc-d6e3e9f5854e)
