[[Docker]]
[[Docker - 11 Docker Compose]]

Você acompanhou durante todo este conteúdo que nos referimos aos containers criados pelo _Compose_ como **serviços**. Mas qual a diferença na prática entre o _container_ e _service_? 🤔

![Qual é o certo Service Container](https://content-assets.betrybe.com/prod/Qual%20%C3%A9%20o%20certo%20Service%20Container.gif)

Qual é o certo? Service? Container?

Até o momento, os nossos exemplos estavam mapeando um serviço para apenas um container, mas isso **nem sempre é verdade**! Em ambientes de produção, temos que garantir que nossas aplicações tenham **alta escalabilidade**, ou seja, a aplicação deve ser capaz de receber uma alta carga de requisições sem maiores problemas durante horários de pico.

E é por este motivo que normalmente temos **múltiplas cópias** dos nossos containers atendendo o mesmo **serviço**! Chamamos a quantidade de cópias de um container como o número de **réplicas** atuais do serviço. Ainda não está nítido? Confira melhor na figura abaixo!

![Diferença entre serviços e containers](https://content-assets.betrybe.com/prod/Diferen%C3%A7a%20entre%20servi%C3%A7os%20e%20containers.png)

Diferença entre serviços e containers

O comando `docker-compose up` aceita a flag `--scale service=<número-de-replicas>`, onde podemos configurar a quantidade de réplicas para um serviço. Entretanto, esta opção normalmente é utilizada em ambientes de produção e não é necessária para nossos estudos agora.

> 🧠 **Lembre-se**: o _Compose_ chama os containers orquestrados de **serviço** para possibilitar a criação de várias réplicas, desde que a situação se mostre necessária para isso. Em nossos estudos na Trybe, podemos chamar serviço de container e vice-versa, ok? 🤓

## Outros orquestradores de containers

E ai, o que achou de tudo o que aprendeu? Dependendo do cenário, o _Compose_ é uma **ótima ferramenta** para orquestrar nossos containers! Mas não é a única opção! Existem vários projetos focados apenas em **orquestrar containers** e alguns nomes podem ser familiares para você:

-   **Kubernetes**: projeto de código aberto de orquestração de containers, mantido pela [CNCF](https://www.cncf.io/);
-   **OpenShift**: projeto de código aberto de orquestração de containers, mantido pela _Red Hat_;
-   **Docker Swarm**: projeto da empresa Docker Inc. para orquestrar containers;
-   **AWS Elastic Container Service** : serviço pago da Amazon para orquestrar containers.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/2f1a5c4d-74b1-488a-8d9b-408682c93724/lesson/ef152506-8e4b-474e-9bcf-9836061afbe6)