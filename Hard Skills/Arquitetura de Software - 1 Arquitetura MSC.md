[[Arquitetura de Software]]


Ao longo dos próximos dias vamos utilizar um modelo de `arquitetura de software` chamado de `modelo baseado em camadas` o qual irá possuir três camadas denominadas de `Model`, `Service` e `Controller`. Para simplificar a nossa comunicação, a partir desse momento iremos nos referir ao modelo apenas como arquitetura `MSC`. 😉

A figura a seguir exibe uma representação visual da `arquitetura MSC`.

![Visão do modelo arquitetural MSC](https://content-assets.betrybe.com/prod/Vis%C3%A3o%20do%20modelo%20arquitetural%20MSC.png)

Visão do modelo arquitetural MSC

Iremos nos aprofundar em cada uma das camadas no momento oportuno. A seguir uma breve descrição das responsabilidades de cada uma das camadas:

-   `Model`: Essa camada tem como responsabilidade acomodar todo código capaz de acessar dados sejam eles em um banco de dados ou no sistema de arquivos. Dessa forma as demais camadas não necessitam saber de qual banco de dados, por exemplo, os dados estão sendo armazenados ou recuperados, ou seja, se utilizarmos um MySQL, um PostgreSQL ou até mesmo um MongoDB, os códigos acomodados nas camadas `Service` e `Controller` não necessitam conhecer esses detalhes;
    
-   `Service`: Essa camada tem como responsabilidade validar as regras de negócio de uma aplicação. Imagine uma `API REST` que realize o gerenciamento de um almoxarifado e que existe uma regra que diz que deve ser enviado um email para o setor de compras da empresa quando o estoque de um determinado produto estiver abaixo de uma quantidade mínima. Códigos que contêm regras desse tipo serão acomodados na camada `Service`;
    
-   `Controller`: Essa camada tem como responsabilidade validar os valores recebidos de um cliente da aplicação. Esses valores podem ser, por exemplo, um **JSON** dentro do corpo da requisição **HTTP**, parâmetros de requisição, entre outros.
    

Hoje iremos nos aprofundar na camada `Model` e as demais camadas serão abordadas de forma apropriada nos próximos dias. 😉

![Vamos que vamos-arquitetura-msc](https://content-assets.betrybe.com/prod/Vamos%20que%20vamos-arquitetura-msc.gif)
Vamos que vamos!


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/3e3b6743-ecda-46fd-a28b-9ef81ea78629)
