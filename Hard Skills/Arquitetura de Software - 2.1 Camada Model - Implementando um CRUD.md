[[Arquitetura de Software]]
[[Arquitetura de Software - 2 Camada Model]]

É muito comum que APIs RESTful possuam endpoints para implementar um CRUD de uma tabela, ou seja, endpoints que permitam cadastrar, listar, buscar algum objeto pelo id, alterar e remover. Portanto a nossa primeira implementação de um código na camada **Model** conterá funções que se comuniquem com a tabela `passengers`. Em paralelo a isso, abordaremos como implementar testes unitários para cada função desse model.

> ⚠ **A proposta é mostrar a implementação da camada de Model. Contudo, ainda não será possível executar uma requisição para uma rota que usa o modelo que desenvolveremos aqui, pois ainda implementaremos as camadas Service e Controller que utilizarão esse componente da camada Model durante os próximos dois dias de conteúdo dessa seção.**

Vamos criar nossa camada **Model** seguindo algumas etapas:

## Setup da camada **Model**

Antes de implementar o model, criaremos a pasta `src/models` e moveremos o arquivo `connection.js` que está em `src` para dentro dessa pasta. Na sequência já criaremos o arquivo `src/models/passenger.model.js` que será o primeiro modelo que desenvolveremos hoje.

Após essas alterações a estrutura de arquivos e diretórios deve estar assim:

```bash
.
├── src/
│   ├── models/
│   │   ├── connection.js
│   │   └── passenger.model.js
│   ├── app.js
│   └── server.js
├── tests/
│   ├── integration/
│   │   └── -
│   └── -unit/
│       └── -
├── env-example
├── docker-compose.yml
├── package.json
├── script.sql
└── thunder-trybecar.json
```

Como alteramos o local do arquivo connection.js de `src` para `src/models` é preciso refletir esse ajuste no arquivo `src/app.js` para que nossa aplicação não falhe para os endpoints que já estão implementados.

```js
// src/app.js
// const express = require('express');
const connection = require('./models/connection');

// ...
// ...
// ...
```

> ⚠️ **A partir daqui usaremos esse padrão das 3 linhas com `// ...` para representar que o arquivo possui um conjunto grande de linhas já existentes/implementadas no arquivo.**

## Implementando a função para listar

Uma das funcionalidades mais básicas de qualquer aplicação é permitir a listagem dos dados de uma determinada tabela. Para podermos retornar os itens que existem na tabela `passengers` implementaremos a função `findAll` em `src/models/passenger.model.js`.

```js
const camelize = require('camelize');
const connection = require('./connection');

const findAll = async () => {
  const [result] = await connection.execute(
    'SELECT * FROM passengers',
  );
  return camelize(result); 
};

module.exports = {
  findAll,
};
```

Começamos a escrita do arquivo, importando a função `camelize` que vem do módulo com o mesmo nome e usamos essa função para transformar os nomes de colunas do padrão **snake_case** (padrão utilizado na nomenclatura de colunas do banco de dados) para **camelCase** (padrão de nomenclatura utilizado em Javascript). Por exemplo, se no objeto existir um atributo com o nome `created_at`, o nome desse atributo após passar pela função `camelize` será alterado para `createdAt`.

Depois disso, importamos o objeto `connection` e definimos a função **findAll** que executará a consulta SQL para recuperar todas as linhas da tabela `passengers` e retornar essas linhas como um _array_ para quem chamar essa função.

Vale reforçar que o módulo `mysql2` envelopa o resultado da consulta `SELECT` em um _array_ bidimensional, ou seja um array com dois arrays dentro. Por isso que usamos a desestruturação do primeiro elemento do _array_ retornada por `connection.execute`. O nosso _result_ é um _array_ formado por vários objetos, onde cada objeto representa uma linha dessa tabela. Essa informação será importante ao implementar o teste dessa função.

### Definindo o arquivo de exportação dos models (_Barrel_)

Acabamos de implementar a primeira função do nosso primeiro model, e a importação dessa função em outro arquivo pode ser feita da seguinte forma.

