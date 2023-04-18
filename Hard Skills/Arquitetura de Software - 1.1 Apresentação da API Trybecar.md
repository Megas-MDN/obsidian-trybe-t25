[[Arquitetura de Software]]
[[Arquitetura de Software - 1 Arquitetura MSC]]


Antes de criar as pastas necessárias para a camada `Model`, vamos analisar uma `API REST` chamada `Trybecar` que tem como propósito gerenciar corridas entre pessoas passageiras e motoristas. Nosso objetivo será refatorar essa `API REST` de tal maneira que seu código esteja em conformidade com a `arquitetura MSC`.

E por que refatorar uma aplicação? Não seria melhor criar uma do zero? 🤔

Como pessoa desenvolvedora, dificilmente você irá criar aplicações do zero quando estiver trabalhando em uma empresa. Tenha em mente que as empresas geralmente possuem um software no qual novas funcionalidades são adicionadas ou as funcionalidades existentes passam por melhorias. Assim o processo de refatoração será uma constante durante sua carreira como pessoa desenvolvedora, e quanto mais exercitarmos essa habilidade mais confortável você estará ao se deparar com a necessidade de alterar código escrito por outras pessoas. 😉

O código completo da aplicação a ser refatorada pode ser obtido nesse [repositório](https://github.com/tryber/msc-architecture-trybecar/tree/complex-application).

⚠️ Recomendamos que você pare nesse momento e realize o clone do repositório pois ele será utilizado na aula de hoje e nas próximas aulas. 😉

O projeto `trybecar` possui a seguinte estrutura de arquivos e diretórios:

```bash
.
├── src/
│   ├── app.js
│   ├── connection.js
│   └── server.js
├── tests/
│   ├── integration/
│   │   └── -
│   └── -unit/
│       └── -
├── .env-example
├── docker-compose.yml
├── script.sql
├── thunder-trybecar.json
└── package.json
```

Os `endpoints` estão definidos no arquivo `src/app.js` sendo:

-   `POST /passengers/:passengerId/request/travel`: **Endpoint** no qual uma pessoa passageira deseja iniciar uma nova corrida. É passado como parâmetro de rota o `:passengerId` que é o `id` da pessoa passageira e um **JSON** no corpo da requisição similar ao seguinte:

```json
{
  "startingAddress": "Rua AAAA",
  "endingAddress": "Rua BBBB",
  "waypoints": [
    {
      "address": "Ponto 01",
      "stopOrder": 1
    },
    {
      "address": "Ponto 02",
      "stopOrder": 2
    },
    {
      "address": "Ponto 03",
      "stopOrder": 3
    }
  ]
}
```

-   `GET /drivers/open/travels`: **Endpoint** no qual uma pessoa motorista irá visualizar todas as viagens em aberto, ou seja, que foram criadas por pessoas passageiras mas que não possuem nenhuma pessoa motorista vinculada. O **endpoint** retorna um **JSON** similar ao seguinte:

```json
[
  {
    "id": 1,
    "passengerId": 3,
    "driverId": null,
    "travelStatusId": 1,
    "startingAddress": "Rua AAAA",
    "endingAddress": "Rua BBBB",
    "requestDate": "2022-08-22T23:34:40.000Z"
  },
  {
    "id": 2,
    "passengerId": 3,
    "driverId": null,
    "travelStatusId": 1,
    "startingAddress": "Rua XYZ",
    "endingAddress": "Rua IJK",
    "requestDate": "2022-08-22T23:35:04.000Z"
  }
]
```

-   `PUT /drivers/:driverId/travels/:travelId/assign`: **Endpoint** no qual uma pessoa motorista irá se vincular a uma viagem em aberta. É passado como parâmetros de rota o `:driverId` que é o `id` da pessoa motorista e o `:travelsId` que é o `id` de uma viagem que esteja em aberto.
    
-   `PUT /drivers/:driverId/travels/:travelId/start`: **Endpoint** no qual uma pessoa motorista irá iniciar uma viagem. É passado como parâmetros de rota o `:driverId` que é o `id` da pessoa motorista e o `:travelsId` que é o `id` de uma viagem que esteja vinculada ao motorista.
    
-   `PUT /drivers/:driverId/travels/:travelId/end`: **Endpoint** no qual uma pessoa motorista irá finalizar uma viagem em andamento. É passado como parâmetros de rota o `:driverId` que é o `id` da pessoa motorista e o `:travelsId` que é o `id` de uma viagem que esteja em andamento e vinculada a um motorista.
    

Todas as rotas citadas estão devidamente implementadas no arquivo `src/app.js`. Ao abrir esse arquivo, não se assuste! 😨 Tem muito código escrito e misturado que chega doer a vista! Mas isso é proposital! 👍

Não seguir modelos arquiteturais resultam em código escrito dessa forma, um monte de linhas que demandam muito tempo para apenas entender o que está escrito. Nossa tarefa é organizar a casa começando a criar a camada `Model`.

Isso veremos na próxima lição. 😆

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/9dd264b4-4f3f-4fd7-a580-eef0f314f518)