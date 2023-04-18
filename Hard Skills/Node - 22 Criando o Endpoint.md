[[Node]]


- [Cadastro de Pessoa](#Cadastro%0dde%0dPessoa)
- [Listagem de Pessoas](#Listagem%0dde%0dPessoas)
- [Atualização e Exclusão de Pessoas](#Atualização%0de%0dExclusão%0dde%0dPessoas)





# Cadastro de Pessoa

Com o intuito de deixar nosso projeto organizado (afinal, organização de código é algo muito valorizado no mercado de trabalho!), vamos criar um subdiretório chamado `routes` dentro de `src` para armazenar os arquivos com as rotas do nosso projeto. Você pode fazer isso executando o comando `mkdir -p src/routes` na raiz do projeto.

No subdiretório `src/routes` vamos criar o arquivo `src/routes/peopleRoutes.js` com o seguinte conteúdo:

```js
// src/routes/peopleRoutes.js

const express = require('express');

const router = express.Router();

router.post('/', (req, res) => {
  const person = req.body;
  res.status(201).json(person);
});

module.exports = router;
```

No trecho de código acima, estamos criando o **endpoint** `POST /`. No corpo da requisição é esperado um arquivo **JSON** (o mesmo que definimos no teste de integração) e simplesmente retornamos o mesmo **JSON** como resposta, cujo código de estado é igual a `201`.

Vamos adicionar o seguinte trecho de código para que o `express` publique nossa rota:

```js
// src/app.js

// const express = require('express');
const peopleRoutes = require('./routes/peopleRoutes');

// const app = express();

// app.use(express.json());

app.use('/people', peopleRoutes);

// module.exports = app;
```

No trecho de código acima:

-   Adicionamos uma variável `peopleRoutes` com o _router_ exportado no arquivo `src/routes/peopleRoutes.js`;
-   Adicionamos esse `middleware` definindo que toda requisição em que o **path** comece com `/people` seja encaminhada para ele.

Tenha em mente que o nosso teste ainda irá falhar, mas estamos criando as peças de softwares necessárias para que, em um determinado momento, ele venha a passar! 😎

Nesse momento, teremos a seguinte estrutura de arquivos e diretórios no projeto:

```bash
.
└── trybecash-api/
    ├── src/
    │   ├── db/
    │   │   └── connection.js
    │   ├── routes/
    │   │   └── peopleRoutes.js
    │   ├── app.js
    │   └── server.js
    ├── tests/
    │   └── integration/
    │       └── people.test.js
    ├── docker-compose.yaml
    └── package.json
```

Ao executar novamente o teste de integração com o comando `npm test`, você deve obter uma saída similar a seguinte:

![Saída esperada quando executarmos os testes-criando-endpoint-cadastro-pessoa](https://content-assets.betrybe.com/prod/Sa%C3%ADda%20esperada%20quando%20executarmos%20os%20testes-criando-endpoint-cadastro-pessoa.png)

Saída esperada quando executarmos os testes

O teste ainda está falhando! _Contudo, o que a saída dos testes está nos dizendo?_ 🤔

Ela diz que o teste esperava receber um **JSON** com a chave `message` contendo o valor `Pessoa cadastrada com sucesso com o id 42`.

Porém, o teste está recebendo como resposta o **JSON** que passamos na requisição! 😮

Agora temos que escrever o código necessário para realizar o cadastro de uma pessoa no banco de dados para que retorne a resposta correta. 🚀

## Realizando a comunicação com o MySQL

Chegou o tão aguardado momento de interagir com o servidor MySQL! 🙏

Vamos criar arquivo `src/db/peopleDB.js`, que tem como responsabilidade agrupar todas as operações _SQL_ relacionadas a tabela `people`. Inicialmente vamos escrever o código necessário para inserir uma pessoa no banco de dados, mas ao longo do dia adicionaremos código referente a outras operações.

O arquivo deve conter o seguinte conteúdo:



```js
// src/db/peopleDB.js

const conn = require('./connection');

const insert = (person) => conn.execute(
    `INSERT INTO people 
      (first_name, last_name, email, phone) VALUES (?, ?, ?, ?)`,
    [person.firstName, person.lastName, person.email, person.phone],
  );

module.exports = {
  insert,
};
```

Inicialmente importamos a conexão com o _MySQL_ do nosso outro módulo e, em seguida, editamos a função `insert` para receber como parâmetro um objeto **person**. Nela escrevemos o código referente a um `INSERT` no banco de dados. Então, chamamos a função `conn.execute()`, a qual recebe dois parâmetros:

1.  Uma **string** que contém um _INSERT_ de dados na tabela **people**. Note que a _string_ foi definida utilizando-se crase para possibilitar a quebra de linhas, mas pode-se utilizar as aspas simples ou duplas;
2.  Um array de valores que são extraídos do objeto **person**;

Vale destacar que no final da string que contém o _SQL_ **INSERT**, existem quatro sinais de interrogação. Você pode estar se perguntando: _“Esse SQL não está escrito errado?”_ 🤔

Esses símbolos de interrogação são chamados de **placeholders** (ou **marcadores**, em português). Sua função é de justamente **marcar** os locais que serão substituídas pelos valores dentro da consulta **SQL**.

_E quais são esses valores que substituirão os sinais de interrogação?_ 🤔

São justamente os valores do array que passamos como segundo parâmetro da função `conn.execute()`! A chamada da função `conn.execute()` com os dois parâmetros citados é o que caracteriza uma `prepared statement` no **mysql2**.

Podemos pensar nas `Prepared Statements` como um **template** ou um **molde** para consultas _SQL_ que uma aplicação deseja executar, e que pode ser customizado utilizando variáveis de parâmetros (os **placeholders** ou **marcadores**). Isso nos oferece dois grandes benefícios:

-   As consultas _SQL_ só necessitam ser preparadas uma única vez, entretanto podem ser executadas múltiplas vezes com os mesmos parâmetros ou com parâmetros diferentes. Quando uma consulta é preparada, o banco de dados irá analisar, compilar e otimizar a execução da consulta;
-   Os parâmetros das **prepared statements** não devem ser vinculadas diretamente na consulta _SQL_ (utilizando concatenação de string, por exemplo). O recurso das _prepared statements_ identifica os parâmetros para o banco de dados, evitando que ele erroneamente interprete strings como parte da consulta. Se uma aplicação utiliza `prepared statements` em **todas as operações** que realiza com o banco de dados, essas operações estão seguras contra o ataque do tipo **SQL injection**.

> ⚠️ **Atenção:** **SQL injection** é um tipo de ataque malicioso que uma aplicação Web pode sofrer através de injeção de código _SQL_ em entradas que não tratam os dados de forma adequada (e.g. formulários, APIs REST, etc). O [relatório anual de 2021](https://owasp.org/www-project-top-ten/) da Open Web Application Security Project (OWASP) apontou os ataques de injeção (categoria do **SQL injection**) como o terceiro maior vetor de ataques maliciosos contra aplicações Web. 😨

Na execução dessa _prepared statement_, os **placeholders** serão substituídos pelos valores do array seguindo a mesma ordem nos quais eles foram declarados, ou seja, o primeiro **placeholder** será substituído pelo primeiro valor do _array_; o segundo **placeholder** será substituído pelo valor do segundo valor do array e assim sucessivamente até o último. Dessa forma, podemos reutilizar esse **INSERT** apenas passando valores diferentes para o array!

Agora que temos uma **prepared statement** para inserir uma pessoa, vamos **refatorar** o **endpoint** `POST /` para que ele consiga realizar o cadastro de uma pessoa no banco de dados:

```js
// src/routes/peopleRoutes.js

// const express = require('express');
const peopleDB = require('../db/peopleDB');

// const router = express.Router();

router.post('/', async (req, res) => {
  const person = req.body;
  try {
    const [result] = await peopleDB.insert(person);
    res.status(201).json({
      message: `Pessoa cadastrada com sucesso com o id ${result.insertId}` });
  } catch (err) {
    console.log(err);
    res.status(500).json({ message: 'Ocorreu um erro ao cadastrar uma pessoa' });
  }
});
// module.exports = router;
```

No código acima, importamos o módulo de `src/db/peopleDB.js`. No **endpoint** `POST /`, criamos a variável `person` para receber os dados da pessoa a ser cadastrada.

Em seguida, temos um bloco `try/catch` responsável por responder a requisição. Dentro do bloco `try` é utilizada a função `insert` passando como parâmetro os dados recebidos na requisição e, por conta do `await`, aguardamos a inserção da pessoa no banco de dados.

Se a inserção ocorrer com sucesso, é retornada uma resposta com o status `201` e com um **JSON** contendo uma mensagem indicando o sucesso da operação.

Em caso de erro, ele é impresso no terminal via `console.log` e é retornada uma resposta com o status `500` e com um **JSON** contendo uma mensagem indicando a falha na operação.

Nesse ponto, podemos iniciar a nossa aplicação com o comando `npm start` e realizar uma requisição do tipo **POST** com o `Thunder` para a nossa _API_, passando o seguinte **JSON**:

Copiar

```json
{
  "firstName": "Luke",
  "lastName": "Skywalker",
  "email": "luke.skywalker@trybe.com",
  "phone": "851 678 4453"
}
```

Ao realizar a requisição com o **Thunder Client**, você deve obter um resultado similar ao seguinte:

![Requisição ao endpoint POST people](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20ao%20endpoint%20POST%20people.gif)

Requisição ao endpoint POST /people

Também podemos executar o nosso teste de integração com o comando `npm test` e…

![Saída esperada quando executarmos os testes](https://content-assets.betrybe.com/prod/Sa%C3%ADda%20esperada%20quando%20executarmos%20os%20testes.png)

Saída esperada quando executarmos os testes

O nosso teste passou! 😎

Nesse momento teremos a seguinte estrutura de arquivos e diretórios no projeto:

```bash
.
└── trybecash-api/
    ├── src/
    │   ├── db/
    │   │   ├── connection.js
    │   │   └── peopleDB.js
    │   ├── routes/
    │   │   └── peopleRoutes.js
    │   ├── app.js
    │   └── server.js
    ├── tests/
    │   └── integration/
    │       └── people.test.js
    ├── docker-compose.yaml
    └── package.json
```

![Vamos que vamos!](https://content-assets.betrybe.com/prod/34b05524-d6e3-4a9b-8d49-6643a5979056-Vamos%20que%20vamos!.gif)
Vamos que vamos!



# Listagem de Pessoas

As próximas ações que implementaremos na **API REST** referentes aos **endpoints** de pessoas, não irão requerer criar novos arquivos, apenas adicionar mais linhas de códigos nos arquivos existentes.

Basicamente, trabalharemos apenas nos arquivos `src/db/peopleDB.js`, `src/routes/peopleRoutes.js` e `tests/integration/people.test.js`, graças à organização de arquivos e diretórios utilizada! 🙏

Assim como foi implementada a inserção de uma pessoa no banco de dados, agora vamos implementar dois novos **endpoints**: um que lista todas as pessoas cadastradas no banco de dados e um segundo que lista uma pessoa do banco de dados a partir do seu `id`.

Como feito anteriormente, vamos iniciar o nosso desenvolvimento pelos **testes de integração** adicionando as seguintes linhas de código:

```js
// src/tests/integration/people.test.js

// const chai = require('chai');
// ...

const peopleList = [
  {
    id: 1,
    firstName: 'Luke',
    lastName: 'Skywalker',
    email: 'luke.skywalker@trybe.com',
    phone: '851 678 4453',
  },
  {
    id: 2,
    firstName: 'Dart',
    lastName: 'Vader',
    email: 'dart.vader@trybe.com',
    phone: '851 678 5665',
  },
];

// describe('Testando os endpoints de people', function () {
  
//  ...

  it('Testando a listagem de todas as pessoas', async function () {
    sinon.stub(connection, 'execute').resolves([peopleList]);
    const response = await chai
      .request(app)
      .get('/people');

    expect(response.status).to.equal(200);
    expect(response.body).to.deep.equal(peopleList);
  });

  it('Testando a listagem da pessoa com id 1', async function () {
    sinon.stub(connection, 'execute').resolves([[peopleList[0]]]);
    const response = await chai
      .request(app)
      .get('/people/1');

    expect(response.status).to.equal(200);
    expect(response.body).to.deep.equal(peopleList[0]);
  });

  // afterEach(sinon.restore);
// });
```

Aqui, criamos a constante `peopleList` com um array de pessoas. Em seguida, adicionamos dois casos de testes:

-   Um **stub** para a função `connection.execute()`, que retornará um array que contém outro array de pessoas armazenadas em `peopleList` e um caso de teste responsável por listar todas as pessoas do banco de dados a partir do **endpoint** `GET /people`, no qual é esperado retornar uma lista de pessoas no formato **JSON**;
    
-   Outro **stub** para a função `connection.execute()`, que retornará um array que contém outro array com a primeira pessoa de `peopleList` e outro caso de teste para listar uma pessoa a partir do seu `id` através do **endpoint** `GET /people/:id`, onde `:id` é um parâmetro de rota que indica o `id` da pessoa no banco de dados.
    

> ⚠️ **Atenção:** o fato de estarmos colocando um array dentro de um array ou um objeto dentro de um array nos testes de integração, é para garantir que o retorno do `stub` tenha o mesmo formato do retorno das funções do `mysql2`. 😉

Nesse ponto, você poderá executar os testes de integração com o comando `npm test` e terá a seguinte saída:

![Resultado da execução do comando npm test-listagem-de-pessoas](https://content-assets.betrybe.com/prod/Resultado%20da%20execu%C3%A7%C3%A3o%20do%20comando%20npm%20test-listagem-de-pessoas.png)

Resultado da execução do comando `npm test`

Como esperado, os nossos testes falharam. Era esperado um status `200` e os testes receberam `404`.

Isso ocorreu porque ainda não implementamos os nossos **endpoints**, então vamos adicionar o seguinte código:

```js
// src/routes/peopleRoutes.js

// const express = require('express');
// const peopleDB = require('../db/peopleDB');

// ...

router.get('/', async (_req, res) => {
  try {
    const [result] = await peopleDB.findAll();
    res.status(200).json(result);
  } catch (err) {
    console.log(err);
    res.status(500).json({ message: err.sqlMessage });
  }
});

router.get('/:id', async (req, res) => {
  try {
    const { id } = req.params;
    const [[result]] = await peopleDB.findById(id);
    if (result) {
      res.status(200).json(result);
    } else {
      res.status(404).json({ message: 'Pessoa não encontrada' });
    }
  } catch (err) {
    console.log(err);
    res.status(500).json({ message: err.sqlMessage });
  }
});

// module.exports = router;
```

O código acima adiciona dois novos **endpoints** `GET /` e `GET /:id`. O novo **endpoint** `GET /` contém um bloco `try/catch`, que é responsável por responder a requisição. Dentro do bloco `try` temos uma chamada para a função `findAll` (ainda não foi implementada no arquivo `src/db/peopleDB.js`, mas o faremos em breve), que retorna uma `Promise` (por isso temos um **await** aqui) e realiza a desconstrução da resposta, armazenando na constante `result`.

A constante `result` contém a lista de pessoas e a mesma é retornada como resposta. Caso ocorra algum erro durante a requisição, o bloco `catch` responderá com um código de estado `500` e a mensagem de erro do `mysql2`.

Já o **endpoint** `GET /:id` também contém um bloco `try/catch`, que é responsável por responder a requisição também! Dentro do bloco `try` temos uma chamada para a função `findById` (ainda não foi implementada no arquivo `src/db/peopleDB.js`, mas o faremos em breve), que recebe o parâmetro de requisição `id` (obtido da desestruturação de `req.params`) e retorna uma `Promise` (por isso temos também um **await** aqui), realizando a desestruturação da resposta e armazenando na constante `result`.

A constante `result` contém um array de pessoas. Porém, nesse **endpoint** essa lista pode ter nenhum objeto (situação na qual não existe uma pessoa no banco de dados com o `id` passado como parâmetro) ou um objeto. Por essa razão temos um bloco `if/else` para avaliar se o tamanho do array `result` é maior que zero.

Se o tamanho do array `result` for maior que zero, uma pessoa foi encontrada no banco de dados e é retornada como resposta da requisição com código de estado `200`. Caso contrário, será retornada como resposta da requisição uma mensagem com status 404 indicando que uma pessoa não foi encontrada.

Se executarmos os nossos testes com o comando `npm test` novamente, eles irão falhar e apresentar uma mensagem de erro indicando que `findAll` e `findById` não são funções. O motivo desse erro é que realizamos a chamada dessas funções no arquivo `src/routes/peopleRoutes.js`, mas não as criamos no arquivo `src/db/peopleDB.js` (lembre-se do espírito do TDD 😎).

Vamos adicionar a definição das funções `findAll` e `findById` no arquivo `src/db/peopleDB.js` com o código necessário para realizar as consultas no banco de dados:

```js
// const conn = require('./connection');
// ...

const findAll = () => conn.execute('SELECT * FROM people');

const findById = (id) => conn.execute('SELECT * FROM people WHERE id = ?', [id]);

// module.exports = {
//   insert,
  findAll,
  findById,
// };
```

Foram adicionadas as constantes `findAll` e `findById` onde:

-   A função `findAll` realiza uma consulta no banco de dados, que retorna todas as pessoas cadastradas;
-   A função `findById` realiza uma consulta no banco de dados, que retorna uma pessoa tendo como critério o valor do seu `id`.

Ambas as funções executam `Prepared Statements` no banco de dados (de forma similar ao `insert` que escrevemos antes). Nesse ponto, você pode executar os testes com o comando `npm test` e deve obter uma saída similar à seguinte:

![Resultado da execução do comando npm test-agora](https://content-assets.betrybe.com/prod/Resultado%20da%20execu%C3%A7%C3%A3o%20do%20comando%20npm%20test-agora.png)

Resultado da execução do comando `npm test`

Os nossos testes passaram! 🎉 🥳 🎉

Também podemos iniciar a nossa aplicação com o comando `npm run dev`, cadastrar mais algumas pessoas utilizando o **endpoint** de cadastro de pessoas criado anteriormente e realizar uma requisição do tipo **GET** com o `Thunder` para o **endpoint** `GET /people` da nossa _API REST_.

Ao realizar a requisição, você deve visualizar uma saída similar a seguinte:

![Requisição ao endpoint GET people](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20ao%20endpoint%20GET%20people.gif)

Requisição ao endpoint `GET /people`.

Também podemos realizar uma requisição do tipo **GET** com o `Thunder` para o **endpoint** `GET /people/:id` da nossa _API REST_.

Ao realizar essa nova requisição, você deve visualizar uma saída similar à seguinte:

![Requisição ao endpoint GET people Id](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20ao%20endpoint%20GET%20peopleid.gif)

Requisição ao **endpoint** `GET /people/:id`.

Você terminou de implementar dois **endpoints** capazes de buscar por pessoas cadastradas no banco de dados! 😎

E agora, aproveite para levantar da cadeira e beber uma água 🚰, que no próximo capitulo de Projeto Missions vamos usar o MYSQL em nossos endpoints e refatorar os nossos testes! 🚀


# Atualização e Exclusão de Pessoas

Para finalizar os **endpoints** de pessoas da nossa _API_, faltam ser implementados dois **endpoints**:

-   Um capaz de alterar os dados de uma pessoa previamente cadastrada no banco de dados;
-   Outro para excluir uma pessoa previamente cadastrada no banco de dados.

O código necessário para implementar essas funcionalidades são similares aos utilizados nos **endpoints** de cadastro, de buscar todos e o de buscar pelo `id`.

Então vamos implementar esses dois **endpoints** e finalizar o nosso **CRUD** de pessoas! 😎

Como de costume, vamos iniciar escrevendo os testes, adicionando as seguintes linhas de código:

```js
// src/tests/integration/people.test.js

// ...

// describe('Testando os endpoints de people', function () {
// ...

  it('Testando a alteração de uma pessoa com o id 1', async function () {
    sinon.stub(connection, 'execute').resolves([{ affectedRows: 1 }]);
    const response = await chai
      .request(app)
      .put('/people/1')
      .send(
        {
          firstName: 'Lucão',
          lastName: 'Andarilho dos céus',
          email: 'lucao.andarilho@trybe.com',
          phone: '851 678 4453',
        },
      );

    expect(response.status).to.equal(200);
    expect(response.body).to
      .deep.equal({ message: 'Pessoa de id 1 atualizada com sucesso' });
  });

  it('Testando a exclusão da pessoa com id 1', async function () {
    sinon.stub(connection, 'execute').resolves([{ affectedRows: 1 }]);
    const response = await chai
      .request(app)
      .delete('/people/1');

    expect(response.status).to.equal(200);
    expect(response.body).to
      .deep.equal({ message: 'Pessoa de id 1 excluída com sucesso' });
  });

  // afterEach(sinon.restore);
// });
```

Com isso, foram adicionados dois casos de teste:

-   **Um caso de teste responsável por atualizar os dados de uma pessoa no banco de dados a partir do endpoint `PUT /people/:id`**: esse teste espera o retorno de um objeto com uma mensagem de sucesso da operação com código de estado `200`. Além disso, possui um **stub** para a função `connection.execute()`, que retornará um array contendo um objeto com a chave `affectedRows` com o valor `1`;
    
-   **Um caso de teste responsável por excluir uma pessoa do banco de dados a partir do endpoint `DELETE /people/:id`**: esse teste espera o retorno de um objeto com uma mensagem de sucesso da operação com código de estado `200`. Além disso, também possui um **stub** para a função `connection.execute()`, que retornará um array contendo também um objeto com a chave `affectedRows` com o valor `1`.
    

Nesse ponto, podemos executar os testes com o comando `npm test` e, assim como ocorreu durante a implementação dos **endpoints** anteriores, aqui também ocorrerá um erro na execução dos testes. (`TDD` sempre! 😎)

E qual é o erro apresentado no console? O mesmo que ocorreu na implementação dos **endpoints** anteriores!

A mensagem de erro mostrará que o teste estava esperando um código de estado `200` e foi recebido `404` para ambos os casos de testes.

💭 **Para refletir:** está percebendo que esse padrão está se repetindo? Graças ao uso do `TDD`! Seguindo essa prática de desenvolvimento situações como essa serão comuns e, com o passar do tempo, você ficará craque em perceber esses padrões de erros e saber onde deve-se alterar o código pra que tudo funcione! 😀

![Vamos que vamos!](https://content-assets.betrybe.com/prod/Vamos%20que%20vamos!.gif)
Vamos que vamos!

Da mesma forma que fizemos em **endpoints** anteriores, vamos implementar os novos **endpoints** adicionando o seguinte código:

```js
// src/routes/peopleRoutes.js

// const express = require('express');
// ...

router.put('/:id', async (req, res) => {
  try {
    const { id } = req.params;
    const person = req.body;
    const [result] = await peopleDB.update(person, id);
    if (result.affectedRows > 0) {
      res.status(200).json({ message: `Pessoa de id ${id} atualizada com sucesso` });
    } else {
      res.status(404).json({ message: 'Pessoa não encontrada' });
    }
  } catch (err) {
    res.status(500).json({ message: err.sqlMessage });
  }
});

router.delete('/:id', async (req, res) => {
  try {
    const { id } = req.params;
    const [result] = await peopleDB.remove(id);
    if (result.affectedRows > 0) {
      res.status(200).json({ message: `Pessoa de id ${id} excluída com sucesso` });
    } else {
      res.status(404).json({ message: 'Pessoa não encontrada' });
    }
  } catch (err) {
    res.status(500).json({ message: err.sqlMessage });
  }
});

// module.exports = router;
```

Nesse código adicionamos dois novos **endpoints** que mapeiam `PUT /:id` e `DELETE /:id`. O **endpoint** mapeado com o método _HTTP_ `PUT`, recebe o `id` da pessoa como parâmetro de rota e também um objeto com os dados da pessoa (com o mesmo formato do objeto utilizado anteriormente no cadastro de pessoa). Em seguida é executada a função `peopleDB.update()`, a qual recebe os dados da pessoa e o `id` da pessoa a ser alterada. Essa operação retornará uma `Promise`, que será esperada e desconstruída para obter o `result`.

É realizada uma verificação na qual é avaliado se a quantidade de linhas afetadas com a operação `update` é maior do que `zero` por meio da propriedade `affectedRows` do objeto `result`:

-   Caso a condição seja verdadeira, será enviada uma resposta com o status `200` e uma mensagem de sucesso.
-   Se a condição for falsa, será enviada uma resposta com o status `404` e uma mensagem de erro. Em caso de erro durante a requisição, será enviada uma resposta com o status `500` e uma mensagem de erro.

O **endpoint** mapeado com o método _HTTP_ `DELETE` possui a mesma estrutura do **endpoint** mapeado com o método _HTTP_ `PUT`, exceto pelo fato de que não recebe nenhum **JSON** no corpo da requisição, apenas recebe o `id` da pessoa como parâmetro de rota.

Nesse ponto podemos executar os testes novamente com o comando `npm test` e obteremos uma falha novamente! Você perceberá que a saída é similar quando implementamos os **endpoints** de cadastrar e buscar pessoas no banco de dados!

![Não acredito, quero ver!](https://content-assets.betrybe.com/prod/N%C3%A3o%20acredito,%20quero%20ver!.gif)

Não acredito, quero ver!

O erro que encontramos está relacionado com a implementação dos métodos `update` e `remove` que ainda não foram realizadas no arquivo `src/db/peopleDB.js`. Por não existirem ainda, não é retornado o valor esperado. Logo, vamos adicionar o seguinte código em nosso projeto:

Copiar

```js
// src/db/peopleDB.js

// const conn = require('./connection');
// ...

const update = (person, id) => conn.execute(
    `UPDATE people 
      SET first_name = ?, last_name = ?, email = ?, phone = ? WHERE id = ?`,
    [person.firstName, person.lastName, person.email, person.phone, id],
  );

const remove = (id) => conn.execute('DELETE FROM people WHERE id = ?', [id]);

// module.exports = {
// ...
  update,
  remove,
// };
```

Nesse ponto, se executarmos os testes todos passarão! 🎉 🥳 🎉

Também podemos utilizar o `Thunder` para enviar uma requisição para o **endpoint** `PUT /people/1` com o seguinte **JSON** no corpo da requisição:

Copiar

```json
{
  "firstName": "Lucão",
  "lastName": "Andarilho das estrelas",
  "email": "lucao.andarilho@trybe.com",
  "phone": "851 678 4453"
}
```

> Certifique-se que a aplicação está rodando antes de fazer as requisições. Você pode usar o comando `npm run dev` para isso! 😉

Realizada essa requisição, os dados da pessoa com `id` igual a 1 foram alterados!

Faça uma nova requisição ao **endpoint** `GET /people` para recuperar todas as pessoas cadastradas no banco de dados. Nessa lista você conseguirá visualizar os dados da pessoa com `id` 1 modificados.

Também podemos realizar uma nova requisição ao **endpoint** `DELETE /people/1` para excluir a pessoa com `id` igual a 1.

Novamente, faça uma nova requisição ao **endpoint** `GET /people` para recuperar todas as pessoas cadastradas no banco de dados. Nessa lista, você conseguirá visualizar que a pessoa com `id` igual a 1 não consta mais, pois foi removida do banco de dados!

E aqui terminamos de implementar os **endpoints** relacionados a tabela `people` do banco de dados! 👏

![Parabéns!](https://content-assets.betrybe.com/prod/Parab%C3%A9ns!.gif)

Parabéns!


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/5fe620e6-2a7b-49c2-9e44-ec3c2784f62b)