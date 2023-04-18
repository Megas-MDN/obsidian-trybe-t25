[[Docker]]

## Acessando o terminal do container

O Docker nos permite executar um comando dentro de um container que já está em execução, isso é **muito útil**, pois nos ajuda a encontrar problemas durante a execução dos nossos projetos.

> Nós vamos utilizá-lo para executar o programa `sh`, que nos permite simular um acesso de terminal dentro do container que já está em execução! Legal, né?

-   Vamos utilizar o comando `docker exec -it <nome-do-container> <comando-a-ser-executado>`, testando o acesso ao terminal com o mesmo exemplo de container criado anteriormente:

```bash
pessoa@trybe:~/course$ docker container run --rm -d --name meu-container alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
99ee42188fa7   alpine:3.14   "sleep 300"   14 seconds ago   Up 13 seconds             meu-container
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
