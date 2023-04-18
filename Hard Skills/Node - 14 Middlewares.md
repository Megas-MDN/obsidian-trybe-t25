[[Node]]

O Express é um framework com um objetivo central: receber requisições e enviar respostas. Você já viu como ele usa funções que recebem requisição (`req`) e resposta (`res`) como parâmetros. Agora, você verá como essas funções podem ser **decompostas** em funções menores, que podem ser aproveitadas em diversas rotas.

Cada função terá uma responsabilidade única, se essa função capturar algum problema, uma resposta de erro será retornada para a pessoa usuária.

Exemplos:

-   Formato de e-mail não apropriado;
-   CPF com formato inválido;
-   Pessoa usuária não tem permissão de acesso.

Agora, se estiver tudo certo, será indicado no final dessa função, seguir para a próxima função da rota (fazendo uma validação diferente). Com isso, serão feitas quantas funções forem necessárias, até que uma delas devolva uma resposta a pessoa usuária. Esse é um estilo de **composição de funções** chamado **middlewares**.

A primeira coisa que você precisa saber sobre middlewares é: **no Express toda função passada para uma rota é um middleware**.

_Calma aí, como assim?_ 🤔

Para o Express, um [middleware](https://expressjs.com/pt-br/guide/using-middleware.html) é uma função que realiza o tratamento de uma requisição HTTP e que pode responder essa request ou chamar o próximo middleware.

> 🤫 **Bom, para te contar um segredo:** estamos usando middlewares desde o começo deste conteúdo, mas com outro nome! Até agora, nos referimos aos middlewares como `callbacks` ao falar sobre roteamento e definição de endpoints. Acontece que todos os callbacks que mostramos nessas rotas são middlewares.

**Na prática, middlewares recebem três parâmetros:** `req`, `res` e `next`, exatamente como as funções callback que usamos até agora para registrar rotas.

**Middlewares não precisam retornar nada.** O fato é que o Express ignora o retorno dos middlewares, visto que o importante é se aquele middleware chamou ou não um método que responda a request, e se ele chamou ou não a função `next`.

Bora estudar como refatorar um middleware? 🚀

## Refatorando um middleware

Agora que você estudou o que são middlewares, o próximo passo será refatorar a API de times de futebol e aplicar na prática o aprendizado de middlewares.

Para isso, preste atenção especialmente nos métodos `POST` e `PUT`:

Vamos para o código?

No código abaixo terá o CRUD completo, observe este código novamente, com o destaque para as rotas `PUT` e `POST`:

```js
// src/server

const app = require('./app');

app.listen(3001, () => console.log('server running on port 3001'));
```

```js
// src/app.js

const express = require('express');

const app = express();

let nextId = 3;
const teams = [
  { id: 1, nome: 'São Paulo Futebol Clube', sigla: 'SPF' },
  { id: 2, nome: 'Sociedade Esportiva Palmeiras', sigla: 'PAL' },
];

app.use(express.json());

app.get('/teams', (req, res) => res.json(teams));

app.get('/teams/:id', (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  if (team) {
    res.json(team);
  } else {
    res.sendStatus(404);
  }
});

app.post('/teams', (req, res) => {
  const requiredProperties = ['nome', 'sigla'];
  if (requiredProperties.every((property) => property in req.body)) {
    const team = { id: nextId, ...req.body };
    teams.push(team);
    nextId += 1;
    res.status(201).json(team);
  } else {
    res.sendStatus(400);
  }
});

app.put('/teams/:id', (req, res) => {
  const id = Number(req.params.id);
  const requiredProperties = ['nome', 'sigla'];
  const team = teams.find(t => t.id === id);
  if (team && requiredProperties.every((property) => property in req.body)) {
    const index = teams.indexOf(team);
    const updated = { id, ...req.body };
    teams.splice(index, 1, updated);
    res.status(201).json(updated);
  } else {
    res.sendStatus(400);
  }
});

app.delete('/teams/:id', (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  if (team) {
    const index = teams.indexOf(team);
    teams.splice(index, 1);
  }
  res.sendStatus(204);
});

module.exports = app;
```

> Lembre-se que para testar, o express deve ter sido instalado na aplicação. Para isso, você pode usar o comando `npm install express@4.17.1 --save-exact`.

> Para instalar e configurar as dependências de desenvolvimento, consulte o conteúdo do segundo dia desta seção, na lição “Express”. 😉

Você reparou que precisou validar os dados enviados duas vezes: uma para a rota `PUT` e outra para rota `POST`, de modo a garantir que as informações esperadas (nome e sigla) fossem enviadas?

Provavelmente, lhe deu vontade de isolar esse código em uma função separada, não é mesmo? Assim não precisaria editar dois trechos diferentes de código, caso um dia quisesse ampliar a validação, de modo a conferir se a sigla tem exatos três caracteres, por exemplo.

> Manter código duplicado é uma receita certeira para bugs. _Don’t Repeat Yourself_!

O Express permite que o tratamento de uma rota seja decomposto em várias funções **middlewares**. Um middleware deve fazer apenas o seu próprio trabalho (por exemplo, conferir um cabeçalho), e então escolher entre responder (`res`) a requisição ou chamar o próximo middleware (`next`). Assim, uma rota pode ser tratada por uma sequência de middlewares, cada um fazendo uma parte do tratamento da requisição.

Vamos ver como ficaria um middleware de validação das propriedades necessárias para a aplicação? 😎

```js
// src/app.js

// ...
const validateTeam = (req, res, next) => {
  const requiredProperties = ['nome', 'sigla'];
  if (requiredProperties.every((property) => property in req.body)) {
    next(); // Chama o próximo middleware
  } else {
    res.sendStatus(400); // Ou já responde avisando que deu errado
  }
};

// Arranja os middlewares para chamar validateTeam primeiro
app.post('/teams', validateTeam, (req, res) => {
  const team = { id: nextId, ...req.body };
  teams.push(team);
  nextId += 1;
  res.status(201).json(team);
});

app.put('/teams/:id', validateTeam, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  if (team) {
    const index = teams.indexOf(team);
    const updated = { id, ...req.body };
    teams.splice(index, 1, updated);
    res.status(201).json(updated);
  } else {
    res.sendStatus(400);
  }
});

// module.exports = app;
```

Repare como o método POST foi definido de uma maneira mais direta e reaproveitável, deixando os detalhes de validação para o middleware `validateTeam`. Se a requisição chegou no segundo middleware, ele pode criar o time sem se preocupar com mais nada.

Os middlewares seguintes podem receber o `next` como um terceiro parâmetro, mas **geralmente o último middleware de uma rota precisa responder a requisição**. Portanto, se ele não for chamar outro middleware, não há necessidade de usar o objeto `next` e você pode escrever a função recebendo apenas dois parâmetros: os objetos `req` e `res`.

## E o que o middleware validateTeam faz?

1️⃣ Faz uma validação básica que apenas confere se todas as propriedades esperadas estão presentes no `req.body`.

2️⃣ Se a validação aprovar, esse middleware endereça a requisição para o próximo middleware, que efetivamente cria o time.

3️⃣ Se a validação falhar, esse middleware retorna uma resposta com `status 400` e **nunca chama o próximo middleware**. `400` é o código HTTP para `Bad Request`, indicando que existe algo errado na requisição. Para mais informações sobre códigos HTTP, confira a [documentação](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status) no site da MDN (Mozilla Developer Network).

Observe o fluxo da requisição no diagrama abaixo:

![Passo a passo da requisição passando pelos middlewares](https://content-assets.betrybe.com/prod/Passo%20a%20passo%20da%20requisi%C3%A7%C3%A3o%20passando%20pelos%20middlewares.png)
> Passo a passo da requisição passando pelos middlewares

Veja um exemplo de requisição que passa na validação:

![Requisição correta do tipo POST feita à rota teams](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20correta%20do%20tipo%20POST%20feita%20%C3%A0%20rota%20teams.gif)

Requisição correta do tipo POST feita à rota /teams

Agora, veja um exemplo que não passa:

![Requisição incorreta do tipo POST feita à rota teams](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20incorreta%20do%20tipo%20POST%20feita%20%C3%A0%20rota%20teams.gif)

Requisição incorreta do tipo POST feita à rota /teams

> 💡 Experimente fazer a mesma requisição comentando a instrução `next()` e você vai notar que a requisição **nunca** vai chegar na segunda rota e, por isso, você nunca terá uma resposta!

![Requisição correta do tipo POST feita à rota recipes que não responde](https://content-assets.betrybe.com/prod/Requisi%C3%A7%C3%A3o%20correta%20do%20tipo%20POST%20feita%20%C3%A0%20rota%20recipes%20que%20n%C3%A3o%20responde.gif)
>Requisição correta do tipo POST feita à rota /recipes que não responde


## Para Fixar



## Exercício 1 


-   Crie um middleware `existingId` para garantir que o `id` passado como parâmetro na rota `GET /teams/:id` existe no objeto `teams`. Refatore essa rota para usar o middleware.

O objeto `teams` é um array. O `id` recebido via parâmetro **é sempre uma string**. Então precisamos converter primeiro antes de procurar pelo `id`. Para confirmar se um valor existe podemos usar o método `array.some`:

> src/app.js

```js
//...
const existingId = (req, res, next) => {
  const id = Number(req.params.id);

  if (teams.some((t) => t.id === id)) {
    // se existe, a requisição segue para o próximo middleware
    return next();
  }

  // se não existe, então vamos retornar o status HTTP 404
  res.sendStatus(404);
};
//...

// usa o middleware
app.get("/teams/:id", existingId, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  res.json(team);
});
```

**Preciso usar `return` sempre que usar `next()`?** O importante aqui é evitar que duas respostas sejam enviadas. Sem o `return` ali, chamaríamos o `next()` e depois do bloco `if` acabaríamos chamando `res.sendStatus(404)` também! Uma alternativa seria usar `else`, assim o código depois do `if` fica inacessível se a condição for verdadeira:

```js
//...
const existingId = (req, res, next) => {
  const id = Number(req.params.id);

  if (teams.some((t) => t.id === id)) {
    // se existe, a requisição segue para o próximo middleware
    next();
  } else {
    // se não existe, então vamos retornar o status HTTP 404
    res.sendStatus(404);
  }
};
//...
```

---

## Exercício 2

-   Reaproveite esse middleware e refatore as rotas `PUT /teams/:id` e `DELETE /teams/:id` para usarem ele também.

Uma vez que o middleware foi criado, basta inseri-lo nas rotas e remover a lógica duplicada:

> src/app.js

```js
//...
const existingId = (req, res, next) => {
  const id = Number(req.params.id);

  if (teams.some((t) => t.id === id)) {
    // se existe, a requisição segue para o próximo middleware
    next();
  } else {
    // se não existe, então vamos retornar o status HTTP 404
    res.sendStatus(404);
  }
};
//...
// a ordem é significativa, embora neste caso faça pouca diferença
app.put('/teams/:id', existingId, validateTeam, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  // não precisamos mais conferir, com certeza o team existe
  const index = teams.indexOf(team);
  const updated = { id, ...req.body };
  teams.splice(index, 1, updated);
  res.status(201).json(updated);
});

app.delete('/teams/:id', existingId, (req, res) => {
  const id = Number(req.params.id);
  const team = teams.find(t => t.id === id);
  const index = teams.indexOf(team);
  teams.splice(index, 1);
  res.sendStatus(204);
});
//...
```

## Exercício 3


É fundamental lembrar do `module.exports` no arquivo novo. Podemos copiar a função exatamente do mesmo jeito, só precisamos lembrar de exportá-la:


```js
// src/middlewares/validateTeam.js

const validateTeam = (req, res, next) => {
  const requiredProperties = ['nome', 'sigla'];
  if (requiredProperties.every((property) => property in req.body)) {
    next(); // Chama o próximo middleware
  } else {
    res.sendStatus(400); // Ou já responde avisando que deu errado
  }
};

module.exports = validateTeam;
```

## Exercício 4


Vamos seguir o mesmo raciocínio que fizemos para isolar o middleware `validateTeam` aqui.

```js
// src/middlewares/existingId.js
const existingId = (req, res, next) => {
  const id = Number(req.params.id);
  if (teams.some((t) => t.id === id)) {
    // se existe, a requisição segue para o próximo middleware
    next();
  } else {
    // se não existe, então vamos retornar o status HTTP 404
    res.sendStatus(404);
  }
};
```

Já no `src/app.js`, ambas funções são substituídas, cada uma, por um `require`. Repare no _caminho relativo_, isto é, o `app.js` está no diretório `src`, e um middleware no `src/middlewares/validateTeam.js` e o outro no `src/middlewares/existingId.js`. Relativamente, seria apenas `./middleware/validateTeam.js` e `./middlewares/existingId.js` respectivamente.

```js
// src/app.js

//...
// não precisa do sufixo .js, o node sabe deduzir
const validateTeam = require('./middleware/validateTeam');
const existingId = require('./middleware/existingId');
//...
// o resto do arquivo fica idêntico
```

Nada muda nas rotas, porque o middleware continua acessível pela mesma variável.



#### Recursos adicionais

-   [Usando Middlewares](https://expressjs.com/pt-br/guide/using-middleware.html)
-   [Escrevendo Middlewares](https://expressjs.com/pt-br/guide/writing-middleware.html)
-   [Express - Middlewares](https://reflectoring.io/express-middleware/)
-   [Middleware no Express - JS](https://www.geeksforgeeks.org/middleware-in-express-js/)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/e3f0b1ef-d574-45ef-abb3-22a6ea384448)