```js
/* Esse é apenas um exemplo demonstrativo, não precisa replicar ele em nenhum arquivo! */
const { findAll } = require('./models/passenger.model.js');
```

Porém essa forma de importação de função acaba prejudicando a forma que iremos escrever partes dos nossos testes como veremos abaixo. Uma forma de resolver é importando o objeto completo em vez de desestruturá-lo na importação.

```js
/* Este é mais um exemplo demonstrativo que não precisa ser replicado! */
const passengerModel = require('./models/passenger.model.js');
```

É relativamente comum alguns **Services** ou outros componentes da arquitetura utilizarem mais de um model por vez, e para não precisarmos criar várias linhas para importar cada model, vamos usar uma estrutura conhecida como _barrel_. A ideia do _barrel_ é criar um arquivo `index.js` na raiz de uma pasta e qualquer recurso de arquivos dessa mesma pasta vai ser importado através da raiz da pasta.

Para isso, crie o arquivo `index.js` na pasta `src/models` com o seguinte conteúdo.

```js
// src/models/index.js

/* Este vai ser o único lugar do nosso código onde importamos o objeto Model direto do seu arquivo*/
const passengerModel = require('./passenger.model');

module.exports = {
  passengerModel,
};
```

Daqui em diante onde precisarmos importar um _model_ vamos utilizar o seguinte padrão.

```js
/* Este é mais um exemplo demonstrativo que não precisa ser replicado! */
const { passengerModel } = require('./models');
```

O caminho pode mudar de acordo com o arquivo que chama o model, mas ele sempre vai importar sem especificar um arquivo, apenas a pasta _models_, como exportamos um objeto no _barrel_ que vai possuir dentro dele vários objetos, nesse caso vamos importar desestruturando os **Models necessários**.

> ⚠️ Utilizaremos o _barrel_ como padrão daqui em diante para exportar e importar nossos componentes de algumas camadas!

### Escrevendo o teste unitário da função `findAll`

Antes de implementar o teste dessa função, entenderemos qual a importância de escrever testes unitários. Esse tipo de teste serve para garantir que as nossas modificações no código sejam consistentes, ou seja, não adicionem `bugs`. Diferente dos `testes de integração` cujo objetivo é testar a interação entre diferentes componentes, os `testes de unidade` vão testar uma parte específica do código como, por exemplo, uma função para assegurar que essa parte esteja funcionando conforme a especificação.

A ideia para realizar o teste da função `findAll` é verificar se a função `connection.execute`, ao ser executada, nos retorna um _array_ com as linhas da tabela `passengers`. Porém, não é interessante no cenário de testes que o código se comunique com o banco de dados, por algumas razões:

-   **Performance:** Se durante os testes o código realizar a chamada para o banco de dados isso vai deixar o teste mais lento.
-   **Imprevisibilidade:** O banco de dados é um ambiente dinâmico, por isso não temos como ter certeza do que será retornado do banco quando uma consulta for executada. O que pode acontecer é que em um determinado momento, ao rodar os testes, a tabela pode ter um número específico de linhas, e ao executar os testes novamente em outro momento, a mesma tabela pode ter um número diferente de linhas da primeira execução, pois houve interações de pessoas usuárias com o banco entre cada execução. Como no teste precisamos fazer asserções, não é possível usar a resposta real do banco como um parâmetro.

Portanto, para escrever os testes usaremos o recurso de criar um `dublê` para o retorno da função `connection.execute` através do módulo **sinon**. Assim, para escrever o teste da função `findAll` seguiremos duas etapas.

> **⚠️ Existe uma outra abordagem de escrever testes sem criar dublês para as interações com o banco de dados e fazer com que o teste se comunique com o banco de dados. Porém, essa abordagem envolve um processo de _setup_ mais avançado, pois é necessário criar uma instância de banco de dados só para o ambiente de testes e garantir que ele sempre vai ser “resetado” para que o que for feito em um caso de testes não interfira em outro caso de teste.**

#### Etapa 1 - Preparar mock

Criaremos o arquivo `tests/unit/models/mocks/passenger.model.mock.js` que ficará responsável por definir um _array_ que usaremos para ser a resposta **mockada** da função `connection.execute`.

