[[Docker]]
[[Docker - 7 Utilizando Containers]]


Agora que já entendemos o que é uma imagem Docker, chegou o tão esperado momento de criar nossa primeira imagem Docker! 🥳

Para usar nossas aplicações dentro de containers, primeiro precisamos criar uma imagem Docker para a aplicação! Podemos fazer isso a partir dos arquivos `Dockerfile`.

O `Dockerfile` é um arquivo de configuração com uma linguagem própria, que é usado pelo Docker como um passo a passo do que você deseja que aconteça.

> Imagine este arquivo como se fosse a _receita_ que o Docker deve seguir para criar uma nova imagem exatamente do jeito que a gente quer!

![Nossas receitas tornarão sua vida de pessoa programadora muito mais apetitosas](https://content-assets.betrybe.com/prod/Nossas%20receitas%20tornar%C3%A3o%20sua%20vida%20de%20pessoa%20programadora%20muito%20mais%20apetitosas.gif)
` Nossas receitas tornarão sua vida de pessoa programadora muito mais apetitosas

A seguir, aprenderemos como utilizar essa linguagem especial do Dockerfile, que como outras linguagens de programação possui **palavras reservadas**, permitindo assim o controle dos recursos necessários para que nossas aplicações funcionem corretamente dentro de containers.

## Limpando tudo antes de começar!

Use o comando abaixo para remover todos os containers e imagens Docker que estejam em seu computador, para que assim você possa acompanhar os exemplos:

Copiar

```bash
docker system prune -af
```

## Um passo de cada vez!

**Vamos para a prática** 💪

Agora vamos criar uma imagem Docker que, quando executada como um container, vai imprimir na tela a seguinte mensagem: `Eu sou uma pessoa estudante da Trybe!`, e terminar sua execução. Para isso, vamos criar um arquivo `Dockerfile` na pasta que estamos programando com o conteúdo abaixo para a construção dessa imagem.

> Atenção: O arquivo _Dockerfile_ deve ser criado na raiz do seu projeto e não tem nenhuma extensão. Ele ficará assim no seu VS Code:

Copiar

```bash
.
└── meu-projeto/
    ├── src/
    │   └── 
    └── Dockerfile
```

Criando o arquivo `Dockerfile` podemos adicionar o conteúdo a seguir:

```dockerfile
FROM alpine:3.14
CMD ["echo", "Eu sou uma pessoa estudante da Trybe!"]
```

Você deve estar se perguntando: _somente essas duas linhas já são suficientes para criarmos nossa primeira imagem Docker?_ 🤔

A resposta é **sim**! Vamos entender o significado de cada linha acima:

-   `FROM alpine:3.14`
    
    -   Essa linha não parece ser tão estranha pra gente, pois já utilizamos a imagem `alpine:3.14` anteriormente;
    -   Logo, a sua explicação é bem nítida: a palavra reservada `FROM` significa que vamos começar a construção desta imagem a partir da imagem Docker **já existente**!
-   `CMD ["echo", "Eu sou uma pessoa estudante da Trybe!"]`
    
    -   A palavra reservada `CMD` mostra qual comando deve ser utilizado ao iniciar a imagem como um container;
    -   Neste caso, o `CMD` aceita uma lista de parâmetros (como o exemplo acima) ou apenas os comandos, sem declarar como lista, por exemplo:
        -   `CMD echo "olá mundo"`

🥳 Eba! Acabamos de criar nosso primeiro arquivo Dockerfile! _Mas e agora, como vamos construir de fato nossa primeira imagem Docker?_

▶️ Para isso, vamos utilizar o comando `docker build <flags> -t <nome-da-imagem> <contexto>`! O comando espera:

-   Uma flag `-t`, que indicará qual será o nome da imagem, e também a tag, se utilizar o formato `<nome>:<tag>`;
-   Um contexto, ou seja, em qual caminho de pasta o Docker deve se basear para processar o arquivo Dockerfile.
    -   Normalmente utilizamos apenas `.` (ponto final), que indica a pasta atual.

Baseando-se então no Dockerfile acima, vamos executar o comando `docker build -t primeira-imagem .`. Vamos ver a saída dos comandos a seguir:


```bash
pessoa@trybe:~$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
pessoa@trybe:~$ docker build -t primeira-imagem .
Sending build context to Docker daemon  3.584kB
Step 1/2 : FROM alpine:3.14
3.14: Pulling from library/alpine
8663204ce13b: Pull complete
Digest: sha256:06b5d462c92fc39303e6363c65e074559f8d6b1363250027ed5053557e3398c5
Status: Downloaded newer image for alpine:3.14
 ---> e04c818066af
Step 2/2 : CMD ["echo", "Eu sou pessoa estudante da Trybe!"]
 ---> Running in e199bcd809d5
Removing intermediate container e199bcd809d5
 ---> 222b0b148f0b
Successfully built 222b0b148f0b
Successfully tagged primeira-imagem:latest
pessoa@trybe:~$ docker images
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
primeira-imagem   latest    222b0b148f0b   3 seconds ago   5.59MB
alpine            3.14      e04c818066af   3 weeks ago     5.59MB
```

Vamos acompanhar passo a passo do que aconteceu acima:

-   Nós executamos o comando `docker images` para mostrar que não temos nenhuma imagem Docker atualmente em nosso computador;
    
    -   Se você tiver algumas imagens nessa lista, é importante removê-las para seguir com os exemplos 😄
-   Na mesma pasta que contém o arquivo Dockerfile acima, executamos o comando `docker build -t primeira-imagem .`
    
    -   Passamos a flag `-t primeira-imagem` para indicar ao Docker como a imagem deve se chamar;
    -   Como contexto, passamos o valor `.` (ponto final) para indicar ao Docker que o processo de construção deve se basear na pasta atual;
    -   _Nós vamos entender a necessidade de saber o contexto mais adiante._
-   Como o Docker não possui a imagem `alpine:3.14` localmente, ele executou o mesmo processo do `docker pull` de maneira _interna_, obtendo a imagem do Docker Hub. Esta ação foi descrita pelo Docker como **Step 1/2**;
    
-   O Docker configura que ao executar essa imagem como container, o comando a ser executado é o `echo Eu sou pessoa estudante da Trybe!"`. Esta ação foi descrita pelo Docker como **Step 2/2**;
    
-   O Docker imprime na tela a mensagem: `Successfully tagged primeira-imagem:latest`
    
    -   A imagem recebe a tag `latest` por padrão caso a gente não declare uma tag específica na flag `-t`.
-   Pronto! O Docker já construiu a nossa primeira imagem!
    
-   Vamos confirmar isso executando o comando `docker images`;
    
-   E podemos ver que agora temos **duas imagens** em nosso computador:
    
    -   A imagem `alpine:3.14` é a que o Docker obteve do Docker Hub, precisamos dela como base na nossa imagem;
    -   A imagem `primeira-imagem:latest`, que é a imagem Docker que acabamos de criar!

![O Docker obteve a imagem base do Docker Hub e construiu a nossa imagem](https://content-assets.betrybe.com/prod/O%20Docker%20obteve%20a%20imagem%20base%20do%20Docker%20Hub%20e%20construiu%20a%20nossa%20imagem.png)

O Docker obteve a imagem base do Docker Hub e construiu a nossa imagem.

**Para fixar** 🧠

_Que tal executar nossa nova imagem `primeira-imagem` como um container e ver se deu tudo certo?_ Bora se testar! 🐋

## Executando um novo container com nossa imagem

Vamos executar o comando `docker run --rm primeira-imagem` e verificar se realmente a mensagem que colocamos é impressa na tela. Veja a saída abaixo:

Copiar

```bash
pessoa@trybe:~$ docker images
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
primeira-imagem   latest    222b0b148f0b   15 minutes ago   5.59MB
alpine            3.14      e04c818066af   3 weeks ago      5.59MB
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~$ docker run --rm primeira-imagem
Eu sou pessoa estudante da Trybe!
pessoa@trybe:~$
```

**Olha que legal!** Vimos que nossa imagem está presente em nosso computador utilizando o comando `docker images`. Depois validamos que não tínhamos nenhum container em execução ou parado utilizando o comando `docker ps -a` e finalmente utilizamos o comando `docker run` para executar nossa imagem como um container!

Vamos conhecer mais palavras reservadas do Dockerfile e criar imagens Docker mais complexas? Agora o céu é o limite pra gente com o Docker! 🐋

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/da25fd46-8818-4234-8603-a442b047370f/lesson/822be635-e9da-4b46-8042-cbf537013935)