[[JavaScript]]

JavaScript é uma linguagem de programação popular por poder ser utilizada para as três frentes de desenvolvimento, o frontend, o backend e o mobile. Para o backend, uma das tecnologias mais utilizadas é o Node.js.Muitas pessoas apresentam dificuldades em entender como é o funcionamento dele, em manipulá-lo para a construção de um servidor e construção de chamadas para APIs. 

Além disso, algumas pessoas podem partir direto para aprender o Node.js, sem antes verificar como é o funcionamento básico do [JavaScript](https://blog.betrybe.com/javascript/).

- [O que é o Node.JS?](#O%0dque%0dé%0do%0dNode.JS?)
- [Conheça a história do Node.JS](#Conheça%0da%0dhistória%0ddo%0dNode.JS)
- [Como funciona o Node.JS?](#Como%0dfunciona%0do%0dNode.JS?)
- [Para que serve o Node.JS? Onde usar?](#Para%0dque%0dserve%0do%0dNode.JS?%0dOnde%0dusar?)
- [Onde não usar o Node.JS?](#Onde%0dnão%0dusar%0do%0dNode.JS?)
- [O que é o NPM? O gerenciador de pacotes do Node.JS!](#O%0dque%0dé%0do%0dNPM?%0dO%0dgerenciador%0dde%0dpacotes%0ddo%0dNode.JS!)
- [O que é um módulo para Node.JS?](#O%0dque%0dé%0dum%0dmódulo%0dpara%0dNode.JS?)
- [Quais os 4 melhores módulos NPM/Frameworks do Node.JS?](#Quais%0dos%0d4%0dmelhores%0dmódulos%0dNPM/Frameworks%0ddo%0dNode.JS?)
- [Quais as vantagens do uso do Node.JS?](#Quais%0das%0dvantagens%0ddo%0duso%0ddo%0dNode.JS?)
- [Quais as desvantagens de usar o Node.JS?](#Quais%0das%0ddesvantagens%0dde%0dusar%0do%0dNode.JS?)
- [Quais as diferenças entre Node.JS e Express.JS?](#Quais%0das%0ddiferenças%0dentre%0dNode.JS%0de%0dExpress.JS?)
- [Quais são os concorrentes do Node.JS?](#Quais%0dsão%0dos%0dconcorrentes%0ddo%0dNode.JS?)
- [O que é o NVM no Node.JS?](#O%0dque%0dé%0do%0dNVM%0dno%0dNode.JS?)
- [Com quais sistemas operacionais o Node.JS é compatível?](#Com%0dquais%0dsistemas%0doperacionais%0do%0dNode.JS%0dé%0dcompatível?)


## O que é o Node.JS?

**Node.js é um ambiente de servidor de tempo de execução que usa JavaScript no lado do servidor e programação assíncrona.** É uma tecnologia gratuita e de código aberto que roda em várias plataformas (Mac OS X, Unix, [Windows](https://blog.betrybe.com/tecnologia/comandos-windows/), etc.)  
  
Com o ele podemos fazer várias coisas, como gerar conteúdo de uma página na web de forma dinâmica, coletar dados de um formulário quando ele for enviado e fazer operações de adição, exclusão e alteração em um [banco de dados](https://blog.betrybe.com/tecnologia/bancos-de-dados/), mediante a requisições de uma API, que também pode ser construída com essa ferramenta. 

### O que é um Runtime?

**Runtime, traduzindo para o Português, significa ambiente de execução.** Seja executado dentro de um navegador da Web ou fora dele, o código-fonte JavaScript que você escreve é ​​primeiro “[compilado](https://blog.betrybe.com/tecnologia/compilador-o-que-e/)” para um formato interno (uma estrutura de dados, por exemplo) e, em seguida, “executado” pelo interpretador de linguagem —  o que chamamos ambiente de execução.

A programação que você escreve diz a este interpretador o que fazer por você. Todas as linguagens interpretadas funcionam dessa maneira, como a linguagem Typescript. Com a maioria das linguagens, há mais de uma implementação disponível. 

### Por que o Node.JS é tão popular?

**Um dos principais fatores por trás da popularidade do Node.js entre os desenvolvedores e desenvolvedoras é seu suporte a milhares de bibliotecas de código aberto**, a maioria hospedadas no site do NPM.  
  
Há também uma comunidade muito ativa em torno dele com muitos eventos e conferências para pessoas programadoras, incluindo Node.js Interactive, Node.js Summit e NodeConf, além de outros eventos regionais.  
  
Os [frameworks](https://blog.betrybe.com/framework-de-programacao/o-que-e-framework/) da Web foram desenvolvidos pela comunidade de código aberto da ferramenta para acelerar o desenvolvimento de aplicativos. Essas estruturas incluem Connect, Sails.js, Koa.js, Express.js, Feathers.js, socket.io, Derby, Hapi.js, Meteor e muito mais. Veremos alguns detalhes de frameworks do Node.js nas seções seguintes.

## Conheça a história do Node.JS

**Em 2009, ano de criação do Node.js por Ryan Dahl, a ferramenta era compatível apenas com os** [**sistemas operacionais**](https://blog.betrybe.com/tecnologia/sistema-operacional-tudo-sobre/) **MacOS e Linux**. Dahl liderou o desenvolvimento e manutenção e mais tarde foi patrocinado pela Joyent.  
  
As possibilidades limitadas do servidor web mais popular na época, o Apache HTTP Server em 2009, foi criticado por Dahl porque tinha que lidar com muitas conexões simultaneamente (até 10.000 e mais).  
  
Quando havia algum código bloqueado em todo o processo, ou uma pilha de execução múltipla implícita em casos de conexões simultâneas, isso levava a problemas, e essa situação tinha que ser resolvida criando código por meio de programação sequencial.  
  
Em 8 de novembro de 2009, no JSConf europeu inaugural, o projeto Node.js foi demonstrado pela primeira vez por Dahl. Ele é uma combinação do mecanismo V8 JavaScript Chrome, uma API de entrada e saída de baixo nível e um laço de repetição de eventos.  
  
Como muitos navegadores competiam para oferecer às pessoas usuárias o melhor desempenho, os mecanismos [JavaScript](https://blog.betrybe.com/javascript/) também se tornaram consideravelmente melhores. Os principais navegadores trabalharam duro para encontrar maneiras de tornar o JavaScript mais rápido e oferecer melhor suporte para ele.  
  
Assim, o Node.js foi construído no lugar e na hora certos. Ele introduziu muitas abordagens para o desenvolvimento do lado do servidor JavaScript e um pensamento inovador que ajudou muitas pessoas.  
  
Vejamos, a seguir, uma linha do tempo dos principais acontecimentos envolvendo o Node.js:

**Ano**

**Acontecimentos**

2009

O início do Node.js;  
NPM foi criado.

2010

O início do Express;  
O início do socket.io.

2011

A versão 1.0 do NPM é lançada;  
Empresas Uber, LinkedIn etc. começaram a adotar o Node.js.

2012

Adoção continua crescendo rapidamente.

2013

O Ghost foi a primeira grande plataforma de blog a usar Node.js.

2014

O IO.js tornou-se um grande fork do Node.js, “The Big Fork”, para introduzir suporte ao ES6 e mover-se mais rápido.

2015

A Fundação Node.js começou;IO.js é mesclado de volta ao Node.js;NPM introduz módulos privados;Node.js 4 (versões 1, 2 e 3 nunca lançadas anteriormente).

2016

O início do [Yarn](https://blog.betrybe.com/desenvolvimento-web/yarn/);O início do Node.js 6.

2017

NPM se concentra mais na segurança;  
O início do Node.js 8;  
HTTP/2;  
A V8 o introduz em seu conjunto de testes, tornando-o oficialmente um alvo para o mecanismo JS, além do Chrome;  
Até 3 bilhões de downloads de pacotes do NPM, semanalmente.

2018

O início do Node.js 10;  
Módulos ES suporte experimental .mjs.

2019

O início do Node.js 12 – 13;  
O trabalho no Deno começou a mover o JS do lado do servidor para a próxima década com suporte moderno a JavaScript.

2020

O início do Node.js 14 – 15;  
GitHub (de propriedade da Microsoft) adquiriu o NPM.

## Como funciona o Node.JS?

Se você está familiarizado com JavaScript, então consegue diferenciar o que é assíncrono e síncrono. Um thread único é uma sequência de eventos responsáveis por executar todas as funções e solicitações. **O comportamento assíncrono é extremamente importante quando se utiliza o Node.js, pois garante que a sequência de eventos (event loop) nunca seja bloqueada por uma função síncrona**.

![Ilustração de como funciona o Node.js](https://u3r3f6s2.rocketcdn.me/wp-content/uploads/2022/10/image1.png)

Mesmo que haja apenas um laço de eventos, quando uma solicitação é feita, a sequência passa a solicitação para uma função assíncrona, que faz o trabalho. Quando essa função é concluída e uma resposta é retornada, ela pode ser passada de volta ao laço de eventos para ser executada pelo retorno de chamada e enviada ao usuário.  
  
Se as funções fossem síncronas, a sequência de eventos ficaria bloqueada com uma solicitação e resposta de um cliente, e todos os outros clientes teriam que esperar até que o cliente terminasse. Devido à natureza assíncrona do JavaScript, os aplicativos que usam o Node.js podem lidar com muitas solicitações acontecendo ao mesmo tempo. 

Isso significa que ao programar em Node.js é importante sempre ter em mente que as funções que estão sendo escritas não são síncronas. 

### Entenda o funcionamento do Node.JS na prática!

Vejamos um exemplo de bloqueio de um dispositivo de entrada e saída (E/S), diferenciando um servidor comum, que utilize linguagens como Java, PHP, dentre outras e um que utilize o Node.js.  

Um servidor com bloqueio seria quando, por exemplo, seu código “paralisa” em uma linha e espera a operação terminar. Nesse período, sua máquina está segurando memória e tempo de processamento para uma _thread_ que não está fazendo nada. 

Dessa forma, seu servidor pode gerar mais _threads_ para atender a solicitação. Isso tem como resultado a realização de mais configurações, mais memória consumida, mais processamento. Inviável, não acha? 

Em contraste, **servidores sem bloqueio, como os criados no Node.JS, usam apenas uma** **_thread_** **para atender a todas as solicitações**. Apesar de parecer algo que seria desprezível, as pessoas criadoras o projetaram com a ideia de que a E/S seria o gargalo, e não os cálculos. Assim, quando as solicitações chegam ao servidor, elas são feitas uma de cada vez. 

Quando o código atendido precisa consultar o banco de dados, por exemplo, ele envia uma solicitação ao banco de dados. No entanto, em vez de esperar pela resposta e parar, ele envia o retorno de chamada para uma segunda fila e o código continua em execução. 

Agora, quando o banco de dados retorna dados, o retorno de chamada é enfileirado em uma terceira fila onde eles estão com execução pendente. Quando o mecanismo não está fazendo nada (pilha vazia), ele pega um retorno de chamada da terceira fila e o executa. 

Observemos a imagem a seguir que, exibe como é essa diferenciação entre um servidor que utiliza o Node.js, em comparação com um servidor tradicional:

![Comparação entre o Node.js e o modelo tradicional](https://u3r3f6s2.rocketcdn.me/wp-content/uploads/2022/10/image-100.png)

## Para que serve o Node.JS? Onde usar?

**O Node.js, na maioria dos projetos, é utilizado para a construção de APIs e de aplicações de bate-papo.** Porém, ele pode ser utilizado para construção de aplicações no frontend, utilizando o que chamamos _handlebars,_ que seriam templates para a criação do HTML ser exibido na página.  
  
Observemos a listagem abaixo, que indica onde podemos utilizar essa tecnologia:

-   Construção de backends e servidores;
-   Construção de frontends;
-   Desenvolvimento de [APIs](https://blog.betrybe.com/desenvolvimento-web/api/);
-   Criação de [microsserviços](https://blog.betrybe.com/tecnologia/microsservicos/);
-   Construção de aplicativos para conversas em tempo real (chat), utilizando socket.io;
-   Desenvolvimento de scripts para automação de tarefas; 

Alguns exemplos de usuários corporativos do software Node.js incluem IBM, LinkedIn, Microsoft, Netflix, PayPal, SAP e Yahoo.

## Onde não usar o Node.JS?

**O uso do Node.js não é recomendado se você está utilizando um banco de dados relacional,** como PostgreSQL, MySQL, SQL Server.

As estruturas ORM (Object-Relational Mapping, ou em português, mapeamento objeto-relacional), são utilizadas para haver conexões com os bancos de dados relacionais, utilizando pacotes adicionais do NPM, tais como o Sequelize e o TypeORM.

Ele também não é recomendado para ser utilizado em aplicações complexas, consideradas grandes. A seguir, vejamos como é o funcionamento do seu gerenciador de pacotes, o NPM. 

## O que é o NPM? O gerenciador de pacotes do Node.JS!

**As letras** **npm** **significam “Node Package Manager”**. Quando você está trabalhando em um projeto JavaScript, você pode usar o NPM para instalar os pacotes de código de outras pessoas em seu próprio projeto. Seu projeto pode ser um projeto da Web, como um site ou aplicativo da Web, ou pode ser um projeto do lado do servidor usando Node.js. Qualquer projeto JavaScript pode usar NPM para extrair pacotes de código existentes.  
  
O NPM é uma ferramenta que você instala no seu computador. Faz parte do Node.js, portanto, instale a versão LTS do Node para obter os comandos dele na linha de comando. Ele deve ser instalado em todos os computadores em que você deseja trabalhar em seu projeto, portanto, se você mover seus arquivos usando uma unidade USB, não esqueça da instalação da versão LTS do Node.

Vamos imaginar um exemplo de uma agência de Correios. Quando você quer instalar uma dependência em seu projeto, você digitará o comando **_npm install_** no terminal. Pois bem, isso pode ser assimilado, como a imagem abaixo, de uma encomenda sendo entregue a você, em seu domicílio:

![Ilustração mostrando o funcionamento do npm install](https://u3r3f6s2.rocketcdn.me/wp-content/uploads/2022/10/image3.png)

Agora, caso você construa uma funcionalidade e deseje adicionar ela no NPM, você estaria “enviando” a sua encomenda, que teria o destino a publicação no site do NPM, conforme a foto abaixo:

![Como funciona npm publish](https://u3r3f6s2.rocketcdn.me/wp-content/uploads/2022/10/image4.png)

Digitando o comando **_npm publish_**, você estará publicando sua aplicação no site do gerenciador de pacotes do Node.js e contribuindo para a comunidade de desenvolvimento crescer cada vez mais. 

## O que é um módulo para Node.JS?

**Um módulo, ou pacote, significa qualquer pedaço de código que um programador ou programadora publicou no NPM.** Você usa esse gerenciador de pacotes na linha de comando para instalar, desinstalar ou atualizar módulos. Alguns exemplos de módulos NPM são:

-   Express;
-   MongoDB; 
-   Lodash; 
-   Nodemailer.

Existem milhares de módulos publicados no NPM. Você pode navegar por eles no [site do NPM,](https://npmjs.com/) mas normalmente você encontrará pacotes recomendados pesquisando no Google. Alguns módulos são adequados apenas para projetos da Web e alguns são adequados apenas para projetos de Node.js. Na seção, a seguir, explicaremos alguns dos principais módulos existentes no NPM. 

## Quais os 4 melhores módulos NPM/Frameworks do Node.JS?

1.  **MongoDB:** pretende ajudar os desenvolvedores e desenvolvedoras a resolver seus problemas relacionados a dados, graças ao modelo de dados flexível e à interface de consulta unificada para qualquer caso de uso. Isso permite enviar e iterar de 3 a 5 vezes mais rápido em qualquer ambiente;
2.  **Nodemailer:** Realiza a tarefa de enviar e-mails dentro do seu aplicativo. Além disso, o Nodemailer protege o gerenciamento de e-mail para que seus clientes tenham acesso a um espaço seguro para envio de mensagens;
3.  **Lodash:** ela é uma biblioteca de utilitários JavaScript popular e altamente usada. Ele oferece modularidade, desempenho, extras e expõe métodos úteis em arrays JS, objetos e outras estruturas de dados.
4.  **Express:** um framework presente no NPM, para auxiliar na criação de servidores e roteamento para requisições a serviços externos. Ele tem uma função chamada Router, que permite criar chamadas para APIs em poucas linhas. 

## Quais as vantagens do uso do Node.JS?

A seguir, veremos as principais vantagens de se utilizar o Node.js:

-   Fácil de aprender;
-   Alto grau de escalabilidade para os projetos;
-   É usado como uma linguagem de programação única;
-   Oferece alto desempenho no desenvolvimento de uma aplicação;
-   O ambiente de tempo de execução de código aberto também oferece o recurso de armazenamento em cache de módulos únicos;
-   As pessoas desenvolvedoras podem obter um suporte estendido para as várias ferramentas comumente usadas;
-   É conhecido por ser altamente extensível, o que significa que você pode personalizar e estender ainda mais de acordo com seus requisitos, como a troca de dados via JSON entre as APIs e comunicações entre cliente e [servidor](https://blog.betrybe.com/tecnologia/o-que-e-servidor/).

## Quais as desvantagens de usar o Node.JS?

**Conforme visto anteriormente, utilizar o Node.js em conjunto com um** [**banco de dados relacional**](https://blog.betrybe.com/tecnologia/banco-de-dados-relacional/) **pode ser um problema.** Além disso, sua utilização não é recomendada para aplicativos web que sejam grandes e complexos.

## Quais as diferenças entre Node.JS e Express.JS?

A diferença entre esses dois termos é a de que, enquanto o **Node.js é uma plataforma para criar aplicativos de E/S orientados a eventos do lado do servidor usando JavaScript, o Express.js é um framework baseado em Node.js para desenvolvimento de aplicações web usando os seus princípios e métodos**. 

Utilizando o Express.js, conseguiremos manipular requisições a uma API de forma simples, bem como o gerenciamento do servidor, comparando com a utilização apenas do Node.js para esses fins. Ou seja, o Express.js é uma biblioteca presente no ecossistema do Node.js para facilitar o manuseio de dados e roteamento das requisições.  

## Quais são os concorrentes do Node.JS?

### Elixir

**Elixir é uma linguagem funcional dinâmica usada para criar aplicativos que podem ser mantidos facilmente.** A linguagem usa a plataforma de máquina virtual Erlang (BEAM), conhecida por executar sistemas com baixa latência e alta tolerância a falhas. A linguagem, portanto, fornece às pessoas desenvolvedores uma ferramenta para criar aplicativos relacionados com redes.

Assim, enquanto o Elixir pode executar tarefas de forma simultânea, mantendo as independentes de outros recursos, ele também possui alta simultaneidade. Já o Node.js, suporta um paradigma de programação orientado a eventos assíncronos.

### Scala

**Scala é uma abreviação da palavra Scalable Language (em português, Linguagem Escalável).** Ou seja, isso indica que a linguagem de programação Scala tem a possibilidade de crescer com o crescimento dos aspectos técnicos do seu programa. 

As pessoas programadoras podem praticar com a linguagem digitando expressões de uma linha e analisando os resultados ou podem usar essa linguagem para missões de programação técnica em grande escala.

Nesse caso, enquanto Scala é uma linguagem de programação de uso geral que fornece suporte para programação orientada a objetos, o Node.js é um ambiente de tempo de execução JavaScript de código aberto e multiplataforma que executa código JavaScript fora de um navegador da web.

### Go

**A linguagem Go (ou Golang) é uma das linguagens de programação que mais crescem.** É uma linguagem de código aberto lançada pelo Google em 2009 e criada por Ken Thompson (designer e criador do UNIX e C), Rob Pike (co-criador do formato UTF 8 e UNIX) e Robert Griesemer. É uma linguagem de programação multifuncional projetada especificamente para criar aplicativos escaláveis ​​e mais rápidos.

Assim, enquanto Golang é uma linguagem de programação com tipagem estática que permite alto desempenho, o Node.js é um ambiente de tempo de execução multiplataforma (não uma linguagem ou estrutura). Ou seja, enquanto a linguagem Go funciona por si só, o Node.js auxilia o JavaScript a funcionar como uma linguagem do lado do servidor.

## O que é o NVM no Node.JS?

**O NVM (Node Version Manager, ou Gerenciador de Versões do Node) é uma forma de gerenciamento de várias versões existentes do Node.js.** Como ele é uma ferramenta em constante atualização com o passar dos anos, em nossa aplicação, facilmente podemos nos perder quando o assunto é versionamento, pois podemos ter uma versão desatualizada.

Ou seja, o NVM é uma maneira de gerenciarmos versões do Node.js, para garantir o funcionamento correto de uma aplicação em determinada versão. Ele permite que as pessoas desenvolvedoras: 

-   Baixem localmente qualquer uma das versões remotas do Long Term Support (LTS) do Node.js com um comando simples;
-   Alternar facilmente entre várias versões, diretamente da linha de comando;
-   Configurar caminhos para alternar facilmente entre diferentes versões baixadas do Node.js.

## Com quais sistemas operacionais o Node.JS é compatível?

**O Node.js é compatível com os sistemas operacionais mais utilizados, como Windows, Linux e MacOs.** No Windows, ele é compatível a partir da versão 7 desse sistema operacional. Ele está com suporte nos sistemas operacionais SmartOS e IBM AIX e, possui um suporte em fase experimental com o FreeBSD.  

O Node.js é um framework que permite a criação de APIs, aplicações de chat e microsserviços. **Possui facilidade em seu aprendizado e utiliza o JavaScript para executar essa linguagem pelo lado do servidor.** Ele não é recomendado para ser utilizado em conjunto com bancos de dados relacionais, tais como MySQL, PostgreSQL.

Ele possui o gerenciador de pacotes NPM para serem adicionados recursos extras a uma aplicação que utilize Node.js. **Esses recursos são chamados de módulos e pacotes e podem auxiliar em diversas coisas.** Basicamente, ele é compatível com os sistemas operacionais mais comuns entre desenvolvedores e desenvolvedoras, tais como Windows, MacOs e Linux.


#### Recursos adicionais

-   [NPM Comandos Cheat Sheet](https://github.com/tryber/Trybe-CheatSheets/blob/master/backend/nodejs/npm/README.md)
-   [Documentação oficial do Node.js](https://nodejs.org/en/docs/)
-   [Documentação oficial do NPM](https://docs.npmjs.com/)
-   [Vídeo: Node.js // Dicionário do Programador](https://www.youtube.com/watch?v=vYekSMBCCiM&t=426s)
-   [Sobre Versionamento Semântico](https://semver.org/lang/pt-BR/)
-   [O guia completo do package.json do Node.js](https://www.luiztools.com.br/post/o-guia-completo-do-package-json-do-node-js/)
-   [Tudo que você queria saber sobre o package-lock.json, mas estava com vergonha de perguntar](https://medium.com/trainingcenter/tudo-que-voc%C3%AA-queria-saber-sobre-o-package-lock-json-mas-estava-com-vergonha-de-perguntar-e70589f2855f)
-   [Entendendo módulos ES6](https://medium.com/trainingcenter/entendendo-m%C3%B3dulos-no-javascript-73bce1d64dbf)
-   [CommonJS vs. ES Modules: Modules and Imports in NodeJS](https://reflectoring.io/nodejs-modules-imports/)
-   [Dissertação sobre as principais Licenças de Software](https://www.teses.usp.br/teses/disponiveis/45/45134/tde-14032012-003454/publico/MestradoVanessaSabino.pdf)
-   [Como funcionam as licenças open source?](https://medium.com/code-prestige/como-funcionam-as-licen%C3%A7as-open-source-9ff1da677ccd)
-   [O lado Legal do Open Source](https://opensource.guide/pt/legal/)
-   [Vídeo do canal Código Fonte explicando sobre Licenças de Software](https://www.youtube.com/watch?v=fPfzp6ov2bQ)


###### Fonte: [Blog Trybe](https://blog.betrybe.com/nodejs/)