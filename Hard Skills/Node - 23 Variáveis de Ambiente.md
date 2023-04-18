[[Node]]


Antes de avançarmos com nossos estudos, precisamos falar de uma situação que, se não for tratada devidamente, pode se tornar um problema em nossa aplicação: os dados necessários para conectar ao banco de dados estarem escritos explicitamente dentro do arquivo `src/db/connection.js`.

_E qual é o problema disso?_ 🤔

Quando o seu código for versionado em um repositório **GitHub** por exemplo, esses dados estarão lá e se o repositório for **PÚBLICO** todas as pessoas que olharem o arquivo `src/repository/connection.js` verão os dados utilizados para conectar ao servidor _MySQL_. Agora imagine se as credenciais existentes nesse arquivo forem dados de um servidor MySQL de produção ao qual apenas pessoas autorizadas deveriam ter acesso? Agora as credencias estão visíveis no **GitHub**! Seria um caos! 🙄

Portanto devemos separar os dados de configuração (no nosso caso do servidor MySQL) da nossa aplicação _Node.js_ e _express_. Para alcançar esse objetivo vamos utilizar um recurso chamado `variável de ambiente`. 😍

Uma **variável de ambiente é um recurso disponível nos `sistemas operacionais` que permite criar uma variável no formato `NOME_DA_VARIÁVEL=VALOR`, onde `NOME_DA_VARIÁVEL` é o nome da variável de ambiente, e `VALOR` se refere a um valor que será vinculado à variável**. Toda vez que solicitarmos ao `sistema operacional` o valor de uma variável de ambiente, fornecemos a ele uma `NOME_DA_VARIÁVEL` e ele retorna o `VALOR` associado a esta chave, se ela estiver definida.

Para exemplificar isso, ao digitar o seguinte comando no console será apresentado o valor da variável de ambiente `$USER`, cujo valor é o nome de usuário da pessoa que está utilizando o sistema no momento da execução do comando:


```bash
echo $USER
```

A figura abaixo exibe a saída do console ao executar o comando anterior:

