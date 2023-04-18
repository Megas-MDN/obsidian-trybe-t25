[[Node]]

Para falarmos sobre arquitetura REST, precisamos antes entender o que é REST e RESTful:

-   `REST` é um conjunto de boas práticas utilizadas durante a construção de uma API;
-   `RESTful` é um serviço web (desenvolvido por nós ou não) que segue as regras definidas pelo REST;

Dessa forma, não há diferenças entre as duas palavras, mas sim uma relação de complemento.

A palavra `REST` tem origem do inglês e significa _Rest Representational State Transfer_. Em português, podemos traduzir como _Transferência de Estado Representacional_ (~~não que tenha ajudado muito~~). Em suma, REST é um estilo arquitetural definido pelo [W3C](https://www.w3c.br/), que estabelece um conjunto de restrições sobre como uma API deve, idealmente, funcionar.

## As 5 restrições para ser RESTful

Como o foco desse conteúdo não é a construção de APIs RESTful em detalhes, inclusive é um assunto que vai longe! Veja as cinco principais restrições REST com descrições simplificadas do que significam.

1.  Interface uniforme (Uniform Interface): respeitar um padrão para transferir informações;
2.  Arquitetura cliente-servidor: o REST quer nossa API organizada de forma que ela sirva a clientes gerenciando suas solicitações HTTP;
3.  Sem estado (stateless): entre uma requisição e outra, a API não armazena informações do cliente. Todas as requisições são independentes;
4.  Cacheable: requisições repetidas podem ser otimizadas, pois retornam os mesmos resultados;
5.  Sistema em camadas (Layered System): quem faz a requisição não vê as várias partes que fazem uma API - só a sua camada que gerencia requisições.

Aqui, vale ressaltar que você só precisa aplicar todas elas caso queira ser RESTful, mas esse padrão **não é bala de prata**. Se sua API for simples e resolver seu problema como estiver, não é necessário utilizar todas.

De olho na dica👀: Cenários diferentes exigem soluções diferentes e no desenvolvimento software nada é escrito em pedra, ou seja, os princípios podem ser quebrados, desde que a justificativa para tal seja **plausível**.

> ⚠️ Aviso: Sabemos que são muitas informações e em várias delas não vamos entrar no detalhe! O mais importante aqui é sair sabendo da existência de padrões e não decorá-los, pois ao longo do curso vamos usá-los e treiná-los. Lembre-se, esses são apenas os primeiros conteúdos de back-end que você está vendo, então, vá com calma! 🚀

Antes de achar os princípios muito complicados, veja como implementamos esse padrão usando Express. Você se surpreenderá.

## REST no Express

De modo geral, os princípios devem ser seguidos independente da tecnologia que utilizamos na implementação de nossa API. Ela pode ser escrita em `Node.js`, `Python`, `Perl`, `Java`, entre outras.

Uma das vantagens de se usar o Express para construção de APIs é a organização das rotas, podendo separar as rotas pelo método (ou verbo) HTTP da requisição. Além disso, torna-se mais simples retornar um formato específico solicitado pelo cliente e/ou retornar um status HTTP.

```js
app.get(...)
app.post(...)
app.put(...)
app.delete(...)
```

Esse é o pulo do gato! Durante a explicação do conteúdo usamos a arquitetura REST em nossa API! 😮

A forma como você aprendeu a fazer APIs hoje **já é** RESTful! Contudo, se tornar especialista em RESTful e saber analisar APIs para ver se respeitam o padrão não é nosso propósito aqui. Basta saber que existem requisições que definem boas práticas para criações de alguns tipos de API.

De olho na dica 👀: As soluções que você aprenderá a criar nos próximos dias irão respeitá-las. Tome nota dessa página e volte aqui de tempos em tempos - você vai ver como sempre buscamos respeitar essas restrições.

E com isso, obtivemos todas as habilidades do dia! Você agora leu sobre como “_Descrever_ uma API REST”.


#### Recursos adicionais

-   [O que é uma API REST?](https://www.redhat.com/pt-br/topics/api/what-is-a-rest-api)
-   [Roteamento no Express - Express](https://expressjs.com/pt-br/guide/routing.html)
-   [Introdução Express/Node - MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Express_Nodejs/Introduction)
-   [Status code - MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status)
-   [O que é API REST - Red Hat](https://www.redhat.com/pt-br/topics/api/what-is-a-rest-api)
-   [REST no glossário - MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Glossary/REST)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/de8f8a05-bc79-4cfb-a06d-482e8c77641a)