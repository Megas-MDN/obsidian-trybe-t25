[[Node]]


Chegou o grande momento 🥺

Dentro do arquivo `app.js`, que fica no diretório `src/`, escreva o trecho de código a seguir:


```js
// src/app.js

// const express = require('express');

// const app = express();

app.get('/', (req, res) => res.status(200).json({ message: 'Olá Mundo!' }));

// module.exports = app;
```

Acesse a rota pelo seu navegador e verá que já alcançamos mais um marco: “_Utilizar_ o _Node.js_ com o _framework_ _Express_ para criar uma _rota_ de um _endpoint_ de API, acessível pelo browser”. Boa! 🚀

Dentro da constante `app`, temos vários recursos, um deles é a função `get`. Usamos essa função toda vez que queremos **pedir** algum dado.

Observe que a função `get` recebe dois parâmetros:

-   1° parâmetro `'/'`: Aqui é rota que tanto falamos. Podem ser `/login`, `/produtos`, `/pessoas`, ou qualquer outra coisa! Neste caso, colocamos apenas `/`.

> Chamamos a rota `/` de rota raiz;

-   2° parâmetro `(req, res) => {}`: Este espera uma função de callback. Esta função pode receber de 2 a 4 parâmetros, sendo eles:
    -   `req`: Essa é a _Request_ (ou requisição), é por meio dela que recebemos os dados (envio por _query_, _params_ e _body_);
    -   `res`: Essa é a _Response_ (ou resposta), é por meio dela que respondemos o que nos é solicitado;
    -   `next`: Não vamos trabalhar com ele nesta aula;
    -   `err`: Não vamos trabalhar com ele nesta aula.

Essa função é responsável por responder nossas requisições. Então, observe o trecho `res.status(200).json({ message: 'Olá Mundo!' })` e reflita sobre o que cada coisa deve significar.

-   `res` como comentado, responde as requisições. Estas requisições podem ser respondidas de vários jeitos, tais como:
    -   Formato text/JSON, como o caso do `res.json({ message: 'Olá Mundo!' })`;
    -   Formato text/HTML, como o caso do `res.send('<h1>Olá Mundo!</h1>')`;
    -   Redirecionamentos, como o caso do `res.redirect('https://www.betrybe.com/')`;
    -   Páginas completas ou partes dela, como o caso do `res.render('index.html')`;
    -   Finalizando, como o caso do `res.end()`;

⚠️ Aviso: Vamos usar apenas o formato JSON por enquanto.

É de costume enviar um _status code_, como é demostrado no trecho `res.status(200)...`. Estes status code são importantes para identificarmos o que está acontecendo com nossas requisições, mas não se preocupe em decorá-los, com o tempo você vai aprendendo a usá-los e, se tiver dúvidas, pode consultar [a documentação do MDN](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status).

Os _status code_ mais conhecidos são:

-   `200`: Que quer dizer ‘ok’;
-   `500`: Que quer dizer erro no servidor;
-   `404`: Este muitas pessoas já viram, ele quer dizer que a página não foi encontrada;

> De olho na dica 👀: associe os status a constantes nomeadas, desse modo você facilita a leitura! `const OK = 200`, `const INTERNAL_SERVER_ERROR = 500` e `const NOT_FOUND = 404` são ótimos começos!

Agora, vá em seu navegador e digite a URL: `http://localhost:3001/`. Não esqueça que o seu servidor deve estar em execução! Se não estiver basta executar o comando `npm run dev`.

Antes de ir para as próximas rotas, voltaremos a anatomia das URLs:

