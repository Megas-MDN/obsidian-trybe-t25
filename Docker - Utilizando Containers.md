[[Docker]]

## Introdução - Manipulação e Criação de Imagens no Docker

### O que vamos aprender?

Antes de seguirmos com os aprendizados sobre Docker, vamos relembrar tudo o que aprendemos no conteúdo anterior?

-   Empacotamento de aplicações;
-   Quais são os problemas que o **Docker** se propõe a resolver;
-   Aspectos da **arquitetura do Docker**;
-   Principais **comandos para utilização do Docker**;
-   Como **rodar imagens do Docker Hub** (repositório oficial de imagens do Docker).

Agora, chegou o momento de aprofundarmos nosso conhecimento sobre Docker!🐋

Hoje, vamos entender o objetivo de cada comando de Docker, seu uso e suas relações. E tem mais! Também vamos criar imagens _Docker_ para nossas aplicações utilizando os padrões e boas práticas do mercado.

### Você será capaz de

-   Criar imagens **do zero** no Docker;
-   Criar imagens Docker usando outras imagens como base;
-   Aplicar boas práticas e padrões na criação de imagem;
-   _Dockerizar_ suas aplicações, ou seja, criar uma imagem Docker com tudo que é necessário para executar seus projetos na hora!

### Por que isso é importante?

Distinguir as definições de imagem e container é algo muito importante!

> Uma **imagem Docker é um arquivo imutável e a partir dele um ou mais containers podem ser gerados**. Essa imagem pode ser criada a partir do comando `docker build`, seguindo as instruções contidas em um arquivo chamado `Dockerfile`.

Frequentemente no contexto de programação, o termo `build` _(‘construir’ em português)_ se refere ao trabalho de obter todo o nosso projeto (código-fonte, imagens, dependências), e a partir dele construir um produto final que seja executável e melhor de distribuir.

O `Dockerfile` é um arquivo que contém as instruções necessárias _(como uma receita)_ para construirmos a imagem Docker exatamente como desejamos. Esse arquivo nos mostra as bibliotecas que devem ser instaladas, arquivos que devem ser inicializados etc.

![Fluxo do dockerfile](https://content-assets.betrybe.com/prod/1fdff935-1d56-4c71-9b2f-7b1443bacbec-Fluxo%20do%20dockerfile.png)

> Um **container Docker é um processo Linux totalmente isolado**. Para que possamos executar esse container é necessário definirmos qual imagem Docker vamos utilizar. Mas e se não tivermos essa imagem Docker localmente em nossa máquina? 🤔

⚠️**Importante**: se tentarmos executar um novo container com `docker run <imagem>`, mas não tivermos essa `<imagem>` _(vamos supor aqui o `hello-world`)_ localmente, ele nos retorna a seguinte mensagem abaixo:


```bash
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
```

Essa mensagem indica que o Docker baixou e armazenou a imagem localmente. A partir disso, sempre que o Docker precisar utilizar esta imagem, ele usará nossa cópia local!

Para avançarmos ainda mais nesse mundo de Docker, hoje veremos onde encontrar essas imagens baixadas e como criar imagens Docker, além de como manipulá-las e removê-las. Vamos mergulhar fundo nesse conteúdo? 🐋

run => executa no build  
ENTRYPOINT => sempre executa obrigatoriamente  
CMD => nem sempre executa - opcional

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/da25fd46-8818-4234-8603-a442b047370f/lesson/670cdc27-f578-4733-907e-87652c46c002)