```js
// tests/unit/models/mocks/passenger.model.mock.js
const passengers = [
  {
    id: 1,
    name: 'Doriana Quintal',
    email: 'doriana.quintal@acme.com',
    phone: '(49) 3882-3117',
  },
  {
    id: 2,
    name: 'Leo Sampaio',
    email: 'leo.sampaio@acme.com',
    phone: '(66) 3692-7793',
  },
  {
    id: 3,
    name: 'Anabela Monteiro',
    email: 'anabela.monteiro@acme.com',
    phone: '(49) 2134-2152',
  },
  {
    id: 4,
    name: 'Estêvão Paranhos',
    email: 'estevao.paranhos@acme.com',
    phone: '(82) 2166-2413',
  },
  {
    id: 5,
    name: 'Mateo Vidigal',
    email: 'mateo.vidigal@acme.com',
    phone: '(51) 2303-7355',
  },
];

module.exports = {
  passengers,
};
```

#### Etapa 2 - Implementar o teste da função `passengerModel.findAll`

Crie o arquivo `tests/unit/models/passenger.model.test.js` com o seguinte conteúdo.

```js
// tests/unit/models/passenger.model.test.js
const { expect } = require('chai');
const sinon = require('sinon');
const { passengerModel } = require('../../../src/models');

const connection = require('../../../src/models/connection');
const { passengers } = require('./mocks/passenger.model.mock');

describe('Testes de unidade do model de pessoas passageiras', function () {
  it('Recuperando a lista de pessoas passageiras', async function () {
    // Arrange
    // Act
    // Assert
  });

  afterEach(function () {
    sinon.restore();
  });
});
```

Inicialmente, foram importados os módulos `chai` e `sinon`, necessários para a escrita dos testes de unidade. Em seguida, foram importados os objetos `connection` e `passengerModel` (note que o arquivo já foi importado através do _barrel_ que definimos anteriormente), além dos nossos dados de **mock** através da variável `passengers`.

Foi declarado um `describe` geral que irá agrupar todos os nossos casos de teste. No momento temos apenas um único caso de teste, ou seja, apenas um `it` que vai testar a listagem das pessoas passageiras presentes no banco de dados. E além disso, definimos o `afterEach` para executar `sinon.restore()` que _reseta_ todos os dublês feitos por meio da função `sinon.stub()` que iremos colocar dentro de cada caso de teste.

> *⚠️ É normal que o _eslint_ mostre um _warning_ para o `afterEach` com a mensagem: “Unexpected use of Mocha `afterEach` hook for a single test case”. Quando escrevermos um segundo caso de testes esse _warning_ desparecerá.

