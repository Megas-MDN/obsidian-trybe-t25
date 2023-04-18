[[React]]


A primeira coisa a se saber é que npm é o gerenciador de pacotes em si, ou seja, ele é quem será utilizado para instalar os pacotes em nossas aplicações React, enquanto o npx executa o comando de um pacote sem instalá-lo diretamente.

Como o create-react-app é um pacote que tem como função única a criação de todos os arquivos necessários para termos um app React, não rodamos ele mais de uma vez por projeto e nem precisamos do pacote instalado em nossas máquinas, por isso SEMPRE executamos ele com o npx e não com o npm.

Antes de iniciarmos o conteúdo, vamos testar se temos o `npm` e o `npx` estão funcionando corretamente? Para isso, criaremos uma pasta, em qualquer lugar, e vamos acessá-la por meio do terminal. Uma vez que estamos dentro da pasta, no terminal, vamos executar o comando abaixo:

```bash
npx create-react-app testando-meu-computador
```

Após o `npx` terminar de executar, ele nos mostra um mini tutorial, em que teremos uma explicação sobre os principais comandos, como na foto abaixo.

![[npx1.png]]
Imagem que demonstra os comandos básicos do npm para usar o create-react-app


Em seguida acesse a pasta:

```bash
1cd testando-meu-computador
```

Para iniciar o servidor de uma aplicação React use o comando abaixo, certificando-se de que está dentro da pasta do projeto:

```bash
1npm start
```

Após o `npm start` terminar de carregar (pode demorar um pouco), ele irá abrir uma aba em seu navegador e você verá algo parecido com o exemplo abaixo, o que significa que tudo está funcionando corretamente.

![[reactrodando.png]]
Imagem que demonstra que tudo funciona corretamente, mostrada no navegador.