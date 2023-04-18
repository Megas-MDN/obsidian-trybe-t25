[[Arquitetura de Software]]
[[Arquitetura de Software - 2 Camada Model]]


Agora que já vimos como implementar um model, vamos analisar o código do **endpoint** `POST /passengers/:passengerId/request/travel` que está no arquivo `src/app.js` e ver como podemos refatorar esse código para usar a camada **Model**.

```js
// ...
// ...
// ...

app.post('/passengers/:passengerId/request/travel', async (req, res) => {
  const { passengerId } = req.params;
  const {
    startingAddress,
    endingAddress,
    waypoints,
  } = req.body;

  if (await passengerExists(passengerId)) {
    const [resultTravel] = await connection.execute(
      `INSERT INTO travels 
          (passenger_id, starting_address, ending_address) VALUE (?, ?, ?)`,
      [
        passengerId,
        startingAddress,
        endingAddress,
      ],
    );
    await Promise.all(saveWaypoints(waypoints, resultTravel.insertId));

    const [[response]] = await connection.execute(
      'SELECT * FROM travels WHERE id = ?',
      [resultTravel.insertId],
    );
    return res.status(201).json(camelize(response));
  }

  res.status(500).json({ message: 'Ocorreu um erro' });
});

// ...
// ...
// ...
```

O código acima cria uma solicitação de viagem e é executado na perspectiva da pessoa passageira. O endpoint recebe o id da pessoa passageira como parâmetro da rota e um body no formato **JSON** com os dados da viagem.

Em seguida a função `passengerExists(passengerId)` verifica se existe um passageiro cadastrado no banco de dados com o `id` fornecido e retorna um valor booleano (`true` ou `false`).

No caso da função `passengerExists(passengerId)` retornar verdadeiro, é realizada a inserção no banco de dados de uma viagem solicitada pela pessoa passageira. Em seguida é realizada a inserção dos pontos de parada da viagem (notem a utilização do `Promise.all` para realizar a inserção de forma concorrente).

Na próxima linha a viagem recém cadastrada é recuperada do banco de dados, em seguida a requisição é respondida com status `201`, com a viagem recém cadastrada no corpo da resposta.

Nesse trecho de código temos e a execução de duas operações `SQL` distintas na tabela `travels`. Na primeira uma operação `INSERT` e na segunda uma operação `SELECT`. Vale ressaltar que se precisássemos das mesmas operações em outro lugar do código atualmente teríamos que copiar e colar, ou seja, seria preciso duplicar o código.

Os problemas dessa abordagem ficam evidentes quando queremos modificar uma instrução `SQL` de uma das operações duplicadas. Tomemos como exemplo a instrução `INSERT`, note que estamos realizando a inserção de dados em apenas três das seis colunas existentes da tabela (vide diagrama DER). Se fosse necessário modificar o `SQL` da operação `INSERT` para inserir dados nas seis colunas da tabela essa alteração deve ocorrer em **TODAS** as ocorrências da operação `INSERT`.

Basta apenas esquecermos de alterar uma das ocorrências da operação `INSERT` para que nossa aplicação venha a falhar miseravelmente.

