[[Node]]
[[Node - 12 Testes de Integração]]

- [Construindo a API](#Construindo%0da%0dAPI)
- [Dublês de teste](#Dublês%0dde%0dteste)
- [Finalizando a API](#Finalizando%0da%0dAPI)

Agora que já conhecemos os contratos da nossa API, iremos configurar o nosso ambiente para darmos início ao desenvolvimento usando TDD.

> Para isso, crie uma pasta chamada `cacau-trybe` e, dentro dela, inicialize um novo pacote Node.js utilizando o `npm`. Em seguida, instale as ferramentas `mocha` e `chai` que iremos usar em nosso projeto.

```bash
mkdir cacau-trybe
cd cacau-trybe
npm init -y
npm install mocha@8.4.0 chai@4.3.4 --save-dev --save-exact
```

> Agora, você também já pode usar o comando `code .` e continuar direto pelo VS Code 🤟

Feito isso, vamos organizar nosso projeto criando as pastas `src` e `tests` e, dentro da última, outra subpasta chamada `integration`.

De olho na dica👀: Essa organização vai facilitar o desenvolvimento quando houver diferentes tipos de teste em seu projeto.

Começaremos os testes com foco na validação do primeiro contrato (lista de chocolates cadastrados). Para isso, vamos construir um teste que valida a requisição `GET` para a rota `/chocolates`.

> Esse teste vai presumir a existência de todas as funções necessárias para receber nossa requisição, realizar consultas internas e retornar a lista com chocolates.

Para isso, crie dentro da pasta `integration` um arquivo chamado `chocolates.test.js`.

```bash
.
├── src
├── tests/
│   └── integration/
│       └── chocolates.test.js
└── package.json
```

De olho na dica👀: O `.test`, no nome do arquivo, não é obrigatório, mas é visto como uma boa prática pela comunidade de desenvolvimento de software.

Além da organização das pastas, também podemos deixar o script de teste configurado no `package.json`.

> Essa configuração irá facilitar a execução dos testes, uma vez que será possível executar todos os testes usando apenas `npm run test` ou simplesmente `npm test`.

Veja a configuração:

> package.json

```json
    "scripts": {
    "test": "mocha tests/**/*.test.js --exit"
  },
```

Veja que usamos uma flag (parâmetro) `--exit` ao final do script. Esse parâmetro vai impedir que os testes fiquem executando indefinidamente quando houver erros em funções assíncronas.

> Caso você queira saber um pouco mais sobre esse parâmetro, acesse a [discussão](https://github.com/mochajs/mocha/issues/2879) sobre ele no repositório do Mocha.

Agora, considerando **a definição do contrato** (aquilo que é esperado no consumo da API), podemos **transformá-lo em teste convertendo-o para um cenário com asserções/afirmações**. Assim como fizemos anteriormente com o `mocha` e o `chai`.

```js
// tests/integration/chocolates.test.js

const chai = require('chai');

const { expect } = chai;

describe('Usando o método GET em /chocolates', function () {
    it('Retorna a lista completa de chocolates!', async function () {
        response = await minhaRequisicao();
        expect(response.status).to.be.equal(200);
    });
});
```

Aqui, temos uma boa definição de asserções para começarmos, mas que deve falhar, pois além de não existirem funcionalidades da nossa API, `minhaRequisicao()` é um **placeholder (está só de enfeite)** sem funcionalidade. Com isso, precisamos de algum recurso que nos ajude na validação à medida que formos construindo a API.

⚠️ Aviso: Para nos ajudar com esse desafio, utilizaremos o plugin [Chai HTTP](https://www.chaijs.com/plugins/chai-http/)! Com ele poderemos simular uma request a nossa API **sem inicializá-la manualmente**.

Primeiro, precisamos instalar esse novo pacote, para isso, execute:

```bash
npm install chai-http@4.3.0 --save-dev --save-exact
```

E então, no nosso teste, iremos adicionar o seguinte trecho, com o plugin na instância do chai:

```js
// tests/integration/chocolates.test.js

// const chai = require('chai');
const chaiHttp = require('chai-http');

chai.use(chaiHttp);

// const { expect } = chai;

// ...
```

Após adicionar o plugin ao chai, poderemos consumir o server em `express` por meio dele, sem que haja a necessidade de subirmos a API manualmente.

> Em outras palavras, o `chai-http` vai criar seu próprio `listen()`, escolher uma porta automaticamente, fazer a requisição ao _endpoint_ e, por último, retornar o resultado dessa requisição.

Abaixo temos um diagrama ilustrando este processo:

![Diagrama do funcionamento do chai-http](https://content-assets.betrybe.com/prod/e2fc2a08-ac07-4cc6-bfcb-8ec2b8ffb79b-Diagrama%20do%20funcionamento%20do%20chai-http.png)


```js
// tests/integration/chocolates.test.js

const chai = require('chai');
const chaiHttp = require('chai-http');

const { expect } = chai;

chai.use(chaiHttp);

describe('Usando o método GET em /chocolates', function () {
    it('Retorna a lista completa de chocolates!', async function () {
        const response = await chai
            .request(app)
            .get('/chocolates');
    });
});
```

Aqui, utilizamos o método `request`, que foi adicionado ao `chai` por meio do plugin. Por tanto, ele nos permite chamar diretamente nossos _endpoints_, simulando chamadas HTTP.

⚠️ Aviso: Internamente, esse método já se encarrega de acessar a API e percorrer o pipeline daquele _endpoint_ no Express, até conseguir os dados da resposta.

Voltando ao cenário de teste, nós ainda precisamos especificar a saída esperada para esse teste. Para isso, vamos recordar o contrato estabelecido para a rota `/chocolates`:

👉 **GET** _`/chocolates`_

-   Objetivo: Retornar uma lista com todos os chocolates cadastrados.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):

```json
  [
    { "id": 1, "name": "Mint Intense", "brandId": 1 },
    { "id": 2, "name": "White Coconut", "brandId": 1 },
    { "id": 3, "name": "Mon Chéri", "brandId": 2 },
    { "id": 4, "name": "Mounds", "brandId": 3 }
  ]
```

Nós iremos dividir a validação desse contrato em duas partes usando o `expect`.

-   Na primeira parte, iremos verificar se o código HTTP retornado corresponde ao valor esperado:

```js
 expect(response.status).to.be.equals(200);
```

Em seguida, validamos se o corpo da mensagem corresponde a lista com todos os chocolates cadastrados na API:

```js
const output = [
  { id: 1, name: 'Mint Intense', brandId: 1 },
  { id: 2, name: 'White Coconut', brandId: 1 },
  { id: 3, name: 'Mon Chéri', brandId: 2 },
  { id: 4, name: 'Mounds', brandId: 3 },
];
expect(response.body.chocolates).to.deep.equal(output);
```

Você pode estar se perguntando: “Por que utilizamos o comando `to.deep.equal` ao invés do `to.be.equals`?” 🤔

Resposta: Nesse caso, precisamos utilizar o `deep` para garantir que todas as informações dentro do objeto retornado são as mesmas do objeto esperado. Do outro modo, essa validação não seria possível, pois não seria realizada a comparação em **profundidade**.

```js
// tests/integration/chocolates.test.js

const chai = require('chai');
const chaiHttp = require('chai-http');

const { expect } = chai;

chai.use(chaiHttp);

describe('Testando a API Cacau Trybe', function () {
  describe('Usando o método GET em /chocolates', function () {
    it('Retorna a lista completa de chocolates!', async function () {
      const output = [
        { id: 1, name: 'Mint Intense', brandId: 1 },
        { id: 2, name: 'White Coconut', brandId: 1 },
        { id: 3, name: 'Mon Chéri', brandId: 2 },
        { id: 4, name: 'Mounds', brandId: 3 },
      ];

      const response = await chai
        .request(app)
        .get('/chocolates');
      expect(response.status).to.be.equal(200);
      expect(response.body.chocolates).to.deep.equal(output);
    });
  });
});
```

Agora, você já pode executar esse teste com o comando `npm test`.

👻

Porém, esse teste irá falhar conforme podemos observar na imagem abaixo:

![Mensagem de erro nos testes 1](https://content-assets.betrybe.com/prod/e2fc2a08-ac07-4cc6-bfcb-8ec2b8ffb79b-Mensagem%20de%20erro%20nos%20testes%201.png)

Falha de execução no Teste

⚠️ Aviso: Não se preocupe com essa falha, ela é exatamente o que precisávamos para começar a construção da nossa API.

O erro identificado foi causado pela falta de definição do `app`, ou seja, a API ainda não foi construída e, consequentemente, não foi importada. Sendo assim, precisaremos construir nossas funcionalidades até que o teste seja executado com sucesso.

Continuando do episódio anterior de Projeto Missions, faremos a construção de testes de integração, uma habilidade que eleva muito o sucesso do projeto.


# Construindo a API

![Building app](https://content-assets.betrybe.com/prod/4242be65-52f7-4aaa-a639-8e4aa164a135-Building%20app.gif)

Bora construir testes!

Para começarmos o desenvolvimento das funcionalidades, precisaremos criar um arquivo para a API chamado `app.js` dentro da pasta `src`.

```bash
.
├── src/
│   └── app.js
├── tests/
│   └── integration/
│       └── chocolates.test.js
└── package.json
```

Em seguida, iremos instalar o `Express` para viabilizar a definição das rotas da aplicação.

```bash
npm install express@4.17.1 --save-exact
```

⚠️ Aviso: Veja que durante o desenvolvimento com TDD, os módulos estão sendo instalados sob demanda. Essa prática deve evitar o uso desnecessário de módulos que não são importantes para o funcionamento da API.

De olho na dica 👀: Outra boa prática, para construir a API, é fazer a separação (I) **do conjunto da definição das rotas** _(No arquivo `app.js`, por exemplo, que será consumido pelo `chaiHttp`)_, (II) do **servidor propriamente dito, que consome essas regras** _(Esse continuaria em `server.js`, para utilizarmos em contextos de não-teste)_:

```js
// src/app.js

const express = require('express');

const app = express();

app.get('/chocolates', async (req, res) => {
  const chocolates = await cacauTrybe.getAllChocolates();
  res.status(200).json({ chocolates });
});

module.exports = app;
```

Em posse do novo arquivo, podemos importar as rotas no arquivo de teste e, em seguida, verificar novamente se o teste será executado com sucesso.

```js
// tests/integration/chocolates.test.js

//const chai = require('chai');
//const chaiHttp = require('chai-http');
const app = require('../../src/app');

//const { expect } = chai;
//...
```

**Mas, adivinhe quem falhou novamente?** 👀

![Falha de execucao no Teste-construindo-a-api-2](https://content-assets.betrybe.com/prod/4242be65-52f7-4aaa-a639-8e4aa164a135-Falha%20de%20execucao%20no%20Teste-construindo-a-api-2.png)

Falha de execução no Teste

⚠️ Aviso: Quando um teste falha no TDD, precisamos construir/refatorar nosso código, mas também significa que estamos indo pelo caminho certo.

O erro encontrado está associado ao tempo de espera pela requisição, ou seja, o pedido chegou ao _endpoint_ mas demorou tanto para ser atendido que o nosso teste não teve paciência de esperar.

> Na verdade, a resposta jamais chegaria, pois nós não construímos a função `getAllChocolates()` definida na rota `GET /chocolates`. Além disso, ainda não existe nenhuma lista de chocolates na Cacau Trybe. 😱 🍫

Bora fazer isso?

> Primeiramente, iremos definir um arquivo para armazenar todas as informações sobre os chocolates da Cacau Trybe. Para isso, crie uma pasta com o nome `files` dentro da pasta `src` e, em seguida, crie o arquivo com o nome `cacauTrybeFile.json` com as seguintes informações:

Veja como:

> src/files/cacauTrybeFile.json

```json
{
    "brands": [
        {
            "id": 1,
            "name": "Lindt & Sprungli"
        },
        {
            "id": 2,
            "name": "Ferrero"
        },
        {
            "id": 3,
            "name": "Ghirardelli"
        }
    ],
    "chocolates": [
        {
            "id": 1,
            "name": "Mint Intense",
            "brandId": 1
        },
        {
            "id": 2,
            "name": "White Coconut",
            "brandId": 1
        },
        {
            "id": 3,
            "name": "Mon Chéri",
            "brandId": 2
        },
        {
            "id": 4,
            "name": "Mounds",
            "brandId": 3
        }
    ]
}
```

Para acessar a lista de chocolates, também precisaremos das funções que irão ler o arquivo JSON e definir filtros de dados de acordo com os contratos da nossa API.

Essas funções serão definidas em um arquivo chamado `cacauTrybe.js` dentro da pasta `src`.

```bash
.
├── src/
│   ├── files/
│   │   └── cacauTrybeFile.json
│   ├── app.js
│   └── cacauTrybe.js
├── tests/
│   └── integration/
│       └── chocolates.test.js
└── package.json
```


```js
// src/cacauTrybe.js

const fs = require('fs').promises;
const { join } = require('path');

const readCacauTrybeFile = async () => {
  const path = '/files/cacauTrybeFile.json';
  try {
    const contentFile = await fs.readFile(join(__dirname, path), 'utf-8');
    return JSON.parse(contentFile);
  } catch (error) {
    return null;
  }
};

const getAllChocolates = async () => {
  const cacauTrybe = await readCacauTrybeFile();
  return cacauTrybe.chocolates;
};

module.exports = {
    getAllChocolates,
};
```

> Veja que a função `getAllChocolates()`, depende da leitura do arquivo `CacauTrybeFile.json` para retornar a lista de chocolates.

Contudo, a leitura desse arquivo também será necessária para as demais rotas. Portanto, já definimos a função `readCacauTrybeFile()` como sendo a responsável por acessar o arquivo de chocolates, independentemente da rota.

Feito isso, também precisaremos importar o arquivo `cacauTrybe.js` no arquivo de rotas para acessar as suas funções.

```js
// src/app.js

//const express = require('express');
const cacauTrybe = require('./cacauTrybe');

//const app = express();
//...
```

Pronto, agora chegou o momento tão esperado de torcermos para que, desta vez, o nosso teste seja executado com sucesso. 🤞

Vamos lá? 1..2..3 e?

![Teste executado com sucesso 3](https://content-assets.betrybe.com/prod/4242be65-52f7-4aaa-a639-8e4aa164a135-Teste%20executado%20com%20sucesso%203.png)

Teste executado com sucesso.

Enfim, conseguimos alcançar nosso objetivo. 🎉

Vamos relembrar um pouco sobre o que fizemos até aqui?

-   Empregando o TDD, focamos inicialmente nos contratos da API para entender quais os cenários de teste precisavam ser construídos.
    
-   Em seguida, executamos os testes, já presumindo as falhas, para guiar as etapas do desenvolvimento.
    

> Perceba que com isso, conseguimos olhar para o problema de uma forma mais direcionada, atacando problemas menores e diminuindo o grau de dificuldade no desenvolvimento.

Esse é um dos principais benefícios do TDD que nos permite alcançar grandes problemas com passos de bebê (_baby steps_).

![Baby steps](https://content-assets.betrybe.com/prod/4242be65-52f7-4aaa-a639-8e4aa164a135-Baby%20steps.gif)

Baby steps!

⚠️ Aviso: Embora o sucesso no teste seja um bom sinal para o desenvolvimento, isso não significa que não podemos melhorar ainda mais o nosso código e testes. Este é, inclusive, o comportamento esperado para o desenvolvimento com o TDD.

**⏰ Hora da reflexão**: imagine que por algum motivo, externo a nossa aplicação, o arquivo `CacauTrybeFile.json` seja corrompido ou deletado. Consequentemente, nossos testes, que antes executavam com sucesso, começam a falhar. O que podemos fazer nesse caso? 🤔

Resposta: O ideal é não permitir que nosso código realize operações de IO de fato, mas apenas simular que elas estão sendo realizadas. Dessa forma, garantimos que um banco de dados inconsistente ou um arquivo faltando na hora de executar os testes não faça com que tudo vá por água abaixo.

> Para isso existe o conceito de `Test Doubles` ou, numa tradução livre, Dublês de Testes (remetendo aos dublês de filmes).

Com esses dublês, podemos simular, por exemplo, as funções do módulo `fs`. Nosso código vai pensar que está chamando as funções do `fs`, porém estará chamando as nossas funções, que se comportarão da maneira que queremos, mas sem a necessidade de escrever, ler ou ter dependência de arquivo reais.

Para nos ajudar com esse tipo de problema, veremos a seguir como criar e usar os dublês de teste.

# Dublês de teste

Retomando o problema do arquivo `CacauTrybeFile.json`, vamos ver na prática como podemos criar um dublê para a função de leitura do `fs`.

⚠️ Aviso: Vale ressaltar que o dublê de teste não se restringe a funções específicas, como a leitura com o `fs`. O que precisamos ter em mente, ao definir um dublê, é o motivo pelo qual estamos isolando essa função.

Neste nosso caso, o motivo racional é que o gerenciamento dos arquivos ultrapassa o escopo de nossa aplicação.

Para nos ajudar na criação e utilização dos dublês, utilizaremos a ferramenta [Sinon](https://sinonjs.org/), a qual fornece funções para diversos tipos dos **`Test Doubles`**.

No momento, focaremos em um tipo de Test Double, o `stub`.

> **Stubs são objetos que podemos utilizar para simular interações com dependências externas ao que estamos testando de fato**.

Primeiro, vamos fazer a instalação do Sinon:

```bash
npm install sinon@11.1.1 --save-dev --save-exact
```

Agora, vamos ver na prática como podemos criar um `stub` para a função `readFile()` do `fs`:


```js
// tests/integration/chocolates.test.js

//const chai = require('chai');
//const chaiHttp = require('chai-http');
const sinon = require('sinon');
const fs = require('fs');

//const app = require('../../src/app');

//const { expect } = chai;

//chai.use(chaiHttp);

const mockFile = JSON.stringify({ 
  brands: [
    {
      id: 1,
      name: 'Lindt & Sprungli',
    },
    {
      id: 2,
      name: 'Ferrero',
    },
    {
      id: 3,
      name: 'Ghirardelli',
    },
  ],
  chocolates: [
    {
      id: 1,
      name: 'Mint Intense',
      brandId: 1,
    },
    {
      id: 2,
      name: 'White Coconut',
      brandId: 1,
    },
    {
      id: 3,
      name: 'Mon Chéri',
      brandId: 2,
    },
    {
      id: 4,
      name: 'Mounds',
      brandId: 3,
    },
  ],
});

//describe('Testando a API Cacau Trybe', function () {
      sinon.stub(fs.promises, 'readFile')
        .resolves(mockFile);
//describe('Usando o método GET em /chocolates', function () {
  //it('Retorna a lista completa de chocolates!', async function () {

//...

```

Perceba que precisamos importar o módulo `fs` e, então, usamos o `sinon` para criar um stub que será utilizado na função `readFile()`. Essa retornará o `mockFile` contendo todo os dados que estavam no arquivo `CacauTrybeFile.json`, conforme especificamos na chamada para `resolves`.

Veja também que usamos o `JSON.stringify()` para transformar os dados em JSON, no mesmo formato em que a função `readFile` retornaria o arquivo JSON.

> O `stub` irá interceptar, durante o teste, todas as chamadas a função `readFile()`, portanto, é imprescindível que os valores passados em `resolves` sejam do mesmo tipo que a função original.
> 
> Vamos testar nosso dublê?

Para isso, renomeie o arquivo `CacauTrybeFile.json` para `corruptedFile.json`.

> Essa mudança, sem o dublê de teste, deveria ocasionar uma falha, concorda?

Agora, execute o teste novamente e veja o resultado:

![Execucao do Teste com sucesso usando Stub 4](https://content-assets.betrybe.com/prod/0fd9032c-6d17-4354-acfe-48a6809cc3f5-Execucao%20do%20Teste%20com%20sucesso%20usando%20Stub%204.png)

Execução do Teste com sucesso usando Stub.

Você pode estar se perguntando: “Mas o que aconteceria se existisse outro arquivo com valores diferentes?” 🤔

Resposta: Se a leitura do novo arquivo fosse realizada dentro do mesmo escopo em que o `stub` foi definido, o valor retornado para o novo arquivo seria o mesmo do primeiro arquivo, resultando, provavelmente, em uma falha do teste. Sendo assim, o ideal é **sempre criarmos Tests Doubles para o escopo de cada cenário de teste.**

De olho na dica👀: O `mocha` nos fornece duas funções chamadas **`beforeEach`** e **`afterEach`**. Como o nome diz, são funções que serão executadas “antes” e “depois” de cada teste:

```js
// tests/integration/chocolates.test.js

// const chai = require('chai');
// const sinon = require('sinon');
// const fs = require('fs');
// const chaiHttp = require('chai-http');
// const app = require('../../src/app');

// const { expect } = chai;

// chai.use(chaiHttp);

// const mockFile = JSON.stringify({
//   ...

describe('Testando a API Cacau Trybe', function () {
  beforeEach(function () {
    sinon.stub(fs.promises, 'readFile')
      .resolves(mockFile);
  });

  afterEach(function () {
    sinon.restore();
  });

  describe('Usando o método GET em /chocolates', function () {
    it('Retorna a lista completa de chocolates!', async function () {
      const output = [
        { id: 1, name: 'Mint Intense', brandId: 1 },
        { id: 2, name: 'White Coconut', brandId: 1 },
        { id: 3, name: 'Mon Chéri', brandId: 2 },
        { id: 4, name: 'Mounds', brandId: 3 },
      ];

      const response = await chai
        .request(app)
        .get('/chocolates');
      expect(response.status).to.be.equal(200);
      expect(response.body.chocolates).to.deep.equal(output);
    });
  });
});
```

Perceba que **antes** do cenário de teste, nós alteramos o comportamento do método do fs criando um stub e, depois da execução do teste, utilizamos a função restore() que o sinon atribui aos stubs para retornarmos o comportamento padrão daquela função.

Anota aí 🖊: A função `restore()` desempenha um papel muito importante quando utilizamos stubs, pois é ela que vai garantir que o stub de um teste não seja replicado para os testes seguintes.

# Finalizando a API

Agora que já conhecemos as metodologias e ferramentas necessárias para o desenvolvimento da nossa API, iremos dar continuidade ao desenvolvimento, observando os demais contratos da nossa API.

Mas primeiro, vamos recapitular quais são eles:

👉 **GET** _`/chocolates/:id`_

-   Objetivo: Buscar um chocolate específico pelo ID.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):

```json
    {
      "id": 4,
      "name": "Mounds",
      "brandId": 3
    }
```

👉 **GET** _`/chocolates/brand/:brandId`_

-   Objetivo: Buscar uma lista de chocolates pelo ID (brandId) da marca.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):

```json
[
  {
      "id": 1,
      "name": "Mint Intense",
      "brandId": 1
  },
  {
      "id": 2,
      "name": "White Coconut",
      "brandId": 1
  }
]
```

Assim como antes, começaremos pela definição dos cenários de teste para cada um dos contratos:

```js
// tests/integration/chocolates.test.js

//describe('Testando a API Cacau Trybe', function () {

//...

describe('Usando o método GET em /chocolates/:id para buscar o ID 4', function () {
    it('Retorna o chocolate Mounds', async function () {
      const response = await chai
        .request(app)
        .get('/chocolates/4');

      expect(response.status).to.be.equal(200);
      expect(response.body.chocolate).to.deep.equal(
        {
          id: 4,
          name: 'Mounds',
          brandId: 3,
        });
    });
  });

  describe('Usando o método GET em /chocolates/:id para buscar o ID 99', function () {
    it('Retorna status 404 com a mensagem "Chocolate not found"', async function () {
      const response = await chai
        .request(app)
        .get('/chocolates/99');

      expect(response.status).to.be.equal(404);
      expect(response.body).to.deep.equal({ message: 'Chocolate not found' })
    });
  });

  describe('Usando o método GET em /chocolates/brand/:brandId para buscar brandId 1', function () {
    it('Retorna os chocolates da marca Lindt & Sprungli', async function () {
      const response = await chai
        .request(app)
        .get('/chocolates/brand/1');

      expect(response.status).to.be.equal(200);
      expect(response.body.chocolates).to.deep.equal([
        {
          id: 1,
          name: 'Mint Intense',
          brandId: 1,
        },
        {
          id: 2,
          name: 'White Coconut',
          brandId: 1,
        },
      ]);
    });
  });
//});
```

Seguindo ao ciclo do TDD, iremos executar nossos testes já presumindo a falha dos novos cenários. Para isso, execute o comando `npm test`.

![Falha de execucao no Teste 5](https://content-assets.betrybe.com/prod/c7e37376-db25-4064-8b32-9d3fcc165a43-Falha%20de%20execucao%20no%20Teste%205.png)

Falha de execução no Teste

Conforme esperado, os três últimos cenários falharam e a nossa meta é refatorar nosso código até que todos esses testes executem com sucesso.

Vamos nessa? 💪

Primeiro, iremos construir as rotas para cada cenário de teste:

Copiar

```js
// src/app.js

//const express = require('express');
//const cacauTrybe = require('./cacauTrybe');

//const app = express();

//app.get('/chocolates', async (req, res) => {
//  const chocolates = await cacauTrybe.getAllChocolates();
//  res.status(200).json({ chocolates });
//});

app.get('/chocolates/:id', async (req, res) => {
  const { id } = req.params;
  // Usamos o Number para converter o id em um inteiro
  const chocolate = await cacauTrybe.getChocolateById(Number(id));
  if (!chocolate) return res.status(404).json({ message: 'Chocolate not found' });
  res.status(200).json({ chocolate });
});

app.get('/chocolates/brand/:brandId', async (req, res) => {
  const { brandId } = req.params;
  const chocolates = await cacauTrybe.getChocolatesByBrand(Number(brandId));
  res.status(200).json({ chocolates });
});

//module.exports = app;
```

Em seguida, iremos definir as funções que irão filtrar as respostas conforme esperado para cada uma das rotas:

Copiar

```js
// src/cacauTrybe.js

//const fs = require('fs').promises;
//const { join } = require('path');

//const readCacauTrybeFile = async () => {
//  const path = '/files/cacauTrybeFile.json';
//  try {
//    const contentFile = await fs.readFile(join(__dirname, path), 'utf-8');
//    return JSON.parse(contentFile);
//  } catch (error) {
//    return null;
//  }
//};

//const getAllChocolates = async () {
//  const cacauTrybe = await readCacauTrybeFile();
//  return cacauTrybe.chocolates;
//};

const getChocolateById = async (id) => {
  const cacauTrybe = await readCacauTrybeFile();
  return cacauTrybe.chocolates
    .find((chocolate) => chocolate.id === id);
};

const getChocolatesByBrand = async (brandId) => {
  const cacauTrybe = await readCacauTrybeFile();
  return cacauTrybe.chocolates
    .filter((chocolate) => chocolate.brandId === brandId);
};

//module.exports = {
//  getAllChocolates,
  getChocolateById,
  getChocolatesByBrand,
//};
```

Novamente, chegamos naquele momento de extrema importância do desenvolvimento, o qual precisamos torcer para que tudo aconteça conforme esperado.🤞

> Execute o teste usando o comando `npm test`.

![Execucao dos testes com sucesso 6](https://content-assets.betrybe.com/prod/c7e37376-db25-4064-8b32-9d3fcc165a43-Execucao%20dos%20testes%20com%20sucesso%206.png)

Execução dos testes com sucesso.

![Parabens](https://content-assets.betrybe.com/prod/Parabens.gif)

Parabéns!

#### Recursos adicionais

-   [Artigo (em português): Test Doubles (Mocks, Stubs, Fakes, Spies e Dummies)](https://medium.com/rd-shipit/test-doubles-mocks-stubs-fakes-spies-e-dummies-a5cdafcd0daf)
-   [Vídeo: TDD (Test Driven Development) // Dicionário do Programador](https://www.youtube.com/watch?v=bLdEypr2e-8)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4684c963-8015-41ad-a901-eb37076d9ff5/lesson/45b8e257-cf4a-4bf9-8d4a-fdfce0a5837e)