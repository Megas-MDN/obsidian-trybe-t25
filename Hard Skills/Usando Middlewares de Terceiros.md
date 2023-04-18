[[Node - 14 Middlewares]]
[[Node]]

Existem middlewares escritos por terceiros que nos fornecem ferramentas úteis para o desenvolvimento de nossas aplicações. Vamos conhecer mais de perto alguns middlewares e como eles nos ajudam a resolver situações específicas na aplicação! 🚀

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico.

## Interpretando conteúdo JSON com `express.json`

Um middleware bastante utilizado é o `express.json`, ele é um middleware que lê o conteúdo da requisição HTTP, interpreta os conteúdos como JSON e cria no objeto `req` uma propriedade `body` com o valor encontrado no conteúdo.

A função `express.json()` utilizada na linha `app.use(express.json())` cria um middleware que processa corpos de requisições escritos em JSON. Se executarmos nossa API e fizermos uma requisição do tipo POST, conseguiremos ter acesso aos valores enviados no body da requisição. Porém, se tirarmos o uso deste middleware, você perceberá que as requisições do tipo POST não conseguem processar os dados enviados no body da requisição.

**Faça o teste:** copie o script abaixo, cole-o em um arquivo chamado `src/experimento-json.js` e execute-o com o comando `node src/experimento-json.js`. Em seguida, realize a request `POST localhost:3000/hello`, passando o JSON `{ "nome": "<seu nome aqui">" }`.

Copiar

```js
// src/experimento-json.js

const express = require('express');
const app = express();

app.post('/fail', (req, res) => {
  res.status(200).json({ greeting: `Hello, ${req.body.nome}!` });
});

app.use(express.json());

app.post('/hello', (req, res) => {
  // req.body agora está disponível
  res.status(200).json({ greeting: `Hello, ${req.body.nome}!` });
});

app.listen(3000, () => { console.log('Ouvindo na porta 3000'); });
```

> 💡 Experimente agora realizar a request `POST localhost:3000/fail`, passando o JSON `{ "nome": "<seu nome aqui">" }`. Perceba que, sem o `express.json`, req.body fica `undefined` e você verá um erro.

## Servindo arquivos estáticos com `express.static`

Um outro middleware que já vem com o Express é o `express.static`. Ele pega o `req.path` e usa para procurar um arquivo. Se encontrado, ele já responde com esse arquivo. Se não, ele assume que alguém vai responder essa requisição e simplesmente passa para o próximo.

Configurar esse middleware é simples:

```js
// src/app.js

//...
const app = express();
// configura para procurar o path no diretório ./images
app.use(express.static('./images'));
//....
```

Com essa configuração, uma requisição `GET /brasao/COR.png` vai passar primeiro pelo `express.static`, que procura por um arquivo em `./images/brasao/COR.png` e vai enviá-lo se ele for encontrado. Experimente baixar o brasão do Corinthians e colocá-lo nesse diretório para testar!

## Gerando logs da aplicação com `morgan`

Um _log_ nada mais é do que **um registro organizado e consistente de todas as ocorrências de um evento**. Logs são fundamentais para reconhecer bugs em uma aplicação web, dando visibilidade para a frequência e as condições em que os bugs ocorreram. E como você nunca sabe quando um bug vai acontecer, é conveniente ter um log de _todas_ as requisições recebidas.

Você pode escrever seu próprio middleware usando `console.log`. Apenas lembre-se que **o `console.log` vai imprimir no terminal que executa seu app, não nas respostas enviadas aos clientes**.

```js
app.use((req, _res, next) => {
  console.log('req.method:', req.method);
  console.log('req.path:', req.path);
  console.log('req.params:', req.params);
  console.log('req.query:', req.query);
  console.log('req.headers:', req.headers);
  console.log('req.body:', req.body);
  next();
});
```

A comunidade open-source tem um pacote muito conveniente para esse fim chamado [morgan](https://www.npmjs.com/package/morgan). Depois de instalar com `npm install morgan@1.10.0 --save-exact`, basta configurar esse middleware e ele vai emitir uma mensagem para cada requisição recebida:

```js
// src/app.js

const express = require('express');
require('express-async-errors');
const morgan = require('morgan');
//...
const app = express();
app.use(morgan('dev'));
app.use(express.static('./images'));
```

![Logs do morgan no terminal](https://content-assets.betrybe.com/prod/Logs%20do%20morgan%20no%20terminal.png)

Logs do morgan no terminal

## Liberando acesso ao frontend com `cors`

Outro middleware bem comum nas aplicações back-end é o **cors**, que permite que outras aplicações front-end consumam sua API. O uso básico desse módulo consiste em instalá-lo usando `npm install cors@2.8.5 --save-exact` e em seguida adicionar as seguintes linhas no seu código:

```js
const cors = require('cors');
app.use(cors());
```

Quando uma aplicação frontend é carregada em um endereço (`localhost:3000`) e tenta acessar uma API em outro endereço (`localhost:3001`), o navegador primeiro perguntará à API se essa aplicação pode fazer essas requisições. Esse é um recurso de segurança presente em todos os navegadores modernos. Antes de existir CORS, os navegadores simplesmente não enviavam requisições de aplicações para outros endereços.

Com o `cors` configurado, nosso back-end vai deixar o navegador enviar requisições para nossa API. Sem o `cors`, o navegador bloquearia as _requests_ do nosso front-end para nossa API. **O middleware `cors` tem um conjunto de configurações que permitem criar regras específicas, limitando quem pode fazer requisições e quais requisições podem ser feitas.**

Por enquanto, você não precisa se preocupar com isso, já que está focando no desenvolvimento do back-end. Um ambiente de produção, no entanto, _exigiria_ essa configuração para permitir a integração com o frontend. Quando essa hora chegar, [leia a documentação](https://www.npmjs.com/package/cors).


## Retornando 404 com um middleware global customizado

Às vezes uma rota simplesmente não existe. Uma requisição `GET /players` vai passar por todos os middlewares em ordem. O `express.static` não vai ver esse arquivo e vai passar pro próximo middleware. O `express.json` nunca responde, só tenta ler o `req.body` _se houver_. O `apiCredentials` não vai reclamar se houver um token válido, passando para o próximo middleware. No entanto, agora as rotas são específicas e ninguém responde ao `GET /players`.

Nesse caso, o Express já vem com um **middleware de erro** pronto para lidar com a maior parte dos casos comuns. Foi esse middleware que respondeu todos os erros que você experimentou hoje. Por padrão, ele responde com HTML para qualquer erro. No entanto, se você quiser customizar sua resposta para rotas não tratadas, basta escrever um middleware global no final das configurações do seu app. Por exemplo, aqui vamos evitar enviar o HTML:

```js
// src/app.js

app.put('/teams/:id', validateTeam, ... );
app.delete('/teams/:id', ... );

// se ninguém respondeu, vai cair neste middleware
app.use((req, res) => res.sendStatus(404));

module.exports = app;
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/87f949db-4efb-40bc-b9b5-32199bca9846)
