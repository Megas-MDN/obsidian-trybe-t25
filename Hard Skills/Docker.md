[[Banco de Dados]]

ROM nginx:1.21-alpine AS primeiro-estagio
WORKDIR /site

COPY config.toml config.toml
COPY index.html /site/layouts/index.html
COPY _index.md /site/content/_index.md

RUN apk add hugo
RUN hugo --minify --gc
RUN mv /site/public/* /usr/share/nginx/html

ENTRYPOINT ["nginx", "-g", "daemon off;"]
### Introdução

Chegou o momento de entender como utilizamos essa ferramenta e qual é a importância dela. Você também aprenderá a fazer a instalação do Docker, entenderá a diferença entre `imagens` e `containers`, além de rodar seu primeiro container Docker, o `hello-world`!


## Por que isso é importante?

Enquanto pessoas desenvolvedoras é comum nos depararmos com diversas ferramentas e tecnologias, tendo que lidar com uma quantidade significativa de ambientes distintos durante o ciclo de desenvolvimento. Por exemplo, temos:

1.  o ambiente **local**, que é o computador que usamos para desenvolver;
2.  o ambiente de **`staging`**, que utilizamos para testar e validar as funcionalidades;
3.  o ambiente de **produção** acessado pelas pessoas usuárias do produto.

Esse cenário exige que sejam feitas a **preparação e configuração de todo o ambiente** com as tecnologias necessárias, além de fazê-las funcionar em conjunto.

Fazer isso nem sempre é uma tarefa simples! O processo se torna ainda mais complexo quando há múltiplos ambientes, distintos entre si, e também há a necessidade de rodar em diversas máquinas _(desde sua máquina pessoal local, servidores externos pagos, ou mesmo uma [máquina virtual](https://pt.wikipedia.org/wiki/M%C3%A1quina_virtual#:~:text=Na%20ci%C3%AAncia%20da%20computa%C3%A7%C3%A3o%2C%20m%C3%A1quina,isolada%20de%20uma%20m%C3%A1quina%20real%E2%80%9D.))_ que, muitas vezes, **possuem configurações e utilizam sistemas operacionais diferentes**.

Por isso, além de nos preocuparmos com o código, temos que fornecer as dependências necessárias para rodá-lo em diferentes configurações. A partir disto surge a famosa frase:

![[docker.gif]]

Essa frase é famosa justamente porque precisamos lidar com os diferentes cenários citados até aqui.

Por exemplo, se uma pessoa desenvolve utilizando uma distribuição ‘A’ de Linux, outra utiliza Windows e outra Mac e no servidor roda uma distribuição ‘B’ de Linux, todas elas estão trabalhando no **mesmo projeto**, e da mesma forma, pois estão disponibilizando-o para o ambiente de produção, em um servidor remoto comum, conhecido como **processo de _deploy_ ou implantação**.

Além dos diferentes sistemas operacionais, é comum que existam softwares, ferramentas e dependências distintas ou com versões diferentes em cada máquina. Dessa maneira, **é muito difícil garantir que o que funciona na máquina de uma pessoa funcionará na máquina de outra** sem a necessidade de fazer novas configurações. Inclusive, não conseguimos nem garantir que também funcionará nos servidores durante o processo de _deploy_.

Para resolver estes problemas de complexidade e de compatibilidade, bem como economizar o tempo no processo de preparação de uma máquina para rodar um programa específico, foi criado o **Docker**. 🐋

![[Pasted image 20230110131136.png]]

Com o Docker também conseguimos simular e testar facilmente um ambiente completo, de maneira leve e inteligente, em questão de minutos, podendo replicar tais configurações para outra máquina com facilidade, além de conseguir **trabalhar com nossas aplicações em escala** de forma simples!

Portanto, por meio do Docker resolvemos o problema de incompatibilidade com outros sistemas, dado que ele funciona como uma espécie de “empacotador” de todas essas dependências e requisitos para que sua aplicação funcione em qualquer ambiente! **Isso torna simples sua disponibilização!**

Por todas essas vantagens, o Docker ganhou muito espaço e seu uso é cada vez mais comum!

As maiores empresas de tecnologia utilizam o Docker para manter grandes arquiteturas, assim como as pequenas empresas utilizam de suas facilidades para manter suas aplicações no ar de forma simples e com menos custos.

[Se olharmos o _Google Trends_](https://trends.google.com.br/trends/explore?date=2013-01-01%202019-01-01&geo=BR&q=%2Fm%2F0wkcjgj) _(dados sobre pesquisas no Google)_, começando pelo ano de lançamento do Docker (2013) até o fim da década (2019), conseguimos ter um bom indicador dessa popularidade por meio do número de pesquisas pelo software “Docker” nesse período. Muito disso se deve ao conceito de “conteinerização” de aplicações, que é adotado por muitas tecnologias atualmente.

![[Pasted image 20230110131217.png]]

Dessa forma, é essencial saber _Docker_, tanto para se adequar ao mercado como para aproveitar seus benefícios durante o ciclo de vida de nossas aplicações.


-   [Documentação Docker](https://docs.docker.com/)
-   [Docker - Limpando contêineres, imagens e volumes](http://www.macoratti.net/19/02/dock_limp1.htm)
-   [Documentação oficial do Docker - About storage drivers](https://docs.docker.com/storage/storagedriver/)
-   [Docker Layers Explained](https://dzone.com/articles/docker-layers-explained)
-   [Documentação oficial do Docker - Docker images](https://docs.docker.com/engine/reference/commandline/images/)
-   [Documentação oficial do Docker - Dockerfile](https://docs.docker.com/engine/reference/builder/)
-   [Docker - Limpando contêineres, imagens e volumes](http://www.macoratti.net/19/02/dock_limp1.htm)
-   [Docker Layers Explained](https://dzone.com/articles/docker-layers-explained)
-   [Documentação oficial do Docker - Docker images](https://docs.docker.com/engine/reference/commandline/images/)
-   [Documentação oficial do Docker - Dockerfile](https://docs.docker.com/engine/reference/builder/)


Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/a852c0dd-0602-4357-88e8-707352e97927/lesson/f8c01b36-6180-4b7e-905c-0b8645155889)


