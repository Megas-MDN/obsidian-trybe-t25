[[Node]]
[[Node - 14 Middlewares]]

## Enviando mensagens de erros personalizadas na resposta

A aplicação realiza a validação dos _inputs_ recebidos, e caso eles apresentem algum erro, a API responde com um código de erro. Entretanto estes códigos [HTTP Status](https://www.httpstatus.com.br/) definem o tipo de erro, mas não trazem nenhuma informação mais precisa do qual seria o erro. Para resolver isso, pode se enviar na responta um json com um objeto por exemplo `{ message: 'Mensagem de erro personalizada'}`. Vamos utilizar como exemplo o middleware `validateTeam`.

```js
const validateTeam = (req, res, next) => {
  const requiredProperties = ['nome', 'sigla'];
  if (requiredProperties.every((property) => property in req.body)) {
    next(); // Chama o próximo middleware
  } else {
    res.sendStatus(400); // Ou já responde avisando que deu errado
  }
};
```

Vamos modificar a função para que cada campo possua uma mensagem específica caso os dados que chegam na requisição não sejam válidos. Ficando assim:

```js
const validateTeam = (req, res, next) => {
  const { nome, sigla } = req.body;
  if (!nome) return res.status(400).json({ message: 'O campo "nome" é obrigatório'});
  if (!sigla) return res.status(400).json({ message: 'O campo "sigla" é obrigatório'});
  next();
};
```

Desta forma, caso seja enviado na requisição um objeto que não possua propriedade “nome”, a aplicação retornar o status 400 e o objeto `{ message: 'O campo "nome" é obrigatório'}`. Caso seja enviado um objeto que não possua propriedade “sigla”, o middleware retorna o status 400 e o objeto `{ message: 'O campo "sigla" é obrigatório'}`. Mas caso seja enviado um objeto com as propriedades “nome” e “sigla”, então será chamado o próximo middleware através do `next()`.

Outro detalhe é que invertemos a lógica da validação. Anteriormente se as informações da requisição estivessem corretas, era chamado o próximo middleware. Agora, primeiramente verificamos todas as informações, e depois, caso estejam corretas, é chamado o próximo middleware. Esta forma permite encadear cada uma das validações, e criar respostas específicas para cada uma.

## Para fixar

Agora é sua vez. Modifique o código do middleware `existingId` para retornar o _http status_ `404` e um objeto no formato `{ message: 'Time não encontrado' }` quando não encontrar o time com o **id** recebido.

## Passando valores entre middlewares com objeto `req`

**Middlewares também podem modificar os objetos `req` e `res`.** Essas modificações serão recebidas pelos próximos middlewares caso `next` seja chamado. Geralmente isso é utilizado para propagar informações de um middleware para o outro. Isso dá ainda mais flexibilidade para sua **composição de middlewares**.

Vamos rever o nosso arquivo `authdata.json`. Ele tem os dados organizados assim:

```json
{
  "dGlqb2xvMjIK": { "appId": 1, "teams": ["SAO", "PAL"] },
  "bDRkcjFsaDAK": { "appId": 2, "teams": ["FLA", "FLU"] }
}
```

Como você pode ver, cada app (representado por um `appId`) tem autoridade sobre alguns times. Quando a API recebe uma requisição para criar um time, ela vai conferir pelo token se aquele app pode criar aquele time. Vamos carregar essa informação em nosso middleware `apiCredentials` e deixá-la disponível para que a rota `POST /teams` confira se o time pode ser criado por esse app.

Primeiro, adicionamos uma linha no nosso middleware para adicionar essa informação ao nosso objeto `req`:

```js
// src/middlewares/apiCredentials.js

//...
module.exports = async function apiCredentials(req, res, next) {
  //...
  const authorized = JSON.parse(authdata);
  if (token in authorized) {
    // modifica o req para guardar a informação importante
    req.teams = authorized[token];
    next();
  } else {
    res.status(401).json({ message: 'Token inválido ou expirado.'});
  }
};
```

Repare que estamos usando `req.teams` para guardar essa informação. Poderíamos criar qualquer propriedade, mas devemos ter cuidado para não sobrescrever as propriedades que `req` já tem. Na dúvida, você pode conferir os campos do `req` usando o debugger. Aqui vamos usar `teams` mesmo, que não tem conflito nenhum.

Agora, no middleware da rota `POST /teams` podemos usar essa informação para conferir se aquele cliente da nossa API tem a autoridade para criar o time que ele está querendo criar:

```js
// src/app.js

//...

app.post('/teams', validateTeam, (req, res) => {
  if (
    // confere se a sigla proposta está inclusa nos times autorizados
    !req.teams.teams.includes(req.body.sigla)
    // confere se já não existe um time com essa sigla
    && teams.every((t) => t.sigla !== req.body.sigla)
  ) {
    return res.status(422).json({ message: 'Já existe um time com essa sigla'});
  }
  const team = { id: nextId, ...req.body };
  teams.push(team);
  nextId += 1;
  res.status(201).json(team);
});

//...
```

Prontinho, agora você também já aprendeu a empregar a passagem de valores entre middlewares e pode dar check em mais uma habilidade do dia! 🤩


## Respondendo duas vezes acidentalmente

Reparou que no middleware do `POST /teams` nós usamos return dentro do bloco `if`? Fizemos isso porque, em Javascript, `return` encerra a função. É exatamente isso que queremos! Depois de enviar uma resposta não precisamos seguir na função. Se seguirmos, vamos ver um erro _extremamente comum_ no desenvolvimento backend:

```bash
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
```

O que essa mensagem está tentando dizer é que você **não pode enviar mais de uma resposta para uma requisição**. Quando passamos pela linha que diz `return res.status(400).json({ message: 'Já existe um time com essa sigla'})`, estamos enviando uma resposta. Se depois do bloco `if` continuamos a função, chegaremos na linha que diz `res.status(201).json(...)`, ocorrendo em enviar _outra_ resposta. E isso é um erro!

### Solução

```js
const existingId = (req, res, next) => {
  const id = Number(req.params.id);
  if (!teams.some((t) => t.id === id)) {
    return res.sendStatus(404).json({ message: 'Time não encontrado' });
  }
  next();
};
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/cdb3f117-0c56-44fc-9cf6-447f61a0c8b4)