![Resultado da execução do comando echo USER](https://content-assets.betrybe.com/prod/Resultado%20da%20execu%C3%A7%C3%A3o%20do%20comando%20echo%20USER.png)

Resultado da execução do comando echo $USER

Você deve estar se perguntando: _como as variáveis de ambiente nos ajudarão a resolver e separar os dados de configuração da nossa aplicação?_ 🤔

O Node.js possui a capacidade de ler variáveis de ambiente definidas em um `sistema operacional`. Vamos ver um exemplo simples! Adicione a seguinte linha:

```js
// server.js

// const app = require('./app');
// ...

// app.listen(port, async () => {
  // console.log(`API TrybeCash está sendo executada na porta ${port}`);
  console.log(`Valor da variável de ambiente $USER: ${process.env.USER}`);
// });
```

A partir de agora, teremos a seguinte saída no console:

![Saída da aplicação após a leitura da variável de ambiente](https://content-assets.betrybe.com/prod/Sa%C3%ADda%20da%20aplica%C3%A7%C3%A3o%20ap%C3%B3s%20a%20leitura%20da%20vari%C3%A1vel%20de%20ambiente.png)

Saída da aplicação após a leitura da variável de ambiente

Note que nossa aplicação conseguiu ler o conteúdo de uma variável de ambiente do `sistema operacional` através do objeto `process.env.NOME_DA_VARIÁVEL`! 😍

Como você já deve estar pensando nesse momento, a solução para nosso dilema será criar variáveis de ambiente para as configurações de acesso ao servidor de banco de dados e ler os valores através do objeto `process.env`. E para facilitar ainda mais o nosso trabalho, vamos utilizar uma biblioteca JavaScript chamada de `dotenv`.

A **biblioteca `dotenv` é um módulo Javascript que carrega variáveis de ambientes armazenadas em um arquivo `.env` para o `process.env`**.

A vantagem de utilizar um arquivo para armazenar as variáveis de ambiente é abstrair a criação das variáveis de ambiente diretamente no `sistema operacional`, pois a forma de criar e disponibilizar variáveis de ambientes varia de um sistema operacional para outro!

Agora vamos refatorar nossa aplicação para utilizar variáveis de ambiente com ajuda do módulo `dotenv` 😎

Primeiramente vamos instalar o módulo `dotenv` como dependência do nosso projeto:

```bash
npm i dotenv@16.0.3 --save-exact
```

Em seguida, vamos criar o arquivo `.env` na raiz do nosso projeto com o seguinte conteúdo:


```bash
MYSQL_HOST=localhost
MYSQL_PORT=33060
MYSQL_USER=root
MYSQL_PASSWORD=root
MYSQL_DATABASE_NAME=trybecashdb
MYSQL_WAIT_FOR_CONNECTIONS=true
MYSQL_CONNECTION_LIMIT=10
MYSQL_QUEUE_LIMIT=0
```

Agora vamos refatorar o arquivo `src/db/connection.js` para utilizar os valores definidos nas variáveis de ambiente:

```js
// src/db/connection.js

// ...

// const connection = mysql.createPool({
  host: process.env.MYSQL_HOST,
  port: process.env.MYSQL_PORT,
  user: process.env.MYSQL_USER,
  password: process.env.MYSQL_PASSWORD,
  database: process.env.MYSQL_DATABASE_NAME,
  waitForConnections: process.env.MYSQL_WAIT_FOR_CONNECTIONS,
  connectionLimit: process.env.MYSQL_CONNECTION_LIMIT,
  queueLimit: process.env.MYSQL_QUEUE_LIMIT,
// });

// module.exports = connection;
```

No arquivo `src/server.js` vamos carregar as variáveis de ambiente definidas no arquivo `.env` inicializando o `dotenv`:

Copiar

```js
// src/server.js

require('dotenv').config();
// const app = require('./app');

// ...
```

Ao executarmos a aplicação novamente, veremos que a mesma inicializará e, caso realizar alguma requisição para um dos **endpoints** implementados, tudo estará funcionando como antes.

Contudo, os dados necessários para a conexão do banco de dados estão sendo lidos do arquivo `.env`. 😎

Mas nossa missão não terminou: se enviarmos o arquivo `.env` para nosso repositório **GitHub**, ainda teremos o mesmo problema com os dados de configuração ficando públicos.

Para solucionar esse problema, basta colocar o arquivo `.env` na lista de arquivos ignorados pelo **git**, o arquivo `.gitignore`. Assim, vamos criar o arquivo `.gitignore` (caso o mesmo ainda não esteja criado) e adicionar uma nova linha com o seguinte conteúdo:

```bash
node_modules
.env
```

A partir desse momento, o **git** ignorará o arquivo `.env` em **commits** futuros, mantendo os dados de configurações não versionados no repositório.

Uma boa prática é criar um arquivo `.env` de exemplo. Assim, quando outras pessoas realizarem um clone do seu repositório, elas terão um exemplo das variáveis de ambientes que devem estar no arquivo `.env` e podem preencher com os valores pertinentes ao seu ambiente de desenvolvimento.

Por exemplo, vamos criar o arquivo `.env-example` com o seguinte conteúdo:

```bash
MYSQL_HOST=<ENDEREÇO DO BANCO>
MYSQL_USER=<NOME DE USUÁRIO DO BANCO>
MYSQL_USER=<PORTA DE CONEXÃO DO BANCO>
MYSQL_PASSWORD=<SENHA DE ACESSO DO BANCO>
MYSQL_DATABASE_NAME=<NOME DO BANCO DE DADOS>
MYSQL_WAIT_FOR_CONNECTIONS=true
MYSQL_CONNECTION_LIMIT=10
MYSQL_QUEUE_LIMIT=0
```

Note que os dados sensíveis foram substituídos por valores informativos e este arquivo pode ser versionado normalmente no **GitHub** sem prejuízo de vazamento de dados de acesso ao banco de dados. 😎

> ⚠️ **Atenção:** lembre-se de adicionar o arquivo `.env` no `.gitignore` antes de realizar um **commit** no repositório! 😬 No arquivo `README.md` do seu repositório crie uma seção explicando a necessidade de renomear o arquivo `.env-example` para `.env` e alterar o arquivo com os dados necessários para acessar o banco de dados 😉


#### Recursos adicionais (opcional)

-   [Repositório da biblioteca `mysql2`](https://github.com/sidorares/node-mysql2)
-   [Documentação da biblioteca `dotenv`](https://www.npmjs.com/package/dotenv)
-   [Testes de integração para aplicações Node.js com Mocha e Chai](https://medium.com/desenvolvimento-com-node-js/testes-de-integra%C3%A7%C3%A3o-para-aplica%C3%A7%C3%B5es-node-js-com-mocha-e-chai-610a1ba15e1b)
-   [Testes de integração para API com Typescript, mocha, chai e sinon](https://dev.to/matheusg18/testes-de-integracao-para-api-com-typescript-mocha-chai-e-sinon-3np9)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/aa97630a-167e-456b-b18f-bdc3019202b5)
