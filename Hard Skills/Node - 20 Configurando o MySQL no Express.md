[[Node]]
[[Mysql]]
[[Node - 14 Middlewares]]

Primeiramente, vamos instalar as dependências necessárias para configurarmos um projeto Express capaz de conectar ao MySQL. No diretório raiz do projeto, execute o seguinte comando:

```bash
npm i express@4.17.1 mysql2@2.3.3 --save-exact
```

A novidade aqui está no módulo (ou _drive_) **mysql2**, responsável por permitir que uma aplicação **Node.js** consiga comunicar-se com o _MySQL_. Comumente chamamos esse tipo de biblioteca (que permite nossa aplicação conversar com banco de dados) de **client**, o qual possui todo o código necessário para enviarmos comandos _SQL_ para o nosso banco de dados, no caso o _MySQL_, e recebermos as respostas dos comandos enviados.

Precisaremos criar em nossa aplicação o arquivo `src/db/connection.js`, que será responsável por realizar a conexão com o servidor MySQL utilizando a biblioteca `mysql2`:

```js
// src/db/connection.js

const mysql = require('mysql2/promise');

const connection = mysql.createPool({
  host: 'localhost',
  port: 33060,
  user: 'root',
  password: 'root',
  database: 'trybecashdb',
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0,
});

module.exports = connection;
```

No trecho de código acima estamos importando a biblioteca **mysql2** com o recurso de `promises`. Isso permitirá utilizar o _MySQL_ de forma assíncrona com **async/await**. Em seguida, criamos uma constante `connection` que recebe um `pool de conexões` criado com a função **createPool**.

Um `pool de conexões` é um repositório que contém um conjunto de conexões estabelecidas previamente com o banco de dados. Essas conexões serão reutilizadas durante a execução da aplicação conforme a necessidade. Em outras palavras, quando uma operação no banco de dados for necessária nossa aplicação irá:

1.  Requisitar uma conexão no `pool` de conexões;
2.  Utilizar essa conexão para enviar uma operação _SQL_ ao servidor _MySQL_;
3.  Devolver a conexão para o `pool` de conexões ao final da operação com o _MySQL_;
4.  Tornar a conexão disponível para ser utilizada em requisições futuras.

O diagrama abaixo mostra de forma visual a interação entre uma aplicação Node.js, o `pool` de conexões e o servidor MySQL.

