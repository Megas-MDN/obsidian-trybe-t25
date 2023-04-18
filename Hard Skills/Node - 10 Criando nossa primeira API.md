[[Node]]


Chegou o grande momento! Agora, vamos criar nossa primeira API e utilizar na prática o que aprendemos até agora, além dos principais métodos HTTP. Vamos nessa?

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico. Contudo, não deixe de praticar tentando executar o código junto ou executando os códigos do exemplo desta seção! 😉

## Listando times por meio do método GET

Em nossa API, os dados serão armazenados em um array de objetos. Para isso, ainda dentro do arquivo `app.js`, crie um array contendo as informações abaixo:


```js
// src/app.js

// const express = require('express');

const teams = [
  {
    id: 1,
    name: 'São Paulo Futebol Clube',
    initials: 'SPF',
  },
  {
    id: 2,
    name: 'Clube Atlético Mineiro',
    initials: 'CAM',
  },
];

// ...
```

Agora, você vai criar um endpoint do tipo `GET` com a rota `/teams`, como mostra o trecho de código abaixo:

```js
// src/app.js

// ...

// app.get('/', (req, res) => res.status(200).json({ message: 'Olá Mundo!' }));

app.get('/teams', (req, res) => res.status(200).json({ teams }));

// module.exports = app;
```

Aqui, a única diferença é que responderemos a requisição com o array de times. Salve o arquivo, o nodemon vai reiniciar o servidor para nós e você pode acessar a URL `http://localhost:3001/teams` em seu navegador.

## Cadastrando times por meio do método POST

Para cadastrar um novo time é muito simples, porém agora queremos receber os dados no corpo da requisição. Para fazer isso, crie um endpoint do tipo `POST` com a rota `/teams`, como mostra o trecho de código abaixo:

Copiar

```js
// src/app.js

// ...

// app.get('/teams', (req, res) => res.status(200).json({ teams }));

app.post('/teams', (req, res) => {
  const newTeam = { ...req.body };
  teams.push(newTeam);

  res.status(201).json({ team: newTeam });
});

// module.exports = app;
```

Os dados serão enviados pelo corpo da requisição e temos acesso a eles por meio do `req.body`. Criamos uma nova constante chamada `newTeam` e aplicamos a desestruturação no `req.body`. Após isso, armazenamos o dado em nosso array de times e respondemos a requisição, agora com o `status 201`.

> Esse status 201 que dizer _created_, ele ajuda na semântica da resposta.

Agora vem um outro ponto importante! Nós não conseguimos mais realizar testes em nossa API utilizando apenas nosso navegador 😔

