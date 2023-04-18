[[Docker]]
[[Docker - 7 Utilizando Containers]]


Imagens Docker são arquivos que funcionam como fotos de programas, bibliotecas, frameworks ou mesmo sistemas operacionais a partir dos quais criamos containers e podemos executar nossos códigos.

## Como o Docker decide se precisa obter imagens de um Registry?

Para responder essa pergunta, vamos voltar ao exemplo de quando rodamos uma imagem do _Docker Hub_ pela primeira vez. Nesse caso, a imagem do _Docker Hub_ é baixada _automagicamente_ para o nosso computador, de modo que você possa confirmar a existência daquela imagem utilizando o comando `docker images`. Veja um exemplo de saída do comando abaixo:

```bash
pessoa@trybe:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
pessoa@trybe:~$
```

🤔 _Mas você sabia que podemos adiantar o processo e já baixar uma imagem do Docker Hub sem necessariamente executar esta imagem como um container?_

Sim, isso é possível! Do mesmo jeito que usamos o comando `git pull` para obter o código-fonte atualizado do _GitHub_, existe o comando `docker pull <nome-da-imagem>`, onde podemos obter a imagem Docker diretamente do Registry e já deixá-la em nosso computador. Veja um exemplo de saída deste comando abaixo:

```bash
pessoa@trybe:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
pessoa@trybe:~$ docker pull alpine:3.14
3.14: Pulling from library/alpine
8663204ce13b: Pull complete
Digest: sha256:06b5d462c92fc39303e6363c65e074559f8d6b1363250027ed5053557e3398c5
Status: Downloaded newer image for alpine:3.14
docker.io/library/alpine:3.14
pessoa@trybe:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
alpine        3.14      e04c818066af   3 weeks ago    5.59MB
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
pessoa@trybe:~$
```

Vamos acompanhar passo a passo o que aconteceu acima:

-   Executamos o comando `docker images` e vimos que tínhamos apenas a imagem `hello-world`, com a tag `latest`.
-   Executamos o comando `docker pull alpine:3.14`, obtendo a imagem `alpine`, com a tag específica `3.14`.
-   Executamos o comando `docker images` novamente e validamos que agora a imagem `alpine:3.14` aparece como uma das imagens Docker disponíveis localmente!

Viu que bacana? Podemos adiantar o processo de obter uma imagem Docker caso seja necessário!

▶️ Agora, vamos entender qual é a lógica que o Docker usa para obter ou não imagens do seu Registry público.

Para revisar o que acabamos de aprender de uma maneira bem simples e entender melhor o processo, vamos dar uma olhada na ilustração abaixo:

