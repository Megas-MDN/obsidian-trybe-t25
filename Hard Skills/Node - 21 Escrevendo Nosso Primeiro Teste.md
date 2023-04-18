[[Node]]


Agora chegou a hora de colocarmos a mão na massa e escrevermos as funcionalidades da nossa _API_! Este é um bom momento para exercitarmos a prática do `TDD` ou `Desenvolvimento Guiado por Testes`.

Quanto mais você exercitar a prática do desenvolvimento de software com `TDD`, melhor suas habilidades ficarão, aumentando suas chances em conseguir a sua oportunidade no mercado de trabalho!

![Então que comece a diversão!](https://content-assets.betrybe.com/prod/Ent%C3%A3o%20que%20comece%20a%20divers%C3%A3o!.gif)

Então que comece a diversão!

Para começar, vamos instalar as dependências necessárias para escrevermos nossos testes de integração. Então, execute o seguinte comando para realizar a instalação das dependências `mocha`, `chai`, `sinon` e `chai-http` como **dependências de desenvolvimento**:

```bash
npm i mocha@10.0.0 chai@4.3.6 sinon@14.0.0 chai-http@4.3.0 -D
```

Que tal começarmos criando uma pessoa no banco de dados? Então antes de escrever o teste e, consequentemente, nosso código, vamos entender o fluxo de cadastro de pessoas que iremos implementar.

O fluxo se dará da seguinte maneira:

1.  Primeiramente receberemos uma `requisição` para o `endpoint` **POST /people**. Essa requisição terá no seu corpo um `JSON` com os dados a serem cadastrados no banco de dados similar ao seguinte:

```json
{
  "firstName": "Luke",
  "lastName": "Skywalker",
  "email": "luke.skywalker@trybe.com",
  "phone": "851 678 4453"
}
```

2.  Em seguida, o express passará o `JSON` recebido na requisição para um componente de software (o qual iremos desenvolver 😉) que irá enviar uma declaração _SQL_ `INSERT` para o **MySQL**;
    
3.  Após o envio do comando _SQL_ inserção da pessoa no MySQL, receberemos uma resposta do MySQL sobre a operação;
    
4.  Enviamos a resposta para a requisição com o código de estado `201` se a operação ocorreu com sucesso, ou o código de estado `500` caso algum erro ocorrer durante o processo de cadastro da pessoa no **MySQL**.
    

A figura abaixo exibe uma representação do fluxo de cadastro de pessoas em nossa aplicação.

![Diagrama com o fluxo de cadastro de pessoas](https://content-assets.betrybe.com/prod/Diagrama%20com%20o%20fluxo%20de%20cadastro%20de%20pessoas.png)

Diagrama com o fluxo de cadastro de pessoas.

> 👀 **De olho na dica:** lembre-se que é muito mais fácil escrevermos código quando o problema a ser resolvido está nítido. 😉

Nesse ponto vamos criar o subdiretório `tests/integration`, que conterá os nossos testes de integração. Você pode fazer isso com o comando `mkdir -p tests/integration` a partir do diretório raiz do projeto.

Assim, teremos a seguinte estrutura de arquivos e diretórios no projeto:

```bash
.
└── trybecash-api/
    ├── src/
    │   ├── db/
    │   │   └── connection.js
    │   ├── app.js
    │   └── server.js
    ├── tests/
    │   └── integration/
    │       └── _
    ├── docker-compose.yaml
    └── package.json
```

> ⚠️ **Atenção:** lembre-se que quando estamos trabalhando com testes, podemos escrever testes de integração e testes de unidade. Uma boa prática é escrever esses testes em diretórios separados e, por esta razão, estamos criando o subdiretório `tests/integration`. Caso estivéssemos trabalhando também com testes de unidade, eles seriam escritos no subdiretório `tests/unit`. 😉

Finalmente, vamos escrever um pouco de código! 🙏

Vamos criar o arquivo `tests/integration/people.test.js` com o seguinte conteúdo:

```js
//  tests/integration/people.test.js

const chai = require('chai');
const chaiHttp = require('chai-http');
const sinon = require('sinon');

const app = require('../../src/app');
const connection = require('../../src/db/connection');

const { expect, use } = chai;

use(chaiHttp);

describe('Testando os endpoints de people', function () {
  it('Testando o cadastro de uma pessoa ', async function () {
    sinon.stub(connection, 'execute').resolves([{ insertId: 42 }]);

    const response = await chai
      .request(app)
      .post('/people')
      .send(
        {
          firstName: 'Luke',
          lastName: 'Skywalker',
          email: 'luke.skywalker@trybe.com',
          phone: '851 678 4453',
        },
      );

    expect(response.status).to.equal(201);
    expect(response.body).to.
      deep.equal({ message: 'Pessoa cadastrada com sucesso com o id 42' });
  });

  afterEach(sinon.restore);
});
```

Com esse código, fazemos as importações necessárias para realizar os **testes de integração**.

Em seguida são criadas as variáveis `app` e `connection` que fazem referência aos módulos `src/app.js` e `src/db/connection.js`. Teremos apenas um `describe` que agrupará os testes relacionados ao endpoint `people`.

Dentro do `describe` criado, temos um caso de teste (declaração `it`) que realiza duas tarefas:

-   Cria um `stub` com o **sinon** na função `execute` de `connection`, de maneira que quando essa função for chamada no teste, ela retornará um array contendo um objeto com a chave `insertId` com o valor 42.
    
-   Uma requisição ao **endpoint** `POST /people` passando um **JSON** com os dados da pessoa a ser cadastrada no corpo da requisição.
    

> ⚠️ **Atenção:** o fato de estarmos colocando um objeto dentro de um array nos testes de integração é para garantir que o retorno do `stub` tenha o mesmo formato do retorno das funções do `mysql2`.

Também foi adicionado um `afterEach` após a declaração `it`, que desfaz o `stub` criado, fazendo com que o método `execute` de `connection` se comporte conforme nossa implementação.

Você deve estar se perguntando o seguinte: _por que estamos criando um `stub` no método `execute` de **connection**?_ 🤔

Nós temos acesso ao método `execute` através da biblioteca `mysql2`, que possui seus testes de integração e testes unitários. Como a biblioteca `mysql2` realiza os testes nas funções que ela disponibiliza, podemos assumir em nossos testes que, da chamada da função `connection.execute()` em diante, tudo está sendo testado!

> 👀 **De olho na dica:** caso tenha curiosidade em saber como são os testes da biblioteca `mysql2`, acesse a pasta tests do [github](https://github.com/sidorares/node-mysql2) da biblioteca.

**Em resumo:** só precisamos testar o comportamento da nossa aplicação até a chamada da função `connection.execute()` (que criamos o mock), que retornará um resultado conhecido e, de posse desse resultado, verificará se a aplicação gera a resposta apropriada.

> ⚠️ **Atenção:** essa premissa é válida para qualquer biblioteca que estivermos utilizando em nossa aplicação e não apenas para `mysql2`. Teste de software é uma boa prática de desenvolvimento, principalmente em bibliotecas escritas pela comunidade. Logo, não precisamos testar o que já está testado!

Para podermos executar o nosso teste (e vermos ele falhar 😛), temos que alterar a chave `test` dos scripts do `package.json`:

Copiar

```json
{
  ...
  "scripts": {
    ...
    "test": "mocha tests/**/*$NAME*.test.js --exit"
  },
  ...
}
```

Agora que temos tudo que é necessário para executarmos nosso teste, vamos executá-lo com o seguinte comando:

```bash
npm test
```

Teremos a seguinte saída:

![Saída esperada quando executarmos os testes-escrevendo-primeiro-teste](https://content-assets.betrybe.com/prod/Sa%C3%ADda%20esperada%20quando%20executarmos%20os%20testes-escrevendo-primeiro-teste.png)

Saída esperada quando executarmos os testes

Como esperado, o nosso teste falhou! 🎉 Vamos analisar a falha e, a partir dela, começarmos a escrever o código para que o teste passe! 😎

O erro apresentado está nos informando que o nosso teste esperava receber um código de estado `201`, mas ele recebeu o código `404`. Isso ocorre porque não criamos ainda o **endpoint** `/people`!

Então vamos criar nosso endpoint? 🚀



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/84ce7903-c73a-42fe-81d9-36e3cb271cf6)
