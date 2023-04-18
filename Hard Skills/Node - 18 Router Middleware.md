[[Node]]
[[Node - 14 Middlewares]]

Você deve estar pensando: _“Nossa! Mas, com todas essas coisas, meu arquivo principal vai ficar gigante!”_ 😱

Calma! O Express tem uma solução bem interessante para organizar suas rotas e middlewares: o **Router.**

**O `Router` é um middleware que “agrupa” várias rotas em um mesmo lugar**, como se fosse uma versão mini do `app` do Express. Ele é depois “plugado” no “app principal”.

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico.

Vamos utilizar o Router para organizar o código que desenvolvemos no app de times:

```js

// src/app.js

const express = require('express');
require('express-async-errors');
const morgan = require('morgan');
// require no nosso novo router
const teamsRouter = require('./routes/teamsRouter');

const app = express();
app.use(morgan('dev'));
app.use(express.static('/images'));
app.use(express.json());
// monta o router na rota /teams (1)
app.use('/teams', teamsRouter);

app.use((err, _req, _res, next) => {
  console.error(err.stack);
  next(err);
});

app.use((err, _req, res, _next) => {
  res.status(500).json({ message: `Algo deu errado! Mensagem: ${err.message}` });
});

module.exports = app;
```

Agora, crie um diretório `routes` e o arquivo `teamsRouter.js`. Veja abaixo como deve ficar:

```js
// src/routes/teamsRouter.js

const express = require('express');
// os requires são relativos ao arquivo, então o path muda ligeiramente
const existingId = require('../middlewares/existingId');
const validateTeam = require('../middlewares/validateTeam');
const apiCredentials = require('../middlewares/apiCredentials');

// cria um router middleware
const router = express.Router();

let nextId = 3;
const teams = [
  { id: 1, nome: 'São Paulo Futebol Clube', sigla: 'SPF' },
  { id: 2, nome: 'Sociedade Esportiva Palmeiras', sigla: 'PAL' },
];

// o path é relativo à rota em que o router foi montado (2)
router.get('/', (req, res) => res.json(teams));

// configurações globais afetam apenas este router (3)
router.use(apiCredentials);

router.get('/:id', existingId, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  res.json(team);
});

router.post('/', validateTeam, (req, res) => {
  const team = { id: nextId, ...req.body };
  teams.push(team);
  nextId += 1;
  res.status(201).json(team);
});

router.put('/:id', existingId, validateTeam, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  const index = teams.indexOf(team);
  const updated = { id, ...req.body };
  teams.splice(index, 1, updated);
  res.status(200).json(updated);
});

router.delete('/:id', existingId, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  const index = teams.indexOf(team);
  teams.splice(index, 1);
  res.sendStatus(204);
});

module.exports = router;
```

Nosso arquivo `app.js` ficou arrumado agora! Routers tem essa qualidade maravilhosa! Vamos prestar atenção em alguns detalhes:

1.  No arquivo `src/app.js`, repare no uso de mais um parâmetro na chamada à função `app.use`. Isso diz ao Express que queremos que aquele middleware (no caso o router) seja executado para qualquer rota **que comece** com aquele caminho(no caso, `'/teams'`).
    
2.  Já no `src/routes/teamsRouter.js`, repare que, ao registrar uma rota no router, não precisamos repetir a parte do caminho que já passamos para `app.use`. É por isso que a rota que definimos com `router.get('/:id')` na verdade se torna acessível por meio de `/teams/:id`.
    
3.  **Routers suportam que qualquer tipo de middleware seja registrado.** Ou seja, se tivermos vários endpoints com autenticação e vários endpoints abertos, podemos criar um router, e registrar nele nosso middleware de autenticação, bem como todas as rotas que precisam ser autenticadas, registrando as rotas abertas diretamente no app.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/cda94a05-9e87-4f4b-a109-08ca198617c6)
