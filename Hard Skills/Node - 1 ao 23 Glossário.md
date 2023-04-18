[[Node]]

## Módulos

Módulos são como “caixinhas” que isolam suas funções, variáveis e afins de outras partes do código. **O Node.js possui três tipos de módulos:**

1.  **Módulos internos**: também chamados de _core modules_, são módulos que já vem com o Node.js quando baixamos o _runtime_.
2.  **Módulos locais**: são aqueles criados por nós na nossa máquina. Eles representam as funcionalidades ou partes do nosso programa que foram separados em arquivos diferentes.
3.  **Módulos externos**: são módulos publicados no NPM, que as pessoas podem baixar e utilizar em suas aplicações.

## Node.js

O Node.js é um interpretador de JavaScript construído a partir do V8 (interpretador utilizado pelo Google Chrome) e que permite a execução de códigos JavaScript fora de navegadores web. De forma resumida, ele nos permite utilizar o JavaScript no backend da aplicação.

## NPM

O [NPM](https://www.npmjs.com/) é o site em que são publicados os pacotes Node.js. Dados do site [ModuleCounts.com](http://www.modulecounts.com/) mostram que atualmente o NPM está entre os repositórios com maior número de pacotes.

## npm

`npm` é a ferramenta de linha de comando(CLI) que realiza o gerenciamento dos pacotes Node.js para nós.

> [Neste repositório](https://github.com/tryber/Trybe-CheatSheets/blob/master/backend/nodejs/npm/README.md) você encontra uma lista para consultas rápidas dos principais comandos `npm` (Cheat Sheet).

## Pacote

Um pacote é um conjunto de arquivos que exportam um ou mais módulos Node.js.

## package.json

É onde estão algumas configurações importantes para o nosso pacote como nome, versão, dependências e **scripts**.

## Promises

Promise é um objeto usado para processamento assíncrono. Uma Promise (de “promessa”) representa um valor que pode estar disponível agora, no futuro ou nunca. Se o código é executado sem nenhum problema, ela é resolvida por meio da função `resolve`; se algo de errado acontecer durante a execução, ela é rejeitada por meio da função `reject`.

## Scripts

São “atalhos” que podemos definir para executar determinadas tarefas relacionadas ao pacote atual. Eles são criados no arquivo `package.json`, mais especificamente no objeto `scripts`. Lá, definimos o par de chave e valor correspondentes ao nome que usaremos para chamar o script e o que será executado ao chamá-lo, respectivamente.

## C.R.U.D. (ou CRUD)

Esse é um acrônimo para um conjunto de operações muitíssimo comuns no mundo do desenvolvimento, elas são:

-   **C**reate: Criar;
-   **R**ead: Ler;
-   **U**pdate: Alterar;
-   **D**elete: Deletar;

## Dependências e dependências de dependências

O **Package.json** é o arquivo onde estão listadas todas as dependências de um projeto. Lá estão sinalizados quais são os pacotes essenciais para o funcionamento da nossa aplicação, tanto em produção (na chave `dependencies`), quanto em desenvolvimento (na chave `dev-dependencies`).

Já o **package-lock.json** é um arquivo bem maior, pois lista também as dependências de nossas dependências, garantindo que tudo que nossa aplicação precisa para rodar está descrito ali. O Node se encarrega de que sempre que instalamos um pacote, os pacotes dos quais ele depende serão instalados junto.

Enquanto isso, a **node_modules** é onde todas as nossas dependências e dependências de nossas dependências efetivamente estão instaladas.

## Framework Express

A palavra _framework_, quer dizer estrutura ou molde e é basicamente isso que ela é para uma aplicação. O framework é como um template, que te sugere uma forma específica de construir sua aplicação e te dá ferramentas pra fazer isso mais rápido.

O **Express** é um _framework_ que nos ajuda a organizar e construir APIs robustas e flexíveis, nos dando ferramentas que fazem as coisas acontecerem com poucas linhas de código, abstraindo a lógica e códigos por trás de funcionalidades muito comuns nas aplicações.

## Métodos de envio

Temos 3 métodos de envio:

-   Envio por **parâmetros de consulta ou query params**: Muito utilizado e amplamente visto em sites na internet.
    
    > Um exemplo de uso é o próprio site de pesquisa do Google, o qual envia o que foi pesquisado pela URL do seu navegador, por exemplo: `https://www.google.com.br/search?q=Trybe`;
    
-   Envio por **parâmetros de rota ou route params**: Também muito utilizado, mas este geralmente é visto em sites de produtos.
    
    > Um exemplo de uso são os e-commerces, quando clicamos em algum produto para ver a página específica dele, por exemplo: `https://www.kabum.com.br/produto/128561`;
    
-   Envio por **body**: Usado para envio de dados sensíveis/sigilosos, utilizado principalmente em formulários e juntamente com outros artefatos, dá maior segurança para sua aplicação.
    
    > Um exemplo de uso é o próprio login do course da Trybe.
    

## Portas

Cada programa tem uma porta atribuída a ele, que é representada por um número. A função dessa porta é identificar para onde serão direcionadas as requisições feitas para aquele programa. Dizemos que um programa está “ouvindo”, do inglês “listen”, uma porta quando ele está alocado pelo sistema operacional pra ela.

## Protocolo

Protocolo é uma convenção que padroniza algo. O protocolo HTTP, que tanto usamos, é uma convenção que padroniza a conexão, comunicação e transferência de dados, entre dois sistemas.

## Rotas

Também são chamadas de caminhos, _paths_ e _endpoints_ de uma API. São a parte de uma URL que usamos para acessar uma API e fazer uma requisição a ela. Por meio dela requisitamos acesso, criação, leitura ou remoção de informações em nossas APIs. Em suma, quando você digita uma URL no navegador, por “trás dos panos” ele está fazendo uma requisição àquela rota.

## Servidores web

São nada mais que programas de computador que entregam algum tipo de informação ou página solicitados via internet. Sempre que você abre seu navegador de internet e faz uma pesquisa no Google, é um servidor web da Google que te “responde”, trazendo o resultado da sua busca a partir das páginas e informações salvas no banco de dados da empresa.


## Assertion

Para de fato testar nossa função, precisamos chamá-la passando o input desejado e então validar se a resposta é aquela que esperamos. Essa validação é o que chamamos de _assertion_, **“asserção”** ou, em alguns casos, **“afirmação”**.

> Sabia que existe um padrão de teste chamado de [**Triplo A**](https://medium.com/@pablodarde/o-padr%C3%A3o-triple-a-arrange-act-assert-741e2a94cf88), cuja estrutura de testes apresenta 3 seções distintas: Ajeitar, Atuar e Afirmar (AAA)?
> 
> **1º A** - Ajeitar (arrange): Criação de todo o código de configuração para levar o sistema ao cenário que o teste pretende simular.
> 
> **2º A** - Atuar (act): Execução dos testes em si.
> 
> **3º A** - Afirmar (assert): Verificação de que o valor recebido satisfaz a expectativa.

## Chai

O [chai](https://www.chaijs.com/api/bdd/) é uma biblioteca de asserção que auxilia o desenvolvimento de testes com Node.js e que pode ser combinada com qualquer framework de testes JavaScript.

## Contratos de APIs

O contrato define como a API deverá se comportar em um determinado cenário. Informações como `Estrutura de Requisição`, `Método HTTP`, `Status Code`, e `Estrutura de Resposta` são comumente utilizadas em contratos de API.

## Mocha

O **[mocha](https://mochajs.org/) é um _framework_ de testes para JavaScript**, isso significa que ele nos ajuda a arquitetar os nossos testes fornecendo a estrutura e interface para escrevermos e executarmos eles.

## Sinon

O [Sinon](https://sinonjs.org/) é uma ferramenta que auxilia na criação e utilização dos dublês, fornecendo funções para diversos tipos de **`Test Doubles`**.

> Os **dublês de teste** são substitutos que sobrepõem dependências necessárias para se testar um sistema ou um comportamento.

## Testes automatizados

De forma simplificada, nos testes automatizados escrevemos um script com a configuração das funções, pré-condições, casos de teste e resultados esperados. Ao ser executado, este script irá executar os testes, comparar os resultados obtidos com os resultados esperados gerar o relatório de teste.

O principal interesse nesse tipo de teste é permitir que tarefas repetitivas e demoradas não consuma o tempo das pessoas, permitindo melhor foco em tarefas de maior valor e que dependem da interpretação humana, como o [teste exploratório](https://www.atlassian.com/br/continuous-delivery/software-testing/exploratory-testing#:~:text=Testes%20explorat%C3%B3rios%20%C3%A9%20a%20abordagem,no%20escopo%20de%20outros%20testes).

## Testes Manuais

Nos testes manuais, reexecutamos o código algumas vezes, buscando validar se o comportamento que queremos está sendo realizado corretamente e também alteramos os parâmetros de entrada para tentarmos garantir que tal funcionamento se mantenha mesmo com essas variações.

## Tipos de teste

Levando em consideração o **escopo** e a **interação** dos testes, os tipos de teste mais comuns são:

1.  **Testes unitários**: consideram um escopo limitado a um pequeno fragmento do seu código com interação mínima entre recursos externos.
    
2.  **Testes de integração**: presumem a junção de múltiplos escopos (que tecnicamente devem possuir, cada um, seus próprios testes) com interações entre eles.
    
3.  **Testes de Ponta-a-ponta**: também chamados de Fim-a-fim _(End-to-End; E2E)_, pressupõem um fluxo de interação completo com a aplicação, de uma ponta a outra. Esse teste é o mais completo, pois necessita que todos os demais testes tenham sido desenvolvidos.
    

> Lembre-se que nenhum tipo de teste é mais importante que o outro, é a combinação entre eles que vai garantir a qualidade do seu código. 😉

## TDD - Desenvolvimento Orientado a Testes

**`TDD` (Test Driven Development)**, ou em bom português, _Desenvolvimento Orientado a Testes_, tem como ideia central começarmos a escrita do código tendo em mente quais cenários devemos cobrir e também como nosso código precisa estar estruturado para que possamos testá-lo. Ele pode ser empregado nos diferentes tipos de teste e resumindo em quatro passos sua implementação, teríamos:

1️⃣ **Interpretação os requisitos**: devemos pensar nos comportamentos que vamos implementar e na estrutura do código: se será uma função, um módulo, quais os inputs, os outputs, etc.

2️⃣ **Início da escrita de testes**: descrevemos quais cenários da nossa aplicação iremos verificar.

3️⃣ **Asserções**: escrevemos as respostas esperadas para cada cenário.

> Perceba que antes mesmo de ter qualquer código, já vamos criar chamadas a ele, o que significa que nossos testes irão falhar. Não se preocupe, pois essa é exatamente a ideia nesse momento.

4️⃣ **Implementação/Refatoração do código**: feita logo após a criação dos testes.

> A ideia é escrever os códigos pensando nos testes e, conforme vamos cobrindo os cenários, nossos testes que antes quebravam começam a passar.


## Middlewares

Para o Express, um [middleware](https://expressjs.com/pt-br/guide/using-middleware.html) é uma função que realiza o tratamento de uma requisição HTTP e que pode responder essa request(`res`) ou chamar o próximo middleware (`next`).

### CORS

CORS é a sigla de _Cross-origin Resource Sharing_. Ele é um middleware utilizado pelos navegadores para compartilhar recursos entre diferentes origens. Um exemplo disso é uma aplicação front-end rodando em um _endpoint_ (`localhost:3000`) que tenta acessar uma API que está rodando em outro _endpoint_ (`localhost:3001`). A função do CORS aí seria basicamente gerenciar se essa API poderia ou não receber as requisições dessa aplicação.

### Express.json

É um middleware nativo do _Express_ que lê o conteúdo da requisição HTTP, interpreta os conteúdos como JSON e cria no objeto `req` uma propriedade `body` com o valor encontrado no conteúdo.

### Express.static

Este é outro middleware que já vem com o Express. Ele faz a busca por um arquivo por meio do `req.path`. Caso ele encontre, já responde a requisição com esse arquivo. Caso não encontre, ele assume que alguém vai responder essa requisição e simplesmente passa para o próximo.

### Middleware de erro

São identificados pelo Express pela quantidade de parâmetros e por isso apresentam **obrigatoriamente quatro parâmetros: `err, req, res, next`**.

É possível encadear vários middlewares de erro apenas colocando-os na sequência em que devem ser executados, mas atenção: eles **sempre devem vir depois de rotas e outros middlewares**!

Além disso, middlewares de erro **só recebem requisições se algum middleware lançar um erro ou chamar `next(err)` com algum parâmetro**.

### Middleware de validação

O Express permite que o **tratamento de uma rota seja feito por vários middlewares em conjunto**, cada um fazendo uma parte do tratamento da requisição. Nesse sentido, podemos criar um ou vários middlewares de validação, como um responsável por verificar se um id é válido, por exemplo.

Validações não costumam ser o objetivo final das requisições e por isso **middlewares de validação costumam ter o parâmetro `next`, além dos já conhecidos `req` e `res`**, para que após fazer a validação pertinente possam, em seguida, escolher entre responder (`res`) a requisição ou chamar o próximo middleware (`next`).

### Middlewares globais

São middlewares que interceptam todas ou quase todas as rotas. De forma simplista, para que um middleware seja aplicado em todas as rotas basta que ele seja usado (`app.use`) antes das rotas no código.

### Morgan

É um middleware de logs de requisições do Node.js. Com ele, podemos monitorar informações sobre as requisições feitas para uma API, como o método utilizado (`POST`, `PUT`, `GET`, etc.) e o status code da resposta, por exemplo.

### Router

Este é mais um middleware nativo do _Express_ e é **utilizado para agrupar várias rotas em um mesmo lugar**, trazendo mais organização para o código, e depois é passado no arquivo que lê as rotas, geralmente o `app.js` em nossos exemplos.


## Docker Compose

É uma ferramenta para definir e executar aplicações Docker de vários containers. Utiliza-se um um arquivo `yaml` para definir as configurações dos serviços daquela aplicação, que serão iniciados com um único comando: `docker compose up`.

## Pool de conexões

Um pool de conexões é um repositório com um conjunto de conexões estabelecidas previamente com o banco de dados. Essas conexões serão reutilizadas durante a execução da aplicação conforme a necessidade, ou seja, se uma API recebe duas ou mais requisições simultâneas, ela usará as conexões disponíveis para atender as requisições com melhor desempenho.

Utilizando uma analogia, o pool de conexões é como um estojo com vários lápis do qual você pode retirar um sempre que precisar e, assim que aquele lápis não for mais necessário pra você, você pode devolver ao estojo para que ele esteja disponível da próxima vez que você precisar dele.

## Prepared statements

São como um template ou um molde para consultas SQL que uma aplicação deseja executar, e que pode ser customizado utilizando variáveis de parâmetros (os placeholders ou marcadores).

São caracterizados pela chamada da função `conn.execute()` com os dois parâmetros: uma string que contém uma _query_ do MySQL construída utilizando _placeholders_ (representados pelo sinal `?`) e um array de valores que substituirão esses _placeholders_, seguindo a mesma ordem nos quais eles foram declarados.

## Variáveis de ambiente

As variáveis de ambiente são cadeias de caracteres que contêm informações sobre o ambiente do sistema e sobre o usuário que está conectado no momento. Seu formato é definido por NOME_DA_VARIÁVEL=VALOR, onde NOME_DA_VARIÁVEL é o nome da variável de ambiente, e VALOR se refere a um valor que será vinculado à variável.

São comumente usadas para guardar chaves e senhas, evitando sua exposição, ou outras configurações do sistema.

### dotenv

A biblioteca dotenv é um módulo Javascript que carrega variáveis de ambientes armazenadas em um arquivo `.env` para o `process.env`. Essa biblioteca elimina a necessidade de configurar variáveis de ambiente no Sistema Operacional.


###### Fonte:
- [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/441a7487-def4-4f4d-9b12-14b0a50145ba)
- [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/fd0a23c8-a146-4c59-942a-2b9ab77b8f5b)
- [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4684c963-8015-41ad-a901-eb37076d9ff5/lesson/593909fe-a50a-4899-98db-8f23dbf8517a)
- [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/27d3ea73-4725-48c0-b38c-8acc4dc4d40a/lesson/ecb6dae3-cad0-4a7c-bb6f-dfea7d44a693)
- ###### [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/d07db7a0-0f11-495a-a5db-7496fb182746)