![Processo de instalacao de uma imagem](https://content-assets.betrybe.com/prod/Processo%20de%20instalacao%20de%20uma%20imagem.png)

Mesmo baseado na mesma Imagem Docker, os containers executam em contextos diferentes.

Agora, vamos entender o que acontece nesta figura com a explicação abaixo:

1️⃣ Executamos o comando `docker run hello-world`

-   Neste momento, o Docker verifica se a imagem existe localmente;
-   Se a imagem existe, o docker começa o processo de subir o container baseado nesta imagem.

2️⃣ Como a imagem `hello-world` não é encontrada localmente por padrão, o Docker faz o mesmo processo que o comando `docker pull` faria, só que de maneira automática.

-   Ao terminar de fazer o download da imagem, o Docker finalmente pode iniciar o processo de subir um novo container baseado na imagem recém baixada!

Para sabermos se o container foi criado a partir da imagem `hello-world`, basta verificarmos a lista de containers atuais que usam o comando que aprendemos no conteúdo anterior:

```bash
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND      CREATED             STATUS                         PORTS         NAMES
8b3b610c87a9   hello-world   "/hello"     24 minutes ago      Exited (0) 1 second ago                      blissful_sinoussi
pessoa@trybe:~$
```

## Uma imagem, vários containers!

📝 **Anote aí**: podemos ter vários contêineres a partir de uma imagem Docker!

Para testar isso na prática, vamos executar novamente o comando `docker run hello-world` e visualizar o que acontece:

Copiar

```bash
pessoa@trybe:~$ docker run hello-world
Hello from Docker!
[...]
For more examples and ideas, visit:
 https://docs.docker.com/get-started/

pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
5751a5cd20a6   hello-world   "/hello"   2 seconds ago    Exited (0) 1 second ago               gracious_ishizaka
6c799b099fb0   hello-world   "/hello"   30 seconds ago   Exited (0) 29 seconds ago             blissful_sinoussi
pessoa@trybe:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
alpine        3.14      e04c818066af   3 weeks ago    5.59MB
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
pessoa@trybe:~$
```

Vamos entender o passo a passo do que aconteceu acima:

-   Nós já tínhamos executado o comando `docker run hello-world` no exemplo anterior;
-   Agora executamos o **mesmo comando** novamente;
-   A mensagem de boas-vindas do Docker aparece;
-   Verificamos a lista de containers em execução ou parados com o comando `docker ps -a`;
-   Vimos que temos **dois** containers diferentes baseados em uma mesma imagem;
-   Executamos o comando `docker images` e verificamos que ainda temos uma imagem `hello-world:latest`!

**Qual aprendizado obtemos neste exemplo?**

> Podemos ter vários containers reproduzindo uma mesma imagem Docker 🤩!

![docker-image-process](https://content-assets.betrybe.com/prod/docker-image-process.png)

Mesmo baseado na mesma Imagem Docker, os containers executam em contextos diferentes.

Toda imagem possui um identificador, chamado de `IMAGE ID`. Além disso, todo container também possui um identificador, chamado de `CONTAINER ID`. Ambos são elementos únicos dentro do Docker e servem como referência para outras possibilidades de comando.

Anteriormente, vimos que o comando `docker rm -f <nome-do-container>` apaga um container pelo seu nome, até mesmo se ele estiver ativo (utilizando a flag `-f`). Pela mesma lógica, podemos utilizar o comando passando o `CONTAINER ID`. Logo, o comando passaria a ser `docker rm -f <id-do-container>`.

Vamos então remover os containers que utilizamos no exemplo anterior.

> ⚠️ **Importante**: os nomes e os identificadores dos containers na sua máquina serão **diferentes** dos utilizados neste exemplo, ok?

Vamos executar o comando `docker ps -a` para obter os nomes e identificadores dos containers primeiro:

```bash
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
5751a5cd20a6   hello-world   "/hello"   2 seconds ago    Exited (0) 1 second ago               gracious_ishizaka
6c799b099fb0   hello-world   "/hello"   30 seconds ago   Exited (0) 29 seconds ago             blissful_sinoussi
pessoa@trybe:~$ docker rm -f 5751a5cd20a6
5751a5cd20a6
pessoa@trybe:~$ docker rm -f 6c799b099fb0
6c799b099fb0
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~$
```

Vamos acompanhar passo a passo o que aconteceu acima:

-   Nós executamos o comando `docker ps -a` para conhecer os identificadores dos containers;
-   Obtemos o ID do container chamado **gracious_ishizaka**, sendo `5751a5cd20a6`, e executamos o comando `docker rm -f`;
-   Obtemos o ID do container chamado **blissful_sinoussi**, sendo `6c799b099fb0`, e executamos o comando `docker rm -f`;
-   Nós executamos novamente o comando `docker ps -a` e validamos que não temos mais nenhum container em nosso computador!

Agora podemos fazer o mesmo processo para gerenciar as imagens Docker em nosso computador! Vamos aprender a remover as imagens para liberarmos espaço de armazenamento. Para remover uma imagem Docker do nosso computador, utilizamos o comando `docker rmi`, onde **rmi** é um acrônimo das palavras _ReMover Imagem_ 🤓. Vamos seguir os comandos abaixo para aprender a remover uma imagem Docker:

> ⚠️ **Importante:** é possível que os identificadores das imagens usados neste exemplo sejam diferentes dos identificadores que aparecem agora no seu computador, ok? Vamos executar o comando `docker images` para obtê-los primeiro:

```bash
pessoa@trybe:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
alpine        3.14      e04c818066af   3 weeks ago    5.59MB
hello-world   latest    feb5d9fea6a5   7 months ago   13.3kB
pessoa@trybe:~$ docker rmi e04c818066af
Untagged: alpine:3.14
Untagged: alpine@sha256:06b5d462c92fc39303e6363c65e074559f8d6b1363250027ed5053557e3398c5
Deleted: sha256:e04c818066afe78a0c9379f62ec65aece28566024fd348242de92760293454b8
Deleted: sha256:b541d28bf3b491aeb424c61353c8c92476ecc2cd603a6c09ee5c2708f1a4b258
pessoa@trybe:~$ docker rmi feb5d9fea6a5
Untagged: hello-world:latest
Untagged: hello-world@sha256:10d7d58d5ebd2a652f4d93fdd86da8f265f5318c6a73cc5b6a9798ff6d2b2e67
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
pessoa@trybe:~$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
pessoa@trybe:~$
```

Vamos acompanhar passo a passo o que aconteceu acima:

-   Nós executamos o comando `docker images` para conhecer os identificadores das imagens;
-   Obtemos o ID da imagem **alpine:3.14**, sendo `e04c818066af`, e executamos o comando `docker rmi`;
-   Obtemos o ID da imagem **hello-world:latest**, sendo `feb5d9fea6a5`, e executamos o comando `docker rmi`;
-   Nós executamos novamente o comando `docker images` e validamos que não temos mais nenhuma imagem em nosso computador!

**Pronto!** Acabamos de aprender como gerenciar melhor as imagens Docker em nosso computador! Que tal começarmos a **criar nossas próprias imagens Docker** agora? Bora lá! 🐋