![Diagrama de interação entre Nodejs o pool de conexões e o servidor MySQL](https://content-assets.betrybe.com/prod/Diagrama%20de%20intera%C3%A7%C3%A3o%20entre%20Nodejs%20o%20pool%20de%20conex%C3%B5es%20e%20o%20servidor%20MySQL.png)

Diagrama de interação entre Node.js, o pool de conexões e o servidor MySQL

O uso do `pool` de conexões é encorajado, pois sem ele, para cada operação com o _MySQL_ uma conexão seria aberta e, após seu uso, seria fechada. Assim, seria necessário abrir novamente uma nova conexão com o _MySQL_ para executar uma nova operação. E abrir uma nova conexão com o _MySQL_ demanda tempo, adicionando um atraso para cada requisição da _API_ como consequência.

Logo, o uso de um `pool` de conexões acelera o processo de execução de consultas no _MySQL_, pois reutiliza as conexões em operações futuras, não precisando criar uma nova conexão a cada operação.

A função **createPool** recebe um objeto com os seguintes parâmetros:

Parâmetro | Descrição | Observações
-- | -- | --
**host** | O endereço _IP_ do _MySQL_ | Como temos um container `docker` sendo executado em nossa máquina local, o valor será **localhost** ou **127.0.0.1** (ambos são equivalentes)
**user** | O nome de usuário que nossa aplicação utilizará para acessar o _MySQL_ | Estamos utilizando o usuário **root** do _MySQL_
**port** | O número da porta que nossa aplicação utilizará para acessar o _MySQL_ | Estamos utilizando a porta 33060 (a porta do computador local que vinculamos com o container no `docker compose`)
**password** | A senha do usuário que nossa aplicação utilizará para acessar o _MySQL_ | Estamos utilizando a senha **root** que foi definida na variável de ambiente **MYSQL_ROOT_PASSWORD** no `docker compose` criado anteriormente
**database** | O nome do banco de dados _MySQL_, o qual queremos que nossa aplicação realize uma conexão | Estamos utilizando o nome do banco que foi definido na variável de ambiente **MYSQL_DATABASE** no `docker compose`
**waitForConnections** | Determina qual será a ação da `pool` de conexões quando nenhuma conexão estiver disponível na `pool` e quando o limite de criação de novas conexões tiver sido alcançado | Se o valor for **true**, será criada uma fila de espera por conexões, caso contrário a `pool` retornará uma _callback_ com um erro. Caso este parâmetro seja omitido, o valor padrão será **true**
**connectionLimit** | O número máximo de requisições de conexão que a `pool` criará de uma vez | Caso este parâmetro seja omitido, o valor padrão será **10**
**queueLimit** | O número máximo de requisições de conexão que a `pool` irá enfileirar antes de retornar um erro | Se o valor deste parâmetro for igual a **0** significa que não existe limite. Caso este parâmetro seja omitido, o valor padrão será **0**

Agora que o conceito de `pool` de conexões foi explicado e o arquivo `connection.js` foi criado, está na hora de configurarmos o `express` no projeto e testarmos se ele consegue se comunicar com o MySQL. Para isso, vamos criar o arquivo `src/app.js` com o seguinte conteúdo:

```js
// src/app.js

const express = require('express');

const app = express();

app.use(express.json());

module.exports = app;
```

No código acima estamos criando as definições do `express`. Vale ressaltar que a função `app.listen()` não está sendo executada no arquivo `src/app.js`. Contudo, estamos realizando um `module.exports` na constante `app` que inicializa o express e registra os `middlewares` que serão utilizados inicialmente.

A razão disso é que quando formos escrever nossos testes de integração, a definição de inicialização, rotas e `middlewares` do express, devem estar separadas da inicialização dele. Isso nos permitirá criar um `mock` das nossas rotas facilitando o processo de testar nossa API.

🤔 Você deve estar se perguntando: “_onde realizaremos a chamada da função `app.listen()` necessária para inicializar o express?”_ Nesse ponto entra o nosso arquivo `src/server.js`, no qual adicionaremos o seguinte conteúdo:

```js
// src/server.js
const app = require('./app');
const connection = require('./db/connection');

const PORT = 3001;

app.listen(PORT, async () => {
  console.log(`API TrybeCash está sendo executada na porta ${PORT}`);

  // O código abaixo é para testarmos a comunicação com o MySQL
  const [result] = await connection.execute('SELECT 1');
  if (result) {
    console.log('MySQL connection OK');
  }
});
```

Acima, criamos uma constante `app` que importa o que foi definido no arquivo `src/app.js` e, a partir dessa constante, iniciamos o nosso `express` executando a função `app.listen()`.

Dentro da função `app.listen()` foi adicionado um trecho de código que executa a função `connection.execute()`, que recebe como parâmetro uma consulta SQL `SELECT 1`. Essa função realiza uma conexão com o MySQL, executa o SQL passado como parâmetro e recebe uma resposta que é armazenada na constante `result` (note que o processo de desestruturação de variáveis está sendo utilizado! 😎).

Depois é verificado com um `if` se o objeto `result` contém alguma coisa e, em caso de positivo, é impresso no console a mensagem `MySQL connection OK`. Se você for no console e executar o comando `npm start`, o `express` será iniciado e apresentará a seguinte saída:

![Saída esperada ao inicializar o projeto](https://content-assets.betrybe.com/prod/Sa%C3%ADda%20esperada%20ao%20inicializar%20o%20projeto.png)

Saída esperada ao inicializar o projeto.

Se você obteve na saída do terminal a mensagem `MySQL connection OK`, saiba que acabou de realizar a sua primeira conexão com o MySQL por meio do **Express**! Parabéns! 🎉 🥳 🎉

Pode parecer pouca coisa, mas não é! Você realizou toda a configuração necessária para que isso fosse possível e, a partir desse ponto, podemos criar funcionalidades mais complexas utilizando comandos SQL mais robustos!

Antes de avançarmos, vamos `refatorar` nosso arquivo `src/server.js` para retirar o código que utilizamos para testar se a comunicação com o MySQL estava ocorrendo, pois esse código não será mais útil para nós de agora em diante. O arquivo deverá estar assim:

```js
// src/server.js

const app = require('./app');

const PORT = 3001;

app.listen(PORT, () => {
  console.log(`API TrybeCash está sendo executada na porta ${PORT}`);
});
```

E nesse ponto teremos a seguinte estrutura de arquivos e diretórios no projeto:

```bash
.
└── trybecash-api/
    ├── src/
    │   ├── db/
    │   │   └── connection.js
    │   ├── app.js
    │   └── server.js
    ├── tests/
    │   └── -
    ├── docker-compose.yaml
    └── package.json
```



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/d55e780a-a5a4-44a4-8d83-d73a2c99c691)

