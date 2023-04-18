[[Docker]]


Já podemos concluir que o arquivo `Dockerfile` é poderoso e simples ao mesmo tempo, mas não vamos parar por aqui!

Chegou a hora de conhecermos outras **palavras reservadas** extremamente úteis na hora de construir imagens Docker mais **complexas** e mais **robustas**!

## Limpando tudo antes de começar!

Use o comando abaixo para remover todos os containers e imagens Docker que estejam em seu computador para que você possa acompanhar os exemplos:

```bash
docker system prune -af
```

## Criando os arquivos para o novo servidor web com Hugo e NGINX

Para este novo exemplo, vamos criar um servidor web novamente, porém haverá uma etapa de **pré-processamento**. Para esta etapa, vamos utilizar uma ferramenta chamada [Hugo](https://gohugo.io/), que nos permite criar páginas web a partir de templates.

_Não se preocupe, você não vai precisar instalar nada extra em seu computador, pois tudo será feito durante o comando docker build_ 😲.

![Vamos modernizar nossas imagens Docker agora!](https://content-assets.betrybe.com/prod/Vamos%20modernizar%20nossas%20imagens%20Docker%20agora!.gif)
`Vamos modernizar nossas imagens Docker agora!`

O objetivo da ferramenta **Hugo** é facilitar a criação de páginas, de modo que as pessoas possam focar mais em escrever o **conteúdo** do que se preocupar com **tags HTML** das páginas.

Vamos começar criando três arquivos, sendo eles:

-   **config.toml**: será um arquivo de configuração para o **Hugo**;
-   **index.html**: será o template HTML que o **Hugo** utilizará para gerar páginas;
-   **_index.md**: será o arquivo com o conteúdo de fato.

▶️ Para o arquivo `config.toml`, use o seguinte código-fonte:


```bash
name = "Meu site em Hugo"
```

▶️ Para o arquivo `index.html`, use o seguinte código-fonte:


```html
<!DOCTYPE html>
   <html>
      <head>
      <title>{{ .Title }}</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   </head>
   <body>
      <h1>{{ .Title }}</h1>
      {{ .Content }}
   </body>
</html>
```

▶️ Para o arquivo `_index.md`, use o seguinte código-fonte:


```markdown
...
title: Meu site em Hugo
...

Meu conteúdo super interessante!
```

▶️ Por fim, para o nosso arquivo `Dockerfile`, use o seguinte código-fonte:

```dockerfile
FROM nginx:1.21-alpine AS primeiro-estagio
WORKDIR /site

COPY config.toml config.toml
COPY index.html /site/layouts/index.html
COPY _index.md /site/content/_index.md

RUN apk add hugo
RUN hugo --minify --gc
RUN mv /site/public/* /usr/share/nginx/html

ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

![Tem algo diferente nesse Dockerfile!](https://content-assets.betrybe.com/prod/Tem%20algo%20diferente%20nesse%20Dockerfile!.gif)

Tem algo diferente nesse Dockerfile!

_*Você já deve ter percebido algumas palavras reservadas novas neste Dockerfile, não é mesmo?_ 🧐

Vamos falar sobre cada uma delas:

![[Pasted image 20230111221134.png]]

⚠️**Importante**: você pode ter percebido que a função do `ENTRYPOINT` parece ser a mesma que o `CMD` que estávamos usando anteriormente 🤔. Essa dúvida é comum e em breve vamos explicar a diferença de uso entre a função do `ENTRYPOINT` e o `CMD`.

## Construindo a nossa nova imagem

Com os arquivos criados acima, vamos executar o comando `docker build -t site-hugo`. Veja a saída dos comandos a seguir:


```bash
pessoa@trybe:~$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
pessoa@trybe:~$ docker build -t site-hugo .
Sending build context to Docker daemon   5.12kB
[...]
Successfully tagged site-hugo:latest
pessoa@trybe:~$ docker images
REPOSITORY   TAG           IMAGE ID       CREATED          SIZE
site-hugo    latest        51dc918e901d   12 seconds ago   78.8MB
nginx        1.21-alpine   51696c87e77e   3 weeks ago      23.4MB
```

Primeiro, validamos que não havia nenhuma imagem Docker em nosso computador. Depois disso, executamos o comando de construção da imagem e vimos como resultado **duas** imagens:

-   A imagem **nginx**, que usamos como imagem base;
-   A nossa imagem **site-hugo**.

> Perceba a diferença entre os _tamanhos_ das imagens, dado que na imagem **site-hugo** nós precisamos instalar a ferramenta Hugo, fazendo a imagem ocupar mais espaço de armazenamento.

## Executando um novo container com nossa imagem

Agora, vamos executar um novo container utilizando nossa imagem recém criada. Lembre-se que vamos utilizar a flag `-p` para mapear uma porta entre nosso computador e a porta do container. Para isso, utilize o seguinte comando:

Copiar

```bash
docker run -p 1234:80 -d --name meu-container site-hugo
```

Agora, abra seu navegador web e acesse o endereço `http://localhost:1234`, verifique se consegue visualizar a página HTML:

![meu-site-hugo](https://content-assets.betrybe.com/prod/meu-site-hugo.png)

Opa, **funcionou!** Não se esqueça de remover o container com o comando abaixo:


```bash
docker rm -f meu-container
```

## Construção em múltiplos estágios

Agora chegou a hora do seu Dockerfile brilhar! 🌟

Vamos aprender um dos conceitos mais importantes na hora de construirmos nossas imagens Docker: **Construção em múltiplos estágios**. Mas, o que é isso? 🤔

![Construção em múltiplos estágios?](https://media.giphy.com/media/puOukoEvH4uAw/giphy.gif)

Construção em múltiplos estágios?

Considere o Dockerfile abaixo, que é o mesmo utilizado no exemplo anterior.

-   Na linha 8, nós instalamos a ferramenta **Hugo**, que foi útil apenas durante a execução do comando `RUN hugo --minify --gc`, na linha 9.
-   Após isso, a gente não precisou mais dessa ferramenta, porém ela ainda ficou instalada em nossa imagem Docker, **ocupando espaço**.

```dockerfile
FROM nginx:1.21-alpine AS primeiro-estagio
WORKDIR /site

COPY config.toml config.toml
COPY index.html /site/layouts/index.html
COPY _index.md /site/content/_index.md

RUN apk add hugo
RUN hugo --minify --gc
RUN mv /site/public/* /usr/share/nginx/html

ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

▶️ Nosso objetivo agora é continuar utilizando o `docker build` para fazer tudo o que for necessário para construir uma imagem Docker funcional, ou seja, não queremos instalar **nada extra** em nosso computador. Precisamos encontrar uma maneira de:

1.  Instalar a ferramenta **Hugo**;
2.  Executar o comando `hugo --minify --gc`;
3.  Obter as páginas HTML resultantes;
4.  Criar uma **nova imagem limpa** baseada no **nginx**;
5.  Copiar apenas as páginas HTML geradas pelo **Hugo** para esta nova imagem;
    
    > Após tudo isso, vamos ter uma imagem Docker apenas com o **nginx** e as páginas geradas pelo **Hugo**.
    

**Será que isso é possível?** A resposta é **sim!** 🤩

> 🥇 Podemos criar imagens **intermediárias** com apenas um arquivo Dockerfile! Imagine agora o poder que nós temos em mãos!

Veja a seguir o mesmo exemplo de Dockerfile que utilizamos anteriormente, porém adaptado para fazer a construção em múltiplos estágios, e assim, usar imagens intermediárias:

```dockerfile
# Primeiro Estágio
FROM alpine:3.14 AS primeiro-estagio
WORKDIR /site

COPY config.toml config.toml
COPY index.html /site/layouts/index.html
COPY _index.md /site/content/_index.md

RUN apk add hugo
RUN hugo --minify --gc

# Segundo Estágio
FROM nginx:1.21-alpine AS segundo-estagio
COPY --from=primeiro-estagio /site/public/ /usr/share/nginx/html
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

![Tem algo diferente nesse Dockerfile!](https://content-assets.betrybe.com/prod/Tem%20algo%20diferente%20nesse%20Dockerfile!.gif)

Tem algo diferente nesse Dockerfile!

Você já deve ter percebido que este Dockerfile é **muito parecido** com o anterior, mas existem dois detalhes importantes:

![[Pasted image 20230111221426.png]]

_Vamos construir essa nova imagem Docker e compará-la com a imagem anterior?_ 🧐

Veja a saída dos comandos abaixo:

```bash
pessoa@trybe:~$ docker build -t multi-stage-site-hugo .
Sending build context to Docker daemon  6.144kB
[......]
Successfully tagged multi-stage-site-hugo:latest
pessoa@trybe:~$ docker images
REPOSITORY              TAG           IMAGE ID       CREATED          SIZE
<none>                  <none>        49f9fac0ad9a   3 seconds ago    65.7MB
multi-stage-site-hugo   latest        c5f6e09557ff   3 seconds ago    23.4MB
site-hugo               latest        51dc918e901d   41 minutes ago   78.8MB
nginx                   1.21-alpine   51696c87e77e   3 weeks ago      23.4MB
alpine                  3.14          e04c818066af   3 weeks ago      5.59MB
pessoa@trybe:~$
```

> Veja a diferença de tamanho das imagens! A imagem **site-hugo**, de apenas um estágio, possui `78.8MB` de tamanho, enquanto a nossa nova imagem usando múltiplos estágios, **multi-stage-site-hugo**, possui apenas `23.4MB`.

E aí, gostou dessa funcionalidade do Docker? Agora nossas imagens Docker estão cada vez mais _robustas_ 🐋.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/da25fd46-8818-4234-8603-a442b047370f/lesson/31eaceb6-7c8f-403b-82da-5743e9953d62)