Veja que dentro desse teste (`it`) existem comentários que sugerem como o teste deve ser composto. Essa estrutura vem de um padrão consagrado para a escrita de testes, o padrão [Triple A](https://medium.com/@pablodarde/o-padr%C3%A3o-triple-a-arrange-act-assert-741e2a94cf88) e que pode ser usado para testes unitários em qualquer camada. Esse padrão define etapas que devem ser seguidas em cada teste:

-   **Arrange (arranjo):** considera a configuração de tudo que é necessário para a execução do teste, geralmente é aqui que são definidos os dublês para funções chamadas dentro da função que será testada no caso de uso.
-   **Act (ação):** define a execução do teste por meio da chamada de uma função sob teste;
-   **Assert (asserção):** estabelece a verificação do resultado do teste, resultando na falha ou sucesso do mesmo.

> ⚠️ Nem todo cenário de teste demanda um arranjo, um exemplo é quando não for necessário criar um dublê para alguma função chamada dentro da função testada como veremos em alguns testes da camada **Service**.;

Agora que já estudamos o padrão _**Triple A**_, que tal escrever o teste da função `findAll` usando esse padrão?

Copiar

```js
it('Recuperando a lista de pessoas passageiras', async function () {
  // Arrange
  sinon.stub(connection, 'execute').resolves([passengers]);
  // Act
  const result = await passengerModel.findAll();
  // Assert
  expect(result).to.be.deep.equal(passengers);
});
```

O **arranjo** é feito na primeira linha dentro do `it` e serve para definir que estamos usando um dublê para a função `connection.execute` e que nesse cenário o seu retorno será um _array_ com a lista de pessoas passageiras (**`[passengers]`**). Fizemos isso, pois como comentamos um pouco mais acima, essa é a forma que o módulo `mysql2` retorna a resposta do banco ao fazer uma consulta do tipo **SELECT**.

> **📝Anote aí:** O dublê (no nosso caso `sinon.stub().resolves()`) de uma função deve sempre emular o retorno original de uma função.

O próximo passo é definir a **ação**, que nesse caso é chamar a função `passengerModel.findAll()` e guardar seu retorno na variável `result`.

Na última linha do `it`, fazemos a **asserção** para comparar se o valor da variável `result` é igual ao valor da variável `passengers`. Perceba que usamos o _**matcher**_ `to.be.deep.equal`, pois nesse caso estamos comparando dois _arrays_ (`result` e `passengers`).

Pronto, se rodarmos o teste usando o comando `npm test` teremos nossa primeira função devidamente testada. 🎉 🥳 🎉

Até aqui, a estrutura de arquivos e diretórios deve estar assim:

```bash
.
├── src/
│   ├── models/
│   │   ├── connection.js
│   │   ├── index.js
│   │   └── passenger.model.js
│   ├── app.js
│   └── server.js
├── tests/
│   ├── integration
│   └── unit/
│       └── models/
│           ├── mocks/
│           │   └── passenger.model.mock.js
│           └── passenger.model.test.js
├── env-example
├── docker-compose.yml
├── package.json
├── script.sql
└── thunder-trybecar.json
```

## Implementando a função para Buscar por id

Continuando a implementação do componente da camada `Model`, o nosso próximo passo é implementar uma função que receba um **id** como parâmetro e consiga realizar uma busca na tabela `passengers` por esse **id**.

Adicione a função `findById` no arquivo `src/models/passenger.model.js`.

```js
// ...

const findById = async (passengerId) => {
  const [[passenger]] = await connection.execute(
    'SELECT * FROM passengers WHERE id = ?',
    [passengerId],
  );
  return camelize(passenger);
};


// module.exports = {
//   findAll,
     findById,
// };
```

Note que estamos desestruturando o retorno da função `connection.execute` em dois níveis (`const [[passenger]]`) sendo que o primeiro nível retorna o _array_ com as linhas encontradas. Porém, como fazemos uma busca por id, o retorno dessa consulta sempre retornará uma das duas opções abaixo:

-   Um _array_ com apenas um elemento (caso exista algum registro com o `id` informado).
-   Ou um _array_ vazio. (caso não exista nenhum registro com o `id` informado);

Como queremos mostrar apenas um objeto, pegaremos apenas esse primeiro elemento do _array_. Assim como na função `findAll`, aplicamos o `camelize` para transformar o objeto do padrão **snake_case** para **camelCase**

### Implementando o teste

No arquivo `tests/unit/models/passenger.model.test.js` adicione um novo bloco `it` para fazer o teste da função `passengerModel.findById`:

```js
// ...

// describe('Testes de unidade do model de pessoas passageiras', function () {
// ...

  it('Recuperando uma pessoa passageira a partir do seu id', async function () {
    // Arrange
    sinon.stub(connection, 'execute').resolves([[passengers[0]]]);
    // Act
    const result = await passengerModel.findById(1);
    // Assert
    expect(result).to.be.deep.equal(passengers[0]);
  });
// ...
```

Esse teste é similar ao teste do `findAll`, com a diferença que agora o dublê retornará um _array_ apenas com o primeiro item do _array_ `passengers` que vem do nosso arquivo de mock, por isso que é passado o parâmetro `[[passengers[0]]]` para a função _resolves_.

Notou o padrão _**Triple A**_ nesse último teste do nosso código? Ao se habituar a escrever testes usando esse padrão vai perceber como vai ficar mais fácil! 😎

Pronto! Temos mais uma função implementada e testada! 🎉 🥳 🎉


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/35826f95-5fc1-4985-8497-7fc1464a937a)