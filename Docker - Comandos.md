[[Docker]]

Chegou a hora de finalmente conhecermos os comandos básicos de interação com o Docker, através do CLI.

> ⚠️ os comandos feitos através do **CLI** são enviados para a **API** interna do Docker, que, por sua vez, envia os comandos para o **Daemon**.

📝 **Anote aí:** Alguns pontos importantes antes de começar:

-   `docker <comando> <subcomando> <parâmetros>` é o formato padrão para comandos não-abreviados no CLI;
    
-   Utilize o parâmetro `--help` no `<comando>` ou `<subcomando>` para ter a relação completa do que pode ser executado a partir deles;
    
    -   Exemplo: `docker container --help` ou `docker container run --help`.
-   Os `<parâmetros>` são opcionais na execução dos comandos;
    
-   O conteúdo faz referência à [documentação oficial](https://docs.docker.com/engine/reference/commandline/docker/) do Docker.
    
-   -   Nos exemplos desta seção, nós usaremos imagens Docker que **já foram construídas e publicadas** no Docker Hub de maneira pública. Em um próximo momento, vamos aprender como criar nossas próprias imagens Docker e executá-las como containers!

## Listando imagens

Primeiro, vamos aprender a visualizar as imagens Docker em nosso computador! Veremos o nome, sua data de criação e seu tamanho em disco.

➡️ Utilize o comando `docker images` para visualizar todas as imagens Docker que já estão presentes em sua máquina.

-   Ao tentar executar um container com uma imagem específica e esta imagem não estiver presente em nossa máquina, o Docker por padrão **tentará obter a imagem Docker através do seu Registry**, o Docker Hub. Veja um exemplo de saída do comando em uma máquina sem nenhuma imagem:


```bash
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

-   Agora, veja um exemplo de saída do comando com uma máquina com várias imagens Docker:

```bash
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
python       3.10      de1ec279ff75   14 hours ago   919MB
alpine       3.14      e04c818066af   2 weeks ago    5.59MB
```

>Isso significa que se tentarmos executar um container utilizando essas imagens e com essas tags, o Docker **utilizará a versão presente na máquina**, e não tentará obtê-la novamente do Docker Hub.

## Listando containers

➡️ Utilize o comando `docker ps` ou o comando mais novo, o `docker container ls`, para listar todos os containers em execução neste momento em sua máquina.

-   Veja o exemplo abaixo em uma máquina que **não há nenhum container** em execução no momento:

```bash
pessoa@trybe:~/course$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~/course$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

-   Agora, veja o exemplo de saída abaixo quando temos alguns containers em execução no momento:

```bash
pessoa@trybe:~/course$ docker container ls
CONTAINER ID   IMAGE         COMMAND        CREATED          STATUS          PORTS     NAMES
1cc75e507cd0   alpine:3.14   "sleep 5000"   7 seconds ago    Up 6 seconds              angry_mirzakhani
9a38f7a32b42   python:3.10   "sleep 5000"   15 seconds ago   Up 15 seconds             hungry_yonath
```

Entretanto, por padrão, o comando `docker ps` **não exibe containers que foram parados ou que terminaram sua execução**. Para visualizar todos os containers atuais, incluindo os que estão em execução e também parados, é necessário utilizar a flag `-a`. Veja o exemplo de saída do comando abaixo:

```bash
pessoa@trybe:~/course$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND        CREATED          STATUS          PORTS                  NAMES
1cc75e507cd0   alpine:3.14   "sleep 5000"   7 seconds ago    Up 6 seconds                           angry_mirzakhani
9a38f7a32b42   python:3.10   "sleep 5000"   15 seconds ago   Up 15 seconds                          hungry_yonath
14a00a2e09c9   alpine:3.14   "/bin/sh"      12 minutes ago   Exited (0) 12 minutes ago              meu-container
```

Acabamos de explicar como verificar a lista de imagens e lista de containers, pois nos próximos exemplos nós vamos usar estes mesmos comandos em conjunto com os novos comandos que vamos aprender. 👀

## Executando um novo container

➡️ Utilize o comando `docker container run <flags>? <imagem>:<tag> <argumentos>?` para executar um container utilizando a imagem identificada pelo `<imagem>:<tag>`.

-   O exemplo abaixo executa um container usando a imagem Docker `alpine` e a tag `3.14`:

```bash
pessoa@trybe:~/course$ docker container run alpine:3.14 echo "Hello World"
Unable to find image 'alpine:3.14' locally
3.14: Pulling from library/alpine
8663204ce13b: Pull complete
Digest: sha256:06b5d462c92fc39303e6363c65e074559f8d6b1363250027ed5053557e3398c5
Status: Downloaded newer image for alpine:3.14
Hello World!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
52712fa829f0   alpine:3.14   "echo 'Hello World'"   19 seconds ago   Exited (0) 19 seconds ago             xenodochial_kapitsa
```

> ⚠️ Os parâmetros `<flags>?` e `<argumentos>?` são **opcionais** (o que é sinalizado pelo uso de `?`), porém vamos aprender seu uso mais adiante.

### Recapitulando 🧠

**Vamos entender passo-a-passo tudo o que aconteceu durante a execução do comando anterior:**

1.  Pedimos para o Docker criar um novo container, baseado na imagem chamada `alpine`, usando a tag `3.14` e passando os argumentos `echo` e `"Hello World"`;
2.  O Docker verifica se já temos esta imagem, com esta tag, no disco da máquina;
3.  **Se a imagem não é encontrada**, o Docker imprime na tela a mensagem `Unable to find image 'alpine:3.14' locally` e começa a baixar a imagem do Docker Hub;
4.  Com a imagem e a tag presentes no disco da máquina, o Docker cria um processo isolado e utiliza a imagem Docker como o “disco” base para este processo;
5.  Como estamos subindo este container passando os argumentos `echo` e `"Hello World"`, o comportamento padrão da imagem `alpine` é executar este comando. Por isso, nós vemos a saída `Hello World` no terminal!
6.  Ao executar o comando `docker ps -a`, verificamos que o container foi criado, porém ele já terminou sua execução e ficou com o status `Exited`.

> **Curiosidade:** a imagem `alpine` é uma imagem Docker especial, pois é muito pequena _(apenas 5.59MB)_ e já possui os comandos básicos de uma distribuição Linux. Nos próximos exemplos abaixo vamos utilizar bastante essa imagem por ser pequena e prática de usar!

> ⚠️ **Atenção**: veja que o Docker atribuiu um nome aleatório para o nosso container. O Docker segue a seguinte regra para dar um nome a um novo container: `<adjetivo>_<nome>`. Entretanto, podemos utilizar a flag `--name <nome-da-sua-escolha>` para dar um **nome específico** ao container criado, em vez de obter um nome aleatório dado pelo Docker.

Veja um exemplo abaixo onde nós utilizamos a flag para dar o nome `meu-container` para o novo container que desejamos executar:


```bash
pessoa@trybe:~/course$ docker container run --name meu-container alpine:3.14 echo "Hello World 2"
Hello World 2!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
6b3491ce9502   alpine:3.14   "echo 'Hello World 2'" 11 seconds ago   Exited (0) 11 seconds ago             meu-container
52712fa829f0   alpine:3.14   "echo 'Hello World'"   2 minutes ago    Exited (0) 2 minutes ago              xenodochial_kapitsa
```

Perceba que o container do exemplo anterior chamado `xenodochial_kapitsa` não foi removido, mesmo que sua execução já tenha sido encerrada. Este é o comportamento padrão do Docker, pois ao terminar a execução, o container ainda permanece disponível para ser executado novamente.

Você pode remover os containers exemplificados acima usando o comando `docker rm <nome-do-container>`.

> 📝 **Anote ai:** um container só pode ser removido com o comando `docker rm <nome-do-container>` se ele estiver parado ou tiver sua execução terminada**.

Vamos remover os dois containers mostrados anteriormente e verificar a lista de containers novamente:

```bash
pessoa@trybe:~/course$ docker rm xenodochial_kapitsa
xenodochial_kapitsa
pessoa@trybe:~/course$ docker rm meu-container
meu-container
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
```

> Note que a lista de containers está está vazia agora!

## Modo “auto-remover”

Este modo é útil para testar várias imagens Docker sem ficar com uma lista de containers parados. A flag `--rm` indica para o Docker que desejamos que um container seja removido ao final da sua execução. Veja abaixo um exemplo do uso da flag:

```bash
pessoa@trybe:~/course$ docker container run --rm alpine:3.14 echo "Hello World 3"
Hello World 3!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

Perceba que após criar um container com a imagem `alpine:3.14` e executar o comando de listar os containers (com a flag `-a`), não há nenhum container atualmente na máquina. Isso significa que o container criado pelo comando `docker run` executou, terminou sua execução e o Docker já fez a remoção deste container automaticamente.

> ⚠️**Importante:** a flag `--rm` vai remover apenas o **container**! A imagem `alpine:3.14` ainda estará presente na máquina. Podemos confirmar isso executando o comando `docker images`. Veja abaixo a saída ao executar os três comandos em sequência:

```bash
pessoa@trybe:~/course$ docker container run --rm alpine:3.14 echo "Hello World 4"
Hello World 4!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
alpine       3.14      e04c818066af   2 weeks ago    5.59MB
```

## Modo “segundo plano”

A flag `-d` ou `--detach` faz com que a execução do container ocorra em **segundo plano**, ou seja, embora não esteja visível, o container executará de forma assíncrona. Esta opção é interessante quando o programa a ser executado é um servidor ou algum processo que você sabe previamente que terá uma execução demorada.

Veja abaixo a saída ao executar um container no modo **detached**. Neste exemplo, trocamos o argumento `echo` pela execução do programa `sleep`, que fará com que o container continue sua execução por 300 segundos (5 minutos):

```bash
pessoa@trybe:~/course$ docker container run --rm -d alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3e
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
81e61d38ca40   alpine:3.14   "sleep 300"   12 seconds ago   Up 12 seconds             amazing_thompson
```

Perceba que ao executar o comando `docker ps` para visualizar os containers em execução atualmente, vemos nosso novo container executando o comando `sleep 300`. Porém, o container está sendo executado em **segundo plano**, por isso ele não travou a utilização do nosso terminal pelo uso da flag `-d`.

Para forçar a parada de execução do container acima, podemos usar o comando `docker stop <nome-do-container>`. Este comando força o container a terminar sua execução atual. Veja a seguir a saída ao executar o comando, usando o nome do container que obtivemos no exemplo acima:

```bash
pessoa@trybe:~/course$ docker container run --rm -d alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3e
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
81e61d38ca40   alpine:3.14   "sleep 300"   12 seconds ago   Up 12 seconds             amazing_thompson
pessoa@trybe:~/course$ docker stop -t 0 amazing_thompson
amazing_thompson
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
```

> **Curiosidade:** o comando `docker stop` envia um pedido _educado_ (chamado internamente de `SIGTERM`) ao container para que ele tenha tempo de encerrar tudo o que precisa antes de parar sua execução de fato. Entretanto, o comando `sleep` que estamos utilizando **ignora esse pedido educado do Docker**. Para que o pedido seja forçado (chamado internamente de `SIGKILL`), vamos utilizar a flag `-t 0`.

Pronto! Conseguimos forçar a paralisação de um contêiner de segundo plano utilizando o comando `docker stop`.

_Mas e se quiséssemos nos conectar no terminal dentro do container, enquanto ele está em execução?_ 🤔

Para isso, vamos conhecer os **comandos avançados** do Docker! 🐋


## Comandos avançados no Docker

## Acessando o terminal do container

O Docker nos permite executar um comando dentro de um container que já está em execução, isso é **muito útil**, pois nos ajuda a encontrar problemas durante a execução dos nossos projetos.

> Nós vamos utilizá-lo para executar o programa `sh`, que nos permite simular um acesso de terminal dentro do container que já está em execução! Legal, né?

-   Vamos utilizar o comando `docker exec -it <nome-do-container> <comando-a-ser-executado>`, testando o acesso ao terminal com o mesmo exemplo de container criado anteriormente:

Copiar

```bash
pessoa@trybe:~/course$ docker container run --rm -d --name meu-container alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
9ee42188fa7   alpine:3.14   "sleep 300"   14 seconds ago   Up 13 seconds             meu-container
pessoa@trybe:~/course$ docker exec -it meu-container sh
/ # ps aux
PID   USER     TIME  COMMAND
    1 root      0:00 sleep 300
   14 root      0:00 sh
   20 root      0:00 ps aux
/ # exit
pessoa@trybe:~/course$ docker stop -t 0 meu-container
meu-container
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
```

### Recapitulando 🧠

Vamos entender passo a passo o que aconteceu nos comandos anteriores:

-   1 - Criamos um novo container a partir da imagem `alpine`, com a tag `3.14`:
    
    -   No modo **detached** (-d);
    -   Atribuindo o nome de **meu-container** (`--name`);
    -   Solicitando sua **remoção** após finalização (`--rm`);
    -   Substituindo o comando padrão para um **comando customizado** (`sleep 300`).
-   2 - Verificamos a lista de containers usando `docker ps`, apenas para validar o sucesso do comando anterior:
    
-   Executamos o comando `docker exec -it meu-container sh`;
    
    -   Passando a flag `-t` e solicitando a criação de uma sessão de terminal;
    -   Passando a flag `-i`, necessária para que a sessão seja **interativa**;
    -   O comando a ser executado será `sh`, que é um programa de terminal linux.
-   3 - Já dentro do container, executamos um comando `ps aux`:
    
    -   Este comando lista todos os processos em execução no momento;
    -   Veja que legal: Dentro do container, os **únicos processos** em execução são:
        -   `sleep 300`, que especificamos na inicialização do container;
        -   `sh`, que especificamos na hora de abrir a sessão interativa;
        -   `ps aux`, que acabamos de executar para obter esta lista;
    -   **É só isso!** Dentro do container, não existe mais nenhum outro processo em execução! Aqui temos a confirmação do isolamento dos containers do resto dos processos da nossa máquina!
-   4 - Usamos o comando `exit` para sair do terminal do container;
    
-   5 - Forçamos a parada de execução do container usando o comando `docker stop`;
    
-   6 - Validamos que não há nenhum container restante na máquina usando `docker ps -a`.
    

Ainda não ficou nítido? Confira na figura abaixo ilustrando a relação entre o comando e a execução do comando no container.

![docker-exec](https://content-assets.betrybe.com/prod/docker-exec.png)

Passos do Docker durante a execução de um comando.

## Ver os logs de um container em execução

Quando executamos um novo container no modo **detached**, isto é, em segundo plano, nós deixamos de ver as informações (logs, erros, etc) que o programa está executando. Entretanto, o Docker oferece um comando para que a gente possa ver essas informações sem precisar se conectar diretamente ao terminal do container.

-   O comando é o seguinte: `docker logs <flags> <nome-do-container>`. Vamos ver um exemplo de saída deste comando:

Copiar

```bash
pessoa@trybe:~/course$ docker container run -d --name meu-container alpine:3.14 date
b89b81f17d0cb19edfcfae94d13f3b6dc0953d7cd9b1aaf0dbf4680d1d9b75ee
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND   CREATED         STATUS                    PORTS     NAMES
b89b81f17d0c   alpine:3.14   "date"    2 seconds ago   Exited (0) 1 second ago             meu-container
pessoa@trybe:~$ docker logs meu-container
Tue Apr 26 13:29:32 UTC 2022
pessoa@trybe:~$ docker rm meu-container
meu-container
pessoa@trybe:~$
```

Ainda não ficou nítido? Confira na figura abaixo ilustrando a relação entre o comando e a obtenção dos logs do container.

![docker-logs](https://content-assets.betrybe.com/prod/docker-logs.png)

Passos do Docker durante a obtenção dos logs.

### Recapitulando 🧠

Vamos entender passo a passo o que aconteceu nos comandos anteriores:

-   1 - Criamos um novo container a partir da imagem `alpine`, com a tag `3.14`:
    
    -   No modo **detached** (-d);
    -   Atribuindo o nome de **meu-container** (`--name`);
    -   Substituindo o comando padrão para um **comando customizado** (`date`).
-   2 - Verificamos a lista de containers usando `docker ps`, apenas para validar o sucesso do comando anterior:
    
    -   A saída do comando mostra que o container já parou sua execução;
    -   Porém, ainda podemos ver os logs de um container parado sem problemas.
-   3 - Executamos o comando `docker logs meu-container`:
    
    -   Não especificamos **nenhuma** flag.
-   4 - É exibido na tela a mensagem `Tue Apr 26 13:29:32 UTC 2022`, que é a saída do comando `date`, feito **dentro** do container.
    
-   5 - Após isso, removemos o container usando o comando `docker rm`.
    

## Monitorando os processos dentro de um container

O comando `docker top`, assim como nos terminais Linux, traz as informações sobre os processos que estão sendo rodados **dentro do container**, o que não inclui, por exemplo, serviços que são compartilhados com o sistema hospedeiro.

O comando a seguir é útil para quando estamos os rodando em segundo plano:

```bash
gabriel@trybe:~$ docker container run -d --rm --name meu-container alpine:3.14 sleep 300
6942640dda0e7d5e3db3fb122ab2e6c77f0d4bcf75b8c1082143cedf8215a193
gabriel@trybe:~$ docker top meu-container
UID      PID     PPID     C     STIME     TTY   TIME       CMD
root     5299    5278     0     09:35     ?     00:00:00   sleep 300
gabriel@trybe:~$ docker stop -t 0 meu-container
meu-container
```

### Recapitulando 🧠

**Vamos entender passo a passo o que aconteceu nos comandos anteriores:

-   1 - Criamos um novo container a partir da imagem `alpine`, com a tag `3.14`:
    
    -   No modo **detached** (-d);
    -   Solicitando sua **remoção** após finalização (`--rm`).
    -   Atribuindo o nome de **meu-container** (`--name`);
    -   Substituindo o comando padrão para um **comando customizado** (`sleep 300`);
-   2 - Verificamos a lista de processos do container usando `docker top`:
    
    -   A saída do comando mostra que existe apenas um processo em execução, que é o processo que especificamos.
-   3 - Forçamos a parada do container usando o comando `docker stop`.
    

## Limpando containers que não estão sendo utilizados

**O comando `docker container prune` remove todos os containers inativos do seu computador.** Além disso, ele pede uma confirmação para executar a operação e no final mostra a quantidade de espaço em disco recuperado. Veja um exemplo de saída do comando abaixo:

```bash
pessoa@trybe:~/course$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
ed2aa643a36af0d3805812a6114e6da1a339f8059e373246270f0446c20f2f7f
[várias linhas]
108085a4660a7e69d1625503f0b078ecc94155edf4b2023796eadad35f1e65f6

Total reclaimed space: 442B
pessoa@trybe:~/course$
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/a852c0dd-0602-4357-88e8-707352e97927/lesson/018a382c-80ae-43fb-9fe1-1ed24732c298)