Isso acontece pois não temos onde enviar os dados do body, mas calma! Podemos resolver isso de uma forma muito simples: em seu Visual Studio Code, instale uma extensão chamada **Thunder Client**, [informações de instalação aqui](https://www.thunderclient.com/).

### Thunder Client

Após instalar a extensão em seu Visual Studio Code, na barra lateral irá aparecer um **ícone de um raio**. Ao **clicar nele**, uma nova barra irá se abrir com um botão superior escrito `New Request` assim como mostra a imagem abaixo:

![Iniciando Thunder Client](https://content-assets.betrybe.com/prod/Iniciando%20Thunder%20Client.png)

Iniciando Thunder Client

Após clicar no botão **New Request**, uma nova aba em seu Visual Studio Code se abrirá.

No campo da URL, selecionaremos o verbo `POST` e preencheremos o endereço com `http://localhost:3001/teams/`. Clicando na aba `Body`, selecionaremos o formato Json e preencheremos o corpo da requisição com as seguintes informações:

Copiar

```json
{
  "id": 3,
  "name": "Clube de Regatas do Flamengo",
  "initials": "FLA"
}
```

O preenchimento deve estar conforme a imagem abaixo:

![Tela de request usando Thunder Client](https://content-assets.betrybe.com/prod/Tela%20de%20request%20usando%20Thunder%20Client.png)

Tela de request usando Thunder Client

Agora, vamos entender o passo a passo do que está acontecendo, seguindo a numeração da imagem.

-   Passo 1: Aqui, podemos preencher com a URL da nossa aplicação(é a mesma que estamos usando no navegador);
    
-   Passo 2: Aqui, podemos escolher o método de envio, observe que tem vários, já aprendemos alguns e outros ainda vamos ver. Neste caso, escolha o método do tipo `POST`;
    
-   Passo 3: Lembra que queremos enviar os dados pelo corpo da requisição? Então aqui pode escolher `Body`.
    
-   Passo 4: Quando optamos pela opção `Body`, isso nos habilita escolher o formato de envio! Existem vários também, mas agora vamos optar por `JSON`.
    
-   Passo 5: Após escolher o formato em que vamos enviar nossos dados, podemos escrevê-lo em formato JSON no campo abaixo.
    

---

Após essa breve introdução à ferramente incrível que é o `Thunder Client`, vamos realizar o teste de nossa aplicação. 🚀

_Clique_ em _Send_ e veja o resultado!

Podemos perceber que o resultado de nossa requisição aparece em uma aba à direita.

> Lembra do `status code` que comentamos antes? Olha ele presente ali na resposta da nossa requisição, sinalizado com o número `6`! 😁

![Telas de request e response usando Thunder Client](https://content-assets.betrybe.com/prod/Telas%20de%20request%20e%20response%20usando%20Thunder%20Client.png)

Telas de request e response usando Thunder Client

Em nossa resposta, tem apenas a seguinte informação:

Copiar

```json
// Dentro do Thunder Client

{
  "team": {}
}
```

Aparentemente funcionou, mas não está trazendo o que nós gostaríamos. 🤔

Vamos parar por aqui? Claro que não! Somos pessoas desenvolvedoras e nossa função é resolver problemas.

Se nós alterarmos o verbo para o método `GET` novamente e clicarmos em _Send_, vamos perceber que o time Flamengo não foi cadastrado, certo? Podemos tentar cadastrar novamente e até fazer _double check_ com o navegador.

A grosso modo, esse comportamento funciona, pois nossa API não está preparada para receber dados. Nós consertamos isso de uma forma bem simples, apenas escrevendo o seguinte trecho de código:

```js
// src/app.js

// ...

// const app = express();

app.use(express.json());

// ...
```

A princípio, vamos entender que o `app.use()` serve para “instalar” algumas coisas que queremos em nossas APIs. Mais adiante, nesta mesma seção, você vai ver todo o poder desta função, mas por ora, saiba que ela serve para configurar mais coisas em nossa API, ok?

Dentro do `app.use()`, passamos uma outra função é ela que habilita a possibilidade de recebermos dados pelo corpo (`body`) de nossa requisição. Após inserir essa linha em seu código, volte no Thunder Client e refaça a requisição tentando inserir o time do Flamengo no array (não esqueça de trocar o método para `POST` novamente para isso, hein? 😉).

Pronto! Agora se você listar todos os clubes na rota `/teams` utilizando o método `GET`, tanto no Thunder Client quanto no navegador, você irá ver que o Flamengo foi cadastrado. E pode se parabenizar, você acabou de passar por mais uma **habilidade** do dia: _Utilizar_ o _VSCode Thunder Client_ para fazer requisições a partir do VSCode.

## Editando times por meio do método PUT

Para alterar algum time, você precisa do `id` deste time e dos novos dados, correto? Com o que aprendemos até agora, os novos dados vêm no corpo da requisição e o `id` vem por parâmetro. Após capturar tudo isso, você precisa procurar dentro do array `teams` o time correspondente com aquele `id` e alterar as informações dele. Como pode acontecer de não existir um time com aquele `id` buscado, precisamos também devolver uma resposta para esses casos. Vamos fazer isso com o trecho de código abaixo:

```js
// src/app.js

// ...

app.put('/teams/:id', (req, res) => {
  const { id } = req.params;
  const { name, initials } = req.body;

  const updateTeam = teams.find((team) => team.id === Number(id));

  if (!updateTeam) {
    res.status(404).json({ message: 'Team not found' });
  }

  updateTeam.name = name;
  updateTeam.initials = initials;
  res.status(200).json({ updateTeam });
});

// ...
```

Observe que o método mudou, não é `GET` nem `POST`! Aqui, estamos trabalhando com método `PUT`, o qual é utilizado quando queremos alterar um recurso. Ele também recebe dados pelo corpo da requisição.

Logo após isso, temos a rota `/teams/:id`. Essa rota mostra para nós que além de esperar os dados vindo pelo `body` da requisição, também esperamos um `id` vindo pela URL, por meio do `req.params`.

Mais adiante em nosso código, desconstruímos essas informações e criamos a variável `updateTeam`, na qual vamos armazenar o resultado da busca pelo id que recebemos como parâmetro dentro do array de times. Caso não seja encontrado um time correspondente, devolvemos uma resposta informando isso.

Quando o time é encontrado, alteramos as informações dele no array e o salvamos na variável `updateTeam`. Ao final, respondemos com o `status 200 - ok` e o time alterado.

⚠️ Aviso: Antes de realizarmos os testes no Thunder Client, você precisa saber disto: Todo dado que vem por `params` ou por `query` (ou seja dados enviados pela URL do navegador) são recebidos como `string`. Por isso, fizemos um “parser” desse valor para `Number` (dentro do `if`).

> Preste bastante atenção nisso, sem esse parser, o `if` nunca vai encontrar o `id`, pois o id 1 é diferente do id ‘1’! Seria como comparar `1 === '1'`, o retorno seria _false_.

Após salvar o arquivo `app.js`, o servidor será reiniciado e você poderá ir até o Thunder Client fazer uma requisição do tipo `PUT`. Para isso, altere o método para `PUT` e a URL para `http://localhost:3001/teams/1`. Em seguida, no `Body`, coloque o seguinte `Json`:

Copiar

```json
// No Thunder Client

{
  "id": "1",
  "name": "Fortaleza Esporte Clube",
  "initials": "FOR"
}
```

Se tudo estiver preenchido corretamente, o resultado deve ser como o da imagem a seguir:

![Alterando um time](https://content-assets.betrybe.com/prod/Alterando%20um%20time.png)

Alterando um time

O resultado esperado é um Status `200` (OK), com a seguinte `response`:

```json
// No Thunder Client - lado direito

{
  "updateTeam": {
    "id": 1,
    "name": "Fortaleza Esporte Clube",
    "initials": "FOR"
  }
}
```

### Para fixar

Que tal treinar seus conhecimentos e listar um time pelo seu `id`? Crie um endpoint do tipo `GET` com a rota `/teams/:id`.

## Deletando times por meio do método DELETE

Para finalizar nossa API, vamos deletar um clube por `id`. Assim como no endpoint da alteração, vamos receber este id por parâmetro, pesquisá-lo no array e deletá-lo. Crie um endpoint do tipo `DELETE` com a rota `/teams/:id` e escreva o trecho de código abaixo:

```js
// src/app.js

// ...

app.delete('/teams/:id', (req, res) => {
  const { id } = req.params;
  const arrayPosition = teams.findIndex((team) => team.id === Number(id));
  teams.splice(arrayPosition, 1);

  res.status(200).end();
});

// ...
```

Novamente capturamos o `id` vindo da URL, encontramos o índice dele no array `teams` com a função `findIndex`, do JavaScript, e removemos o time do array com a função `splice`, também do JavaScript. Ao final, apenas retornamos um `status code 200` dizendo que está tudo ok e encerramos a requisição.

Após tudo isso, bora para o Thunder Client realizar os testes!?

> Só não se esqueça que o método agora é o `DELETE` e que você deve passar o id que será excluído via URL.

Pronto, finalizamos o CRUD de times, que tal executar o linter com o comando `npm run lint` e ver se esta tudo bem 😉

E pode se dar um biscoito/bolacha pela sua habilidade - essa é das grandes! “_Utilizar_ o _Node.js_ com o _framework_ _Express_ para criar uma aplicação _C.R.U.D._ - de _criação_, _leitura_, _atualização_ e _remoção_ de dados”.

⚠️ Aviso: na nossa aplicação, o arquivo `app.js` foi mais que suficiente para abrigar nosso código. Mas se prepare para, em aplicações maiores, usar um arquivo separado só pras suas rotas. No futuro, faremos APIs grandes! 🤩

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/0ca9d8cc-c80d-4296-931b-d3e3833795ba)
