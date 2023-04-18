[[Node - 14 Middlewares]]
[[Node]]

Até agora, falamos de middlewares comuns, que recebem `req`, `res` e `next` e tratam uma request caso tudo esteja correndo bem. Acontece que existe ainda um outro tipo de middleware: o **de erro**.

É importante saber que:

-   Middleware de erro **sempre deve vir depois de rotas e outros middleware**;
    
-   Middleware de erro **só recebe requisições se algum middleware lançar um erro ou chamar a função `next()` com algum parâmetro**.
    
-   Middleware de erro **sempre deve receber quatro parâmetros**.
    

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico. **O Express utiliza a quantidade de parâmetros que uma função recebe para determinar se ela é um middleware de erro ou um middleware comum**. Ou seja, mesmo que você não vá utilizar os parâmetros `req`, `res` ou `next`, seu middleware de erro precisa recebê-los. Você pode adicionar um underline no começo do nome do parâmetro que não será utilizado. Isso é uma boa prática e sinaliza para quem está lendo o código quais argumentos de fato estão sendo utilizados na implementação da função. Por exemplo: `function (err, _req, res, _next) {}`.

Também é possível encadear middlewares de erro, no mesmo esquema dos comuns, simplesmente colocando-os na sequência em que devem ser executados.

Bora colocar a mão na massa e aprender na prática, como utilizar um middleware de erros!!!

**Pré-configurações:** 1 - Em um arquivo `app.js`, teremos as configurações básicas da nossa aplicação, utilizando o express.

```js
// src/app.js
const express = require('express');
const app = express();

const PORT = 3000;

app.use(express.json());

app.listen(PORT, () => console.log(`Rodando na porta: ${PORT}`));
```

2- Em um arquivo `teams.json`, teremos uma lista de objetos, contendo as seguintes informações:


```json
 // ./teams.json
 [
   {
     "nome": "Sociedade esportiva Palmeiras",
     "fundação": "26 de agosto de 1914"
   },
   {
     "nome": "Sport club Corinthians Paulista",
     "fundação": "1 de setembro de 1910"
   },
   {
     "nome": "São Paulo Futebol Clube",
     "fundação": "25 de janeiro de 1930"
   },
   {
     "nome": "Club de Regatas Vasco da Gama",
     "fundação": "21 de agosto de 1898"
   },
   {
     "nome": "Clube Atlético Mineiro",
     "fundação": "25 de março de 1908"
   }
 ]
```

Com nossas configurações iniciais prontas, agora criaremos nossa lógica. Para pegar as informações do nosso arquivo `teams.json`, e caso aconteça algum erro, configuraremos um middleware para lidar com esse erro.

Para isso, comece definindo uma rota `/teams`, utilizando o método **GET**.

Nessa rota, utilizaremos o módulo `fs` para acessar as informações do nosso arquivo `teams.json`, convertendo para JSON e mandando como resposta para o usuário.

É importante ressaltar que essa lógica deve estar dentro do escopo de um **try catch**, pois caso aconteça algum erro, o **catch** irá passá-lo como parâmetro para nosso `next`.

Copiar

```js
 // ./app.js
 // const express = require('express');
 const fs = require('fs').promises;
 // const app = express();
 // const PORT = 3000;
 // app.use(express.json());
 app.get('/teams', async (req, res, next) => {
    try {
         const data = await fs.readFile(path.resolve(__dirname, './teams.json'));
         const teams = JSON.parse(data);
         return res.status(200).json({ teams })
     } catch (error) {
        return next(error);
    }
 });
 // app.listen(PORT, () => console.log(`Rodando na porta: ${PORT}`));
```

Por fim, precisamos definir o middleware de erro, que será chamado sempre que tiver um `next(error)` em nosso código.

Copiar

```js
// ./app.js
// const express = require('express');
// const fs = require('fs').promises;
// const app = express();
// const PORT = 3000;
// app.use(express.json());
/*
 app.get('/teams', async (req, res, next) => {
   try {
     const data = await fs.readFile(path.resolve(__dirname, './teams.json'));
     const teams = JSON.parse(data);
     return res.status(200).json({ teams })
   } catch (error) {
     return next(error);
   }
 });
 */

//...
app.use((error, _req, res, _next) => {
   return res.status(500).json({ error: error.message });
});
// app.listen(PORT, () => console.log(`Rodando na porta: ${PORT}`));
```

> Para visualizar o middleware de erro atuando corretamente, tente excluir conteúdo do arquivo `teams.json`, dessa forma, o `fs` não conseguirá trazer nenhuma informação e um erro será gerado. Repare que estamos chamando `next(error)` com o _error_ como parâmetro. Isso diz ao Express que ele deve executar middleware de erro. Ou seja, **quando passamos qualquer parâmetro para o `next`, o `Express` entende que é um erro e deixa de executar middlewares comuns**, passando a execução para o próximo middleware de erro registrado para aquela rota, router ou aplicação.

Um exemplo desse fluxo pode ser visualizado na imagem abaixo:

![Fluxo utilizando um middleware de erro](https://content-assets.betrybe.com/prod/60ced083-e890-42c8-ad00-cf2610ab85f0-Fluxo%20utilizando%20um%20middleware%20de%20erro.png)

Fluxo utilizando um middleware de erro

Esse mesmo tipo de erro pode acontecer ao fazer uma query para um banco de dados e ter várias possíveis falhas, como por exemplo: o banco não está respondendo ao nosso pedido de conexão, temos uma query escrita errada, as credenciais de acesso ao banco estão erradas, entre outras falas.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/8637f4e5-9ea6-4bdb-8fad-0e10384f26d9)