![Informacoes adicionais do framework Express](https://content-assets.betrybe.com/prod/Informacoes%20adicionais%20do%20framework%20Express.png)

Informações adicionais do framework Express

Neste caso, usamos o domínio `localhost`, pois estamos trabalhando em nossa máquina local. Observe novamente, também, que na figura passamos a porta de forma explicita, `http://localhost:3000/`, e que em nossa aplicação, estamos utilizando a porta 3001!

> Quando estamos trabalhando localmente, temos essa flexibilidade de poder escolher as portas e ter várias aplicações rodando em paralelo. Já no site da Trybe, observe que não precisamos passar a porta, pois estas são padrão (servidores HTTP geralmente respondem na porta 80).

Agora, o que são `GET` e `status code`?🤔

Vamos ver! A maior parte das requisições, na Internet, são feitas seguindo um formato específico - um protocolo chamado **HTTP**.

## Anatomia de requisições: o protocolo HTTP

Vamos analisar o que compõe uma requisição HTTP. Para isso, analisaremos a requisição que é feita pelo navegador quando abrimos a página `https://developer.mozilla.org`.

> Anota aí 🖊: Protocolo é uma convenção que padroniza algo. Neste caso, o protocolo HTTP é uma convenção que padroniza a conexão, comunicação e transferência de dados, entre dois sistemas.

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico.

```bash
GET / HTTP/1.1
Host: developer.mozilla.org
Accept: text/html
```

Vejamos quais são as informações presentes nessa requisição:

-   **O método HTTP** definido por um verbo em inglês. Nesse caso, utilizamos o `GET`, que normalmente é utilizado para “buscar” algo do servidor, e é também o método padrão executado por navegadores quando acessamos uma URL.

> Você vai aprender sobre verbos HTTP em breve;

-   **O caminho no servidor do recurso que estamos tentando acessar**. Nesse caso, o caminho é `/`, pois estamos acessando a página inicial da aplicação;
    
-   **A versão do protocolo** (1.1 é a versão nesse exemplo);
    
-   **O local (host, ou “hospedeiro”) onde está o recurso que se está tentando acessar**, ou seja, a URL! Ou, se for mais direto, o endereço IP servidor.
    

> Nesse caso, utilizamos `developer.mozilla.org`, mas poderia ser `localhost:port`, caso você esteja trabalhando localmente.

Lembra das portas? Elas entram aqui. Quando não especificamos as portas na URL, recebemos direcionamento para alguma porta padrão. Quando especificamos, é pra ela que vamos. Ao escrever `localhost:port`, você está falando para o seu sistema operacional que quer acessar o programa rodando na porta `port` da sua máquina local.

-   **Os headers, ou cabeçalhos,** são informações adicionais a respeito de uma requisição ou de uma resposta. Eles podem ser enviados do cliente para o servidor, ou vice-versa. Na requisição do exemplo acima, temos o header `Host`, o qual informa o endereço do servidor e o header `Accept`, que informa o tipo de resposta a qual esperamos do servidor.

> Alguns exemplos extras de headers podem ser vistos [aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers).

Esses são os dados transmitidos em uma request do tipo `GET`. No entanto, o `GET` não é o único método HTTP existente. Na verdade, existem 39 métodos diferentes! Os mais comuns são: `GET`, `PUT`, `POST`, `DELETE` e `PATCH`, além do método `OPTIONS`, utilizado por clientes para entender como deve ser realizada a comunicação com o servidor. A principal diferença entre os métodos é o seu significado e veremos isso na prática logo mais.

Quando um servidor recebe uma requisição, ele envia de volta uma **resposta**. Veja um exemplo:

```bash
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (aqui vêm os 29769 bytes da página solicitada)
```

A composição da resposta é definida por:

-   A versão do protocolo (1.1 no nosso exemplo);
    
-   O código do status que diz se a requisição foi um sucesso ou não. Nesse caso, deu certo, pois recebemos um código **200**, acompanhado de uma pequena mensagem descritiva (**OK**, nesse caso);
    
-   Os **headers** no mesmo esquema da requisição. No caso do exemplo acima, o **Content-Type** diz para o navegador o que ele precisa fazer. No caso do HTML, ele deve renderizar o documento na página;
    
-   Um **body** ou corpo (da requisição), que envia dados quando necessário, sendo opcional. Por exemplo, caso você submeta um formulário registrando um pedido em uma loja virtual, no corpo da resposta pode ser retornado o número do pedido ou algo do tipo. Veremos exemplos logo mais!
    

Após a resposta, a conexão com o servidor é fechada aguardando futuras requisições (seu navegador faz essa parte por você).

Note que tanto requisições quanto respostas podem ter `headers` e um `body`. No entanto, é importante não confundir uma coisa com a outra:

-   o body e os headers da **requisição** representam a informação que **um cliente está enviando para o servidor**;
-   o body e os headers da **resposta** representam a informação que **o servidor está devolvendo para o cliente**.

O nosso servidor, inclusive, poderá ser chamado de **Servidor HTTP**.

![Representacao de cliente e servidor](https://content-assets.betrybe.com/prod/Representacao%20de%20cliente%20e%20servidor.png)

Representação de cliente e servidor

## E como uma requisição envia dados para o servidor?

Existem 3 formas de nós enviarmos dados para um servidor, duas pela própria URL e uma pelo corpo da requisição.

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível no final do tópico.

### Envio por consulta, ou `req.query`

Quando pesquisamos algo no Google, usamos esse método!

-   Construção: `/rota?variavel1=valor&variavel1=valor&variavelN=valor`
-   Explicação:
    -   `/rota` é o caminho, por exemplo, `/produtos`, `/pessoas`, `/pesquisa`, …;
    -   `?` é o indicador que vamos passar dados em para a rota;
    -   `&` é o separador que se usa quando queremos enviar muitos dados;
    -   `variavelN` é uma chave identificadora, por exemplo, `nome`, `frequenciaMinima`, `q`, …;
    -   `valor` é o valor da variável, por exemplo, `nome=Tobias`, `frequenciaMinima=144`, `q=express`, …;

⏰ Hora da prática: Experimente pesquisar alguma coisa no Google e observe a mudança na URL, por exemplo: `https://www.google.com.br/search?q=Express`. Quando nós pesquisamos algo, a URL recebe a rota `/search` e o parâmetro `q` com o valor pesquisado (aqui no caso foi a palavra `Express`).

> Essa é uma requisição `GET` 😉

### Envio por parâmetro ou `req.params`

Esse exemplo é mais visível em e-commerces ou sites que têm produtos cadastrados.

-   Construção: `/rota/:variavelN`
-   Explicação:
    -   `/rota` é o caminho, por exemplo, `/produto`, `/pessoa`,, …;
    -   `/:` é o indicador que vamos passar um dado para a rota;
    -   `variavelN` é uma chave identificadora, por exemplo, `id`, …; _(aqui geralmente passamos `ids` mas não se restringe a isso)_

Um exemplo prático é quando usamos algum site de compras para ver as informações do produto, vamos usar o site da Kabum por exemplo: `https://www.kabum.com.br/produto/117767/`. Quando nós entramos para ver mais detalhes de um produto, a URL recebe a rota `/produto` e o parâmetro `117767` que é o `id` deste produto.

> Como o envio anterior, essa também é uma requisição `GET`. 😉

### Envio por corpo ou `req.body`

Este exemplo nós não vemos na barra de endereços, mas usamos muito!

Sabe quando preenchemos um formulário de pagamento após uma compra online ou entramos no course com nosso e-mail e senha? Aí está o envio de informações pelo corpo da requisição.

O envio de informações vai pelo corpo e não mais pela URL, onde podemos ver explicitamente… Isso se dá por duas questões:

-   A primeira é por segurança, que é a mais importante! Imagine sua senha ou código de segurança do seu cartão de crédito escritos na URL do seu computador e quem está perto de você podendo ler. 😱
    
-   O segundo motivo é pelo tamanho do que enviamos. Imagina que inviável enviar todo um cadastro de um formulário gigante pela URL! 😁
    

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/663ba013-3d8d-408b-b218-c956ee74a14c)

