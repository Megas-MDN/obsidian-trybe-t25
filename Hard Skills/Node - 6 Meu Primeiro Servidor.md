[[Node]]



Nesta seção, você vai criar e configurar seu primeiro servidor web com Node.js usando o framework Express.

Mas espera, o que é um servidor?!🤔

![Nao estamos falando de quem te servia na cantina](https://content-assets.betrybe.com/prod/Nao%20estamos%20falando%20de%20quem%20te%20servia%20na%20cantina.jpeg)

Dica: não estamos falando sobre a cantina da escola! 🤭

## Servidores

**Servidor** ou **Server**, em inglês, como o próprio nome já diz, é quem ou aquele que serve! Eles dão às pessoas e aplicações recursos, informações e funcionalidades que elas precisam! Na área da programação, temos vários tipos de servidores, tais como:

-   Servidor Web; _(esse será nosso foco)_;
-   Servidor de arquivos;
-   Servidor de impressão;
-   Servidor de e-mail.

Anota aí 🖊: Em poucas palavras, servidores web são programas de computador que entregam algum tipo de informação ou página a quem os solicita através da internet. Toda vez que você abre seu navegador de internet e faz uma pesquisa no _Google_, é um servidor web da Google que te “responde”, trazendo o resultado da sua busca a partir das páginas e informações salvas no banco de dados da empresa.

Assim como temos vários tipos de servidores, também temos vários tipos de servidores web! Observe a seguir alguns nomes que você pode encontrar na internet:

-   Apache HTTP Server;
-   NGINX;
-   Apache Tomcat;
-   Node.js; _(Vamos focar neste)_.

Quando começamos a falar ou pesquisar mais sobre o Node.js ou node, para os íntimos 😁, alguns nomes como o já conhecido `npm` (node package manager) e o tal do `Express` também começam a surgir! Falaremos disso em breve… Por ora, continue a leitura.

## Criando sua aplicação do zero

Inicie criando os diretórios que você irá trabalhar:

```bash
mkdir soccer-team-manager soccer-team-manager/src && cd soccer-team-manager && code .
```

Aqui, você criou o diretório `src` dentro de `soccer-team-manager`, que é a pasta da sua aplicação.

> O uso da pasta `src` para organização de sua aplicação é bem comum! A sigla `src` vem de _source-code_, que podemos traduzir para o português como: “código fonte”; é aqui que você vai deixar os arquivos e diretórios da sua API!

Agora, inicie um pacote Node.js com o comando:

```bash
npm init -y
```

⚠️ Aviso: o comando acima vai criar o arquivo `package.json` para você. Com este arquivo criado e configurado, você pode instalar as dependências que usará ao longo da construção da sua API.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/8d0e802c-d620-4fd7-a424-d92d6022b09a)