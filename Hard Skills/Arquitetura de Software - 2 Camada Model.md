[[Arquitetura de Software]]



A camada `Model` tem como responsabilidade acomodar as `entidades` da nossa aplicação. Como assim? 🤔

Quando os `endpoints` da API `trybecar` foram apresentados, três `entidades` foram mencionadas: pessoa motorista, pessoa passageira e viagem. As ações que a `API` fornece através dos `endpoints` se referem a essas `entidades`, ou seja, toda vez que uma ação é disparada através da `API`, ela atuará sobre os dados armazenados de pelo menos uma das `entidades` relacionadas.

Na `API` `trybecar` os dados das `entidades` estão sendo armazenados em um banco de dados **MySQL** e a camada `Model` fornece uma maneira unificada de acessar esses dados. Dessa forma, quando qualquer outra parte da aplicação necessitar dos dados de alguma entidade, existirá um `Model` que irá fornecer esses dados de maneira padronizada.

Abaixo segue o diagrama entidade relacionamento do banco de dados da aplicação `trybecar`:

![Diagrama DER da API REST trybecar](https://content-assets.betrybe.com/prod/aaea4425-9d63-4062-b55a-b465415348c0-Diagrama%20DER%20da%20API%20REST%20trybecar.png)

Diagrama DER da API REST trybecar

No repositório do projeto `trybecar` existe um arquivo chamado `script.sql` que contém as _queries_ `SQL` para a criação do banco de dados e a inserção de alguns dados que serão utilizados ao longo da seção.

A principal vantagem de utilizarmos a camada `Model` é a de unificar o acesso aos dados, evitando a duplicação de código relacionado ao acesso a dados.

#### Recursos adicionais

-   [Software Architecture Guide - Martin Fowler](https://martinfowler.com/architecture/)

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/eb5fe4aa-8d6f-4aa7-a326-6a0603f50d69)