![E agora-model](https://content-assets.betrybe.com/prod/b444fac1-ee73-4a1c-812e-6ad2ea0fe359-E%20agora-model.gif)

E agora?

Esse é o tipo de problema que a camada `Model` irá nos ajudar a resolver. Iremos centralizar nessa camada todo o código que contém operações `SQL` de forma que, quando for necessário realizar alguma modificação em alguma query `SQL`, seja feito em apenas um único lugar.

Então vamos começar a refatorar o código e aplicar a camada `Model`! 🚀🚀🚀


## Refatorando a inserção de viagens

O foco agora é remover qualquer presença de código SQL do nosso arquivo `src/app.js`. Porém, realizaremos isso por etapas. Nosso primeiro objetivo é mover o trecho em destaque para a camada **Model**.

```js
// app.post('/passengers/:passengerId/request/travel', async (req, res) => {
// ...

//   if (await doesPassengerExist(passengerId)) {
        const [resultTravel] = await connection.execute(
          `INSERT INTO travels 
              (passenger_id, starting_address, ending_address) VALUE (?, ?, ?)`,
          [
            passengerId,
            startingAddress,
            endingAddress,
          ],
        );
//     await Promise.all(saveWaypoints(waypoints, resultTravel.insertId));

// ...
```

Já vimos anteriormente como implementar uma função `insert` para o model da tabela `passengers`. Quando pensamos na camada **Model**, o ideal é que cada tabela possua seu próprio arquivo de model com o escopo de lidar com uma tabela específica. Portanto, criaremos agora um model específico para a tabela `travels` que possuirá sua própria versão da função `insert`.

Porém, dessa vez, realizaremos isso usando o fluxo _TDD_ (_Test Driven Development_). No processo _TDD_, primeiro escrevemos o teste antes do código que será testado. Primeiro o teste falhará, e realizaremos alterações no código até passar no teste.

Primeiramente, criaremos o arquivo `tests/unit/models/mocks/travel.model.mock.js` com os dados de `mock` que serão utilizados em nossos testes:

```js
const newTravel =  {
  driverId: 1,
  passengerId: 2,
  travelStatusId: 2,
  startingAddress: 'Rua Alfa',
  endingAddress: 'Rua Omega',
  requestDate: '20202',
};

module.exports = {
  newTravel,
};

```

Nesse arquivo estamos criando e exportando o objeto `newTravel`, que simula um objeto para ser inserido no banco de dados.

Com os nossos dados de `mock` criados, agora geraremos o arquivo: `tests/unit/models/travel.model.test.js`, com o seguinte conteúdo:

```js

const { expect } = require('chai');
const sinon = require('sinon');

const connection = require('../../../src/models/connection');
const { travelModel } = require('../../../src/models');

const { newTravel } = require('./mocks/travel.model.mock');

describe('Testes de unidade do model de viagens', function () {
  it('Realizando uma operação INSERT com o model travel', async function () {
    // arrange
    sinon.stub(connection, 'execute').resolves([{ insertId: 42 }]);

    // act
    const result = await travelModel.insert(newTravel);

    // assert
    expect(result).to.equal(42);
  });

  afterEach(function () {
    sinon.restore();
  });
});
```

Aqui, estamos criando um `teste de unidade` que irá avaliar o comportamento da função `travelModel.insert`. Perceba que o teste dessa função é bastante similar a função `insert` em `tests/unit/models/passenger.model.test.js`.

Se executarmos o teste agora veremos ele falhando, pois ainda não implementamos o componente **Model** da tabela `travels`. Criaremos o arquivo `src/models/travel.model.js` e então a estrutura de diretórios ficará assim:

```bash
.
├── src/
│   ├── models/
│   │   ├── connection.js
│   │   ├── index.js
│   │   └── passenger.model.js
│   │   └── travel.model.js
│   ├── app.js
│   └── server.js
├── tests/
│   ├── integration
│   └── unit/
│       └── models/
│           ├── mocks/
│           │   └── passenger.model.mock.js
│           │   └── travel.model.mock.js
│           └── passenger.model.test.js
│           └── travel.model.test.js
├── env-example
├── docker-compose.yml
├── package.json
├── script.sql
└── thunder-trybecar.json
```

Ao executar o nosso teste com o comando `npm test` ele irá continuar falhando! Isso acontece por não existir a função `insert` no arquivo `src/models/travel.model.js`. Vamos incluir a função `insert` no arquivo `src/models/travel.model.js` para que o erro da falta da função seja resolvido.

Copiar

```js
const insert = (travel) => travel;

module.exports = {
  insert,
};
```

No código acima estamos retornando o objeto `travel` que está sendo recebido como parâmetro da função. A próxima etapa é adicionar esse novo _model_ ao arquivo _barrel_ da pasta _models_.

```js
// src/models/index.js
// const passengerModel = require('./passenger.model');
const travelModel = require('./travel.model');

// module.exports = {
//   passengerModel,
  travelModel,
// };
```

Executaremos o teste de unidade novamente com o comando `npm test` e o mesmo irá falhar novamente! (Lembrem-se que isso faz parte do TDD)😎

Contudo, se observarmos a falha no _console_ agora, veremos que o nosso teste está esperando como resultado o valor `42`, mas está recebendo um objeto como resposta o objeto `travel` (que foi passado como parâmetro). Para resolver isso, temos que refatorar a função `insert` do arquivo `src/models/travel.model.js`.

```js
const snakeize = require('snakeize');
const connection = require('./connection');

const insert = async (travel) => {
  const columns = Object.keys(snakeize(travel)).join(', ');

  const placeholders = Object.keys(travel)
    .map((_key) => '?')
    .join(', ');

  const [{ insertId }] = await connection.execute(
    `INSERT INTO travels (${columns}) VALUE (${placeholders})`,
    [...Object.values(travel)],
  );

  return insertId;
};

module.exports = {
  insert,
};
```

Perceba aqui que replicamos a mesma lógica utilizada na função `insert` em `src/models/passenger.model.js` para função `insert`em `src/models/travel.model.js`. As diferenças foram apenas o nome do parâmetro (`travel`) e o nome da tabela na operação SQL (`INSERT INTO **travels***...`). Caso você precise implementar um model para alguma outra tabela pode replicar o formato desse método e fazer esses ajustes.

Se executarmos nosso teste agora, veremos ele passando. 🎉 🥳 🎉

Agora que temos a garantia que essa funcionalidade atende aos requisitos, podemos substituir o código que fazia a operação `INSERT INTO travels...` do nosso arquivo `app.js` e pela chamada da função `insert` da camada de Models.

Copiar

```js
const express = require('express');
const connection = require('./models/connection');
const camelize = require('camelize'); 

const { travelModel } = require('./models');

// ...

//   if (await doesPassengerExist(passengerId)) {
      /* Aqui substituímos o trecho de código SQL pela chamada a função insert do model
     e armazenamos o retorno da função na variável travelId */
      const travelId = await travelModel.insert({ passengerId, startingAddress, endingAddress });

      /* Renomeamos o parâmetro result.insertId para travelId */
      await Promise.all(saveWaypoints(waypoints, travelId));

      const [[response]] = await connection.execute(
        'SELECT * FROM travels WHERE id = ?',

        /* Renomeamos o parâmetro result.insertId para travelId */
        [travelId],
      );
//     return res.status(201).json(camelize(response));
//   }

// ...
```

Pronto, já conseguimos fazer a refatoração do código que insere uma viagem no banco de dados, deixamos o nosso código mais enxuto, e agora temos um método reutilizável. Todo momento em que precisarmos realizar uma inserção na tabela `travels`, podemos usar a função `travelModel.insert`.

Agora é hora de mais uma pausa para beber uma água e alongar um pouco antes de seguirmos para a próxima refatoração.

## Refatorando a busca de viagem por id

Na lição anterior, refatoramos a inserção de viagens, que era realizada diretamente no arquivo `src/app.js` para um componente na camada `Model`. Porém, o código atual do endpoint POST `/passengers/:passengerId/request/travel` ainda contém um código SQL que faz uma busca de uma viagem pelo id

```js
// app.post('/passengers/:passengerId/request/travel', async (req, res) => {
// ...

      const [[response]] = await connection.execute(
        'SELECT * FROM travels WHERE id = ?',

        // Renomeamos o parâmetro result.insertId para travelId
        [travelId],
      );
//     return res.status(201).json(response);
//   }

// ...
```

Ainda seguindo a ideia do TDD, Começaremos a escrever o `teste de unidade` para a função do model que busca uma viagem a partir do seu `id`.

Começaremos adicionando no arquivo `tests/unit/models/mocks/travel.model.mock.js` os dados de `mock` que serão utilizados em nossos testes:

```js

const travelsFromDB = [
  {
    
    id: 1,
    driver_id: 3,
    passenger_id: 4,
    travel_status_id: 1,
    starting_address: 'Rua XYZ',
    ending_address: 'Rua ABC',
    request_date: '20202',
  },
  {
    
    id: 2,
    driver_id: 1,
    passenger_id: 2,
    travel_status_id: 2,
    starting_address: 'Rua Alfa',
    ending_address: 'Rua Omega',
    request_date: '20202',
  },
];

const travels = [
  {
    
    id: 1,
    driverId: 3,
    passengerId: 4,
    travelStatusId: 1,
    startingAddress: 'Rua XYZ',
    endingAddress: 'Rua ABC',
    requestDate: '20202',
  },
  {
    
    id: 2,
    driverId: 1,
    passengerId: 2,
    travelStatusId: 2,
    startingAddress: 'Rua Alfa',
    endingAddress: 'Rua Omega',
    requestDate: '20202',
  },
];

// ...

// module.exports = {
  travels,
  travelsFromDB,
//   newTravel,
// };

```

Nesse arquivo adicionamos dois arrays: `travelsFromDB` e `travels`, que também estão sendo exportados. O array `travelsFromDB` é um array de objetos o qual simula uma resposta do banco de dados (em `snake_case`), enquanto o array `travels` simula a resposta da camada `Model` (em `camelCase`).

O próximo passo é adicionar o seguinte conteúdo no arquivo `tests/unit/models/travel.model.test.js`:

```js
// ...

// Aqui estamos adicionando a importação do travelsFromDB
const { newTravel, travels, travelsFromDB } = require('./mocks/travel.model.mock');

// describe('Testes de unidade do model de viagens', function () {
  // ...

  it('Recuperando uma travel a partir do seu id', async function () {
    // arrange
    sinon.stub(connection, 'execute').resolves([[travelsFromDB[0]]]);
    // act
    const result = await travelModel.findById(1);
    // assert
    expect(result).to.be.deep.equal(travels[0]);
  });

// ...
```

Perceba que o teste aqui preserva a mesma ideia do testes do **Model** de pessoas passageiras.

Nesse momento, se executarmos o teste com o comando `npm test` teremos uma falha pelos mesmos motivos do teste escrito anteriormente (por faltar a implementação da função `findById`). Agora implementaremos a função `findById` de maneira apropriada. 👍

No arquivo `src/models/travel.model.js` adicionaremos a função `findById` com o seguinte código:

```js
const camelize = require('camelize');
// const snakeize = require('snakeize');
// const connection = require('./connection');

// ...

const findById = async (travelId) => {
  const [[result]] = await connection.execute(
    'SELECT * FROM travels WHERE id = ?',
    [travelId],
  );
  return camelize(result);
};

// module.exports = {
//   insert,
  findById,
// };
```

Aqui existe uma diferença em relação ao arquivo `passenger.model`, o nome da tabela na operação SQL de INSERT é **travels** (`SELECT * FROM **travels**...`).

Execute o teste novamente com `npm test` e veja que agora o teste vai passar. 🎉 🥳 🎉

Com essa adição podemos realizar mais uma refatoração no arquivo `src/app.js` substituindo o código antigo pela chamada da função `travelModel.findById`:

Copiar

```js
//const express = require('express');

/* Aqui podemos remover a importação da função camelize pois já está sendo utilizada no model */

// ...

// app.post('/passengers/:passengerId/request/travel', async (req, res) => {
// ...

//   if (await doesPassengerExist(passengerId)) {
// ...

    /* Aqui substituímos a consulta SQL pela nossa função findById */
    const travel = await travelModel.findById(travelId);
    /* Aqui não é mais necessário usar o camelize pois o model já retorna o objeto no formato correto. */
    return res.status(201).json(travel);
//   }

// ...
```

Note que além de remover a query SQL que estava no trecho de código também removemos o acoplamento do arquivo `app.js` com o módulo `camelize`. Agora é responsabilidade do componente da camada _**Model**_ retornar o dado no formato apropriado.

Temos o nosso **endpoint** `POST /passengers/:passengerId/request/travel` devidamente refatorado acomodando o código referente às nossas `entidades` na camada `Model`, ou seja, no arquivo `src/models/travel.model.js`. 🎉 🥳 🎉

## Refatorando a rota GET /drivers/open/travels

Para consolidar nossos estudos sobre a camada `Model`, vamos refatorar o endpoint `GET /drivers/open/travels`. Agora todo o código de acesso ao banco de dados na camada ficará na camada de `Model`. O trecho de código a ser refatorado em `src/app.js` é o seguinte:

```js
// ...

app.get('/drivers/open/travels', async (_req, res) => {
  const [result] = await connection.execute(
    'SELECT * FROM travels WHERE travel_status_id = ?',
    [WAITING_DRIVER],
  );
  res.status(200).json(camelize(result));
});

// ...
```

Note que temos uma consulta `SQL` na tabela `travels`, responsável por buscar todas as viagens onde o valor da coluna `travel_status_id` seja igual à constante `WAITING_DRIVER`. Vamos mover essa consulta para a camada `Model`. 😎

Adicionaremos mais um caso de testes no arquivo `tests/unit/models/travel.model.test.js` com o seguinte conteúdo:

```js
// ...

// describe('Testes de unidade do model de viagens', function () {
  // ...

  it('Recuperando as travels a partir do seu travel_status_id', async function () {
    // arrange
    sinon.stub(connection, 'execute').resolves([travelsFromDB]);
    // act
    const result = await travelModel.findByTravelStatusId(1);
    // assert
    expect(result).to.be.deep.equal(travels);
  });

// ...
```

Se executarmos os testes com o comando `npm test` eles falharão e acho que você já deve imaginar o porquê! 🙃

Nesse ponto, adicionaremos o seguinte código no arquivo `src/models/travel.model.js`:

```js
// ...

const findByTravelStatusId = async (travelStatusId) => {
  const [result] = await connection.execute(
    'SELECT * FROM travels WHERE travel_status_id = ?',
    [travelStatusId],
  );
  return camelize(result);
};

// module.exports = {
//   insert,
//   findById,
  findByTravelStatusId,
// };
```

Agora se executarmos os `testes de unidade` com o comando `npm test` os mesmos passarão! 🎉 🥳 🎉

Logo podemos refatorar o endpoint `GET /drivers/open/travels` substituindo o código existente por este:

```js
// ...

app.get('/drivers/open/travels', async (_req, res) => {
  const result = await travelModel.findByTravelStatusId(WAITING_DRIVER);
  res.status(200).json(result);
});

// ...
```

Note que o código refatorado ficou mais simples e semântico do que o antigo. Essa é a vantagem de acomodar todo código que lida com as nossas entidades na camada `Model`.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/3f4c4253-0ea5-4432-9176-68610d749584)