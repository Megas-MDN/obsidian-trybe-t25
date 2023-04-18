[[Docker]]
[[Docker - 11 Docker Compose]]

Agora que já instalamos o _Compose_, vamos criar nosso primeiro arquivo. Resumidamente, o arquivo _Compose_ é onde conseguimos especificar todos os parâmetros que antes rodávamos unitariamente utilizando `docker run`.

![E la vamos nós para mais um arquivo de receitas](https://content-assets.betrybe.com/prod/9557f11e-f2a4-4a36-9d0c-b4f067884e52-E%20la%20vamos%20n%C3%B3s%20para%20mais%20um%20arquivo%20de%20receitas.gif)
`E lá vamos nós para mais um arquivo de receitas!`

**Mapear todos os comandos e estruturá-los em um único arquivo com o _Compose_ tem diversas vantagens:**

-   Evita ter que digitar sempre vários parâmetros para executar o comando `docker run`;
-   Facilita na **ordem** de execução, caso um container seja dependente de outro;
-   Permite configurar **políticas de reinicialização**, onde dizemos ao _Compose_ o que fazer caso um container dê erro ou termine sua execução.

Toda a configuração do **Compose** é feita por meio de um arquivo `YAML`. É uma boa prática utilizar o nome `docker-compose.yaml`, porém qualquer outro nome de nossa escolha pode ser utilizado.

Agora chegou o momento onde de fato criaremos nosso primeiro arquivo `docker-compose.yaml`, conhecendo sua estrutura básica. Após isso, vamos poder finalmente orquestrar múltiplos containers em nosso computador. Vamos começar? 😉

## Estruturando nosso projeto

Nosso objetivo será criar três serviços que vão comunicar-se entre si. Vamos simular uma arquitetura muito comum com um **banco de dados**, um serviço de **back-end** e um serviço de **front-end**. Este exemplo é muito importante, pois mostrará a necessidade de utilizar o _Compose_ para gerenciar múltiplos serviços ao mesmo tempo!

A estrutura de pastas ficará desta maneira:

```bash
aula-docker-compose/
├── backend
│   └── Dockerfile
├── frontend
│   └── Dockerfile
└── docker-compose.yaml
```

Para criar a Imagem Docker do **back-end**, crie a pasta `backend` e o arquivo Dockerfile com o seguinte conteúdo:

```dockerfile
FROM betrybe/docker-compose-example-backend:v1
ENTRYPOINT ["npm", "start"]
```

Para criar a Imagem Docker do **front-end**, crie a pasta `frontend` e o arquivo Dockerfile com o seguinte conteúdo:

```dockerfile
FROM betrybe/docker-compose-example-frontend:v1
ENTRYPOINT ["npm", "start"]
```

Para o **database**, vamos usar a seguinte Imagem Docker já pronta:

-   `betrybe/docker-compose-example-database:v1`

Agora, vamos começar nosso novo arquivo: `docker-compose.yaml`!

## Versão do Arquivo _Compose_

Todo arquivo `docker-compose.yaml` deve iniciar com a chave `version`. Dessa maneira, definimos qual versão deverá ser utilizada pelo _Compose_ para interpretar o arquivo, evitando assim que o `docker-compose.yaml` fique incompatível com versões mais recentes da ferramenta.

> 👀 **De olho na dica:** você pode consultar as especificações de cada versão [neste link](https://docs.docker.com/compose/compose-file/compose-versioning/#versioning).

Aqui utilizaremos a versão `3` do _Compose_. Sendo assim, nosso arquivo `docker-compose.yaml` começa da seguinte maneira:

```yaml
version: '3'
```

## Criando Serviços

No _Compose_ existe o conceito de `services`. Logo, vamos configurar nosso arquivo _Compose_ com os três serviços que citamos acima.

> ⚠️ A ordem dos serviços neste arquivo não é importante._

```yaml
version: '3'
services:
  frontend:
    [...]
  backend:
    [...]
  database:
    [...]
```

Perceba que aqui apenas atribuímos nomes aos nossos serviços, porém não especificamos o que deverá ser executado ainda.

Lembre-se que todo _container_ é criado a partir de uma _imagem_. Sendo assim, precisamos especificá-las aos nossos serviços. Temos duas opções para isso:

1️⃣ `image`: especifica uma imagem Docker **pronta**, seja local ou a ser baixada no _Docker Hub_;

2️⃣ `build`: especifica a **pasta** contendo um arquivo `Dockerfile` a partir do qual o _Compose_ vai executar o comando `docker build` automaticamente.

Em nosso exemplo, construiremos as três partes da aplicação a partir de imagens Docker de exemplo já disponíveis no _Docker Hub_. Portanto, usaremos a opção `image` para o serviço de **database** e a opção `build` para os serviços de **backend** e **frontend**. Nosso `docker-compose.yaml` ficará assim:

```yaml
version: '3'
services:
  frontend:
    build: frontend/    # Especificamos o contexto, ou seja, a pasta onde está o Dockerfile.
  backend:
    build: backend/     # Mesmo caso aqui.
  database:
    image: betrybe/docker-compose-example-database:v1    # Especificamos a Imagem Docker diretamente.
```

Nosso arquivo vai funcionar como se estivéssemos executando o comando `docker build` para o **back-end** e o **front-end**. Logo depois, três vezes o comando `docker run`, uma vez para cada serviço.

## Mapeamento de Portas

A próxima configuração importante de cada serviço é o **mapeamento de portas**. Vimos nos conteúdos anteriores como realizar este mapeamento no comando `docker run` ao utilizar a flag `-p <porta-do-computador>:<porta-do-container>`. Dentro de cada serviço, podemos especificar o `ports`, que é uma **lista de mapeamentos de portas entre o computador local e as portas do container**.

Em nosso exemplo, a imagem Docker do front-end expõe a porta **3000**, enquanto a imagem Docker para o nosso back-end expõe a porta **3001**. O formato da especificação é exatamente como utilizamos na flag `-p`. Logo, nosso arquivo ficará assim:

```yaml
version: '3'
services:
  frontend:
    build: frontend/
    ports:
      - 3000:3000
  backend:
    build: backend/
    ports:
      - 3001:3001
  database:
    image: betrybe/docker-compose-example-database:v1
```

> 📝**Anote aí**: o primeiro parâmetro é sempre a porta do computador local e o segundo parâmetro é a porta exposta no container.

## E se o container apresentar um problema?

Quando estamos trabalhando com vários containers ao mesmo tempo, é possível que algum deles encontre problemas e **pare de funcionar**. Quando utilizamos apenas o Docker, precisamos parar o que estamos fazendo, investigar o problema e tentar executar o container novamente.

Entretanto, o _Compose_ nos permite configurar uma **política de reinicialização**! 🤔

Seu uso é **simples**! Dizemos ao _Compose_ o que ele deve fazer caso um container pare sua execução, de maneira automática! Devemos configurar este comportamento através da chave `restart`.

O _Compose_ possui quatro políticas de reinicialização, sendo elas:

-   `no` : define que o container não reiniciará automaticamente (Padrão);
-   `on-failure`: define que o container será reiniciado caso ocorra alguma falha apontada pelo `exit code`, diferente de zero;
-   `always`: especifica que sempre que o serviço parar, seja por um falha ou porque ele simplesmente finalizou sua execução, ele deverá ser reiniciado;
-   `unless-stopped`: define que o container sempre será reiniciado, **a menos que** utilizemos o comando `docker stop <container>` manualmente.

É importante especificarmos este valor, principalmente se utilizarmos o _Docker Compose_ em ambiente de produção.

Com a adição dessa configuração, nosso arquivo `docker-compose.yaml` estará assim:

```yaml
version: '3'
services:
  frontend:
    build: frontend/
    restart: on-failure
    ports:
      - 3000:3000
  backend:
    build: backend/
    restart: on-failure
    ports:
      - 3001:3001
  database:
    image: betrybe/docker-compose-example-database:v1
    restart: on-failure
```

## Usando Variáveis de Ambiente

Uma **variável de ambiente é um recurso disponível nos `sistemas operacionais` que permite criar uma variável no formato `NOME_DA_VARIÁVEL=VALOR`. Onde `NOME_DA_VARIÁVEL` é o nome da variável de ambiente, e `VALOR` se refere a um valor que será vinculado à variável**. Toda vez que solicitarmos ao `sistema operacional` o valor de uma variável de ambiente, fornecemos a ele uma `NOME_DA_VARIÁVEL` e ele retorna o `VALOR` associado a esta chave, se ela estiver definida.

Para exemplificar, ao digitar o seguinte comando no console:

```bash
echo $USER
```

Agora será apresentado o valor da variável de ambiente `$USER`, cujo valor é o nome de usuário da pessoa que está utilizando o sistema no momento da execução.

Veja abaixo um exemplo de saída deste comando:

```bash
1# echo $USER
2bruno
```

É possível criar e usar **variáveis de ambiente** dentro dos containers. O nome da chave que utilizamos é `environment`. Com esta chave, configuramos as variáveis de ambiente em nossos serviços do _docker-compose_. Podemos especificar no arquivo _docker-compose_ para que ele utilize o conteúdo de variáveis de ambiente do nosso próprio computador!

Em nosso arquivo de exemplo, vamos precisar passar para nosso back-end o nome do serviço onde o banco de dados vai rodar, em uma variável chamada `DB_HOST`. Logo, nosso arquivo de exemplo ficará assim:

```yaml
version: '3'
services:
  frontend:
    build: frontend/
    restart: on-failure
    ports:
      - 3000:3000
  backend:
    build: backend/
    restart: on-failure
    ports:
      - 3001:3001
    environment:
      - DB_HOST=database
  database:
    image: betrybe/docker-compose-example-database:v1
    restart: on-failure
```

O serviço `backend` agora possui uma variável de ambiente chamada `DB_HOST`, uma referência ao serviço `database` que poderá ser utilizada pelo servidor para se conectar ao banco de dados.

Simples não? 🧐

> **Anota aí 🖊:** A ideia de variáveis de ambiente é trazer mais dinamismo entre ambientes. Por exemplo: Na maioria das empresas, usualmente temos o ambiente de **teste** e o ambiente de **produção**, esses dois ambientes possuem nome de pessoa usuária e senha diferentes para cada ambiente. Deixar esses dados fixos ou expostos no código, engessaria a aplicação e seria inseguro. As variáveis de ambiente entram para reduzir esse problema. Tendo variáveis com o mesmo nome em cada ambiente, por exemplo `DB_USER` e `DB_PASSWORD`. Em cada ambiente a aplicação consegue se conectar em banco de dados diferentes, **isolando assim o ambiente de teste e o de produção**.

## Dependência entre Serviços

Uma configuração importante para garantir a ordem de inicialização e encerramento dos nossos serviços é a chave `depends_on`. Com esta chave, conseguimos criar **dependências entre os serviços**! 🤨

Para entendermos melhor os comportamentos desta chave, vamos voltar para nosso arquivo e ver as novas alterações aplicadas:

```yaml
version: "3.8"
services:
  frontend:
    build: frontend/
    restart: on-failure
    ports:
      - 3000:3000
    depends_on:
      - backend
  backend:
    build: backend/
    restart: on-failure
    ports:
      - 3001:3001
    environment:
      - DB_HOST=database
    depends_on:
      - database
  database:
    image: betrybe/docker-compose-example-database:v1
    restart: on-failure
```

Cada serviço do nosso arquivo `docker-compose.yaml` recebeu a chave `depends_on`, que é uma lista de quais serviços o _Compose_ deve executar primeiro, antes de executar o serviço atual. Nesse exemplo, os serviços serão iniciados respeitando a ordem que especificamos: primeiro o serviço `database` será iniciado, depois o serviço `backend` e finalmente o serviço `frontend`!

Agora que criamos nosso primeiro arquivo _Compose_, está na hora de finalmente executá-lo e orquestrar nossos containers! Bora lá? 🐋


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/2f1a5c4d-74b1-488a-8d9b-408682c93724/lesson/1ad977dd-5f74-4ff0-a2db-119b30242d32)