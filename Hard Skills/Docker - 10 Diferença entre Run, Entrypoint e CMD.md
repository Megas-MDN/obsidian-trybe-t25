[[Docker]]

Essas três palavras reservadas do Dockerfile são as maiores fontes de confusão para as pessoas iniciantes de Docker: **RUN, ENTRYPOINT e CMD**. Elas parecem fazer a mesma coisa, entretanto cada uma dessas palavras reservadas são importantes e necessárias, dependendo do contexto.

![Qual a diferença entre elas?](https://media.giphy.com/media/FcuiZUneg1YRAu1lH2/giphy.gif)

Qual a diferença entre elas?

Logo, para deixarmos nítido o uso de cada uma delas, vamos ver a explicação junto com alguns exemplos:

-   `RUN <comando> <argumento1> <argumento2> <argumentoN>`:
    
    -   Indica que o comando dado deve ser executado durante a construção da imagem Docker!
    -   Ou seja, é muito comum utilizar o `RUN` para fazer instalações de dependências.
-   `ENTRYPOINT <comando> <argumento1> <argumento2> <argumentoN>`:
    
    -   Indica qual é o comando (e seus argumentos) que **deve** ser executado ao iniciar esta imagem Docker como um container;
    -   Considere o `ENTRYPOINT` como **obrigação** de comando a ser executado;
    -   Ele sempre será utilizado como _ponto de entrada_ da imagem.
-   `CMD <comando> <argumento1> <argumento2> <argumentoN>`:
    
    -   Indica qual é o comando (e seus argumentos) que **pode** ser executado ao iniciar esta imagem Docker como um container;
    -   Conside o `CMD` como **sugestão** de comando a ser executado;
    -   Ele pode ser substituído ao executar o comando `docker run imagem <comando> <argumento1>`.

▶️ Considere o seguinte Dockerfile abaixo e que já construímos essa imagem com nome de `exemplo-cmd`:

```dockerfile
FROM alpine:3.14
CMD ["echo", "Olá mundo!"]
```


▶️ Ao executar essa imagem como um container com o comando `docker run --rm exemplo-cmd`, sem passar nenhum parâmetro extra, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-cmd
Olá mundo!
pessoa@trybe:~$
```

▶️ Agora, ao executar essa imagem como um container com o comando `docker run --rm exemplo-cmd echo "Sou diferente!"`, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-cmd echo "Sou diferente!"
Sou diferente!
pessoa@trybe:~$
```

> Perceba que o conteúdo de `CMD` foi totalmente substituído.

▶️ Agora vamos mudar este Dockerfile de `CMD` para `ENTRYPOINT`, de modo a construir essa imagem com o nome de `exemplo-entrypoint`:

```dockerfile
FROM alpine:3.14
ENTRYPOINT ["echo", "Olá mundo!"]
```

▶️ Ao executar essa imagem como um container com o comando `docker run --rm exemplo-entrypoint`, sem passar nenhum parâmetro extra, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-entrypoint
Olá mundo!
pessoa@trybe:~$
```

▶️ Agora, ao executar essa imagem como um container com o comando `docker run --rm exemplo-entrypoint "Sou diferente!"`, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-entrypoint "Sou diferente!"
Olá mundo! Sou diferente!
pessoa@trybe:~$
```

> Perceba que o conteúdo de `ENTRYPOINT` **não** é substituído e que o parâmetro `"Sou diferente"` é colocado depois do comando do `ENTRYPOINT`. Isso significa que o container executou o comando `echo "Olá mundo!" "Sou diferente"`.

▶️ Agora vamos mudar este Dockerfile para usar `CMD` e `ENTRYPOINT` ao mesmo tempo, de modo a construir essa imagem com o nome de `exemplo-entrypoint-cmd`:

```dockerfile
FROM alpine:3.14
ENTRYPOINT ["echo"]
CMD ["Sou a mensagem padrão."]
```

▶️ Ao executar essa imagem como um container com o comando `docker run --rm exemplo-entrypoint-cmd`, sem passar nenhum parâmetro extra, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-entrypoint-cmd
Sou a mensagem padrão.
pessoa@trybe:~$
```

▶️ Agora, ao executar essa imagem como um container com o comando `docker run --rm exemplo-entrypoint-cmd "Sou uma mensagem nova!"`, temos:

```bash
pessoa@trybe:~$ docker run --rm exemplo-entrypoint-cmd "Sou uma mensagem nova!"
Sou uma mensagem nova!
pessoa@trybe:~$
```

**E ai, o que achou?**

▶️ Podemos usar `ENTRYPOINT` para dizer **exatamente** o que deve ser executado ao iniciar a imagem como um container. Também podemos usar o `CMD` como uma sugestão de parâmetros padrão.

Imagine que o Docker ao iniciar um container vai executar o comando da seguinte maneira:

```bash
<conteúdo-do-entrypoint> <conteúdo-do-cmd>
```

É por estes motivos que `ENTRYPOINT` e `CMD` _parecem_ ter a mesma funcionalidade, mas na prática eles são **complementares**!

![Agora você é mestre do Dockerfile!](https://content-assets.betrybe.com/prod/teste.gif)

Agora você é mestre do Dockerfile!



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/da25fd46-8818-4234-8603-a442b047370f/lesson/93c74629-1ea8-4fbd-9c2a-5db417249348)