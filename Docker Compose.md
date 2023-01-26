[[Docker]]

Chegou o momento de aprender a configurar um ambiente com vários containers de maneira mais simples e prática. Faremos isso com o uso da ferramenta **Docker Compose** (que chamaremos apenas de _Compose_).

Em um ecossistema de aplicações com várias linguagens de programação e tecnologias distintas rodando em seus respectivos containers, o _Compose_ entra como uma solução para organizar o funcionamento e a configuração de todas essas partes que compõem uma arquitetura.

![Compose gerenciando nossos Containers Docker](https://content-assets.betrybe.com/prod/Compose%20gerenciando%20nossos%20Containers%20Docker.gif)
`Compose gerenciando nossos Containers Docker`

Usando o _Compose_, definimos em um arquivo de configuração `YAML` todos os detalhes para executar nosso ambiente de desenvolvimento local, aproveitando todas as vantagens que o `Docker` oferece, porém sem se preocupar em subir cada um dos containers que envolvem uma aplicação com seus parâmetros específicos no `run`.

Do mesmo jeito que comparamos o `Dockerfile` a uma receita para construir imagens Docker, podemos dizer que o arquivo _Compose_ também é uma receita, a qual indica todos os componentes que serão utilizados e também em que **ordem** cada container deve ser executado.

Além disso, nossos ambientes geralmente possuem vários serviços que precisam se comunicar entre si. Por exemplo, um back-end com um front-end ou um serviço com um banco de dados. Nesse contexto, saber como trabalhar com o conceito de **redes** é muito vantajoso por nos permitir lidar com essa comunicação entre containers mais facilmente.

Outro recurso importante que também precisamos entender são os **volumes**. Eles são componentes do Docker responsáveis por preservar uma pasta dentro do container, **mesmo se ele terminar sua execução**. Isso é muito útil, pois é comum precisarmos de soluções para que os dados ou arquivos (como em um banco de dados) possam persistir entre uma execução e outra de container.

Esses componentes junto à própria ferramenta _Compose_ nos permitem criar todo o nosso ambiente de maneira simples, utilizando todos os recursos e vantagens do Docker. Isso garantirá que mesmo que nosso ambiente tenha diversos serviços, como APIs, front-ends, banco de dados, entre outros, conseguiremos integrá-los, permitindo que tudo isso rode em qualquer ambiente com Docker. Com isso, nossas aplicações passam a ser publicadas de forma descomplicada e mais eficiente (parece um sonho, mas é realidade). ⭐

## Instalação do Compose

Vamos começar colocando a mão na massa! Fazer a instalação da ferramenta _Compose_ é bem simples, mas antes certifique-se que você já possui o próprio **Docker** instalado.

-   Caso você esteja utilizando `Windows` ou `Mac`, o _Docker Compose_ já é instalado junto com o próprio `Docker Desktop`. Os passos para a instalação podem ser conferidos nos links abaixo:
    
    -   [Windows](https://docs.docker.com/desktop/windows/install/)
    -   [Mac](https://docs.docker.com/desktop/mac/install/)
-   Caso esteja utilizando alguma distribuição `Linux`, basta usar o seguinte comando para realizar a instalação:
    

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Por padrão, binários baixados da Internet não possuem permissão de execução. Logo, basta usar o programa `chmod` para aplicar a permissão de execução (`+x`) ao binário que acabamos de baixar. Execute o seguinte comando no seu terminal:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

Para validar a instalação basta executar o comando `docker-compose --version`. Se tudo ocorrer bem, você verá a seguinte saída em seu terminal:


```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose --version
docker-compose version 1.25.0, build unknown
pessoa@trybe:~/aula-docker-compose$
```

Depois disso, devem ser exibidos os detalhes da versão instalada em seu terminal.

> 👀 **De olho na dica:** para ter mais detalhes sobre o Compose (ou caso ocorra algum erro) consulte o [guia oficial](https://docs.docker.com/compose/install/#install-compose).


-   [Documentação oficial do Docker - Use volumes](https://docs.docker.com/storage/volumes/)
-   [Configurando opções de rede dos containers](https://www.youtube.com/watch?v=pKJgQmXXryg)
-   [Manage sensitive data with Docker secrets](https://docs.docker.com/engine/swarm/secrets/)
-   [Overview of Docker Compose](https://docs.docker.com/compose/)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/2f1a5c4d-74b1-488a-8d9b-408682c93724/lesson/170b7b6e-925c-40e8-9d0a-08e41f599ec5)