[[Node]]
[[Node - 14 Middlewares]]

É comum você precisar reaproveitar um middleware para todas as rotas da sua aplicação (ou para uma boa parte delas). Nesses casos, você pode configurar o app para passar todas as requisições por um middleware. Por exemplo, imagine um middleware chamado `apiCredentials`. Nós já vamos escrever esse middleware, mas primeiro imagine a função neste momento. A função apenas confere se a requisição enviou um token para autorizar o uso da sua API. A configuração `app.use(apiCredentials)` seria adicionada logo no começo do nosso arquivo. Ela ficaria assim:


```js
//...
const app = express();
const teams = { ... };

app.use(apiCredentials);
app.use(express.json());

app.get('/teams', (req, res) => res.json(teams));
// ...
```

Aqui é importante destacar que o `app.use` só afeta as rotas que vem abaixo da sua definição. Ou seja, **todas as rotas da API de times vão passar pelo middleware de autenticação**. Se você deseja liberar a rota `GET /teams` para todos, mas exigir credenciais para as demais rotas, precisa mudar a ordem dessa configuração. Veja como fazer isso no exemplo abaixo:

```js
//...
const app = express();
const teams = { ... };

app.use(express.json());
// não precisa passar pelo apiCredentials pra chegar aqui
app.get('/teams', (req, res) => res.json(teams));
// se chegou até aqui, então vai passar pelo apiCredentials
app.use(apiCredentials); 
// só vai chegar aqui se tiver credenciais
app.post('/teams', ...);
app.put('/teams', ...);
// ...
```

## Usando middlewares assíncronos

Ok, você já aprendeu como configurar um middleware _global_, ou seja, que intercepta todas ou quase todas as rotas. Agora, veja como você implementaria esse middleware nas próximas explicações.

Suponha que você tem um arquivo `authdata.json` com um objeto mapeando tokens com as informações dos apps que usam nossa API. Quando uma requisição chega, ela precisa ter um cabeçalho `X-API-TOKEN` com um token presente nesse arquivo. Se não tiver o cabeçalho ou se não tiver um token válido, vamos responder com o código http `401 Unauthorized`.

O arquivo `authdata.json` ficaria **fora do diretório src/** e seria assim:

```json
{
  "dGlqb2xvMjIK": { "appId": 1, "teams": ["SAO", "PAL"] },
  "bDRkcjFsaDAK": { "appId": 2, "teams": ["FLA", "FLU"] }
}
```

Vamos escrever esse middleware em um arquivo separado em `src/middlewares/apiCredentials.js`:

```js
// src/middlewares/apiCredentials.js

const fs = require('fs/promises');

// como vamos ler arquivos assincronamente, precisamos do async
module.exports = async function apiCredentials(req, res, next) {
  // pega o token do cabeçalho, se houver
  const token = req.header('X-API-TOKEN');
  // lê o conteúdo do `./authdata.json` (relativo à raiz do projeto)
  const authdata = await fs.readFile('./authdata.json', { encoding: 'utf-8' });
  // readFile nos deu uma string, agora vamos carregar um objeto a partir dela
  const authorized = JSON.parse(authdata);

  if (token in authorized) {
    next(); // pode continuar
  } else {
    res.sendStatus(401); // não autorizado
  }
};
```

Repare que no uso do método `req.header()` para acessar um cabeçalho, estamos usando `req.header('X-API-TOKEN')` porque o cabeçalho (_header_) usado é o `X-API-TOKEN`. O protocolo HTTP tem cabeçalhos já estabelecidos, mas é costume prefixar cabeçalhos customizados com `X-`, como fizemos com `X-API-TOKEN`.

Agora vamos voltar e usar o middleware no nosso app:

Copiar

```js
// src/app.js

const app = express();
const apiCredentials = require('./middlewares/apiCredentials');
//...
app.use(express.json());
app.use(apiCredentials); 

app.get('/teams', (req, res) => res.json(teams));
app.post('/teams', ...);
app.put('/teams', ...);
// ...
```

Muito bom, nosso middleware está funcionando sem problemas! Veja abaixo um caso de sucesso:

![Requisição GET teams com token da API sendo aceita](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20GET%20teams%20com%20token%20da%20API%20sendo%20aceita.gif)

Requisição GET /teams com token da API sendo aceita

Agora, veja a requisição abaixo sendo rejeitada:

![Requisição GET teams com token da API sendo rejeitada](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20GET%20teams%20com%20token%20da%20API%20sendo%20rejeitada.gif)

Requisição GET /teams com token da API sendo rejeitada

Com isso, você conseguiu mais uma habilidade: empregar middlewares assíncronos no express! Legal demais, né? 🚀

## Lidando com erros assíncronos

Por padrão, o Express vai encaminhar todos os erros lançados para serem tratados pelos **middlewares de erros**. No entanto, erros lançados em middlewares assíncronos não são tratados do mesmo jeito.

Por exemplo, se por acaso o arquivo `authdata.json` não estivesse disponível no momento da requisição, ou tivesse um JSON quebrado, você obteria um erro, mas não teria uma resposta HTTP.

Veja esse problema na imagem abaixo:

![Requisição GET teams sem resposta por erro do servidor](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20GET%20teams%20sem%20resposta%20por%20erro%20do%20servidor.gif)

Requisição GET /teams sem resposta por erro do servidor

Existem algumas soluções para este problema, mas a mais simples está em um pacote chamado `express-async-errors`. Basta instalar com `npm install express-async-errors@3.1.1 --save-dev --save-exact`, importar ele no arquivo `app.js` antes de criar o objeto `app` e esse pacote vai alterar o comportamento padrão do express. Ficaria assim:

```js
const express = require('express');
require('express-async-errors'); // não precisa definir uma variável

const apiCredentials = require('./middlewares/apiCredentials');

const app = express();
// ...
```

Veja abaixo a resposta HTTP com o erro:

![Requisição GET teams recebendo resposta com erro 500](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20GET%20teams%20recebendo%20resposta%20com%20erro%20500.gif)
Requisição GET /teams recebendo resposta com erro 500


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/7c6ef235-b4b5-41d3-85c4-54b53169c15f)