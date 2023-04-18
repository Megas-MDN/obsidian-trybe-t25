[[Docker]]

## Distribuição de um software autossuficiente (`Standalone`)

Considere, por exemplo, a distribuição de um software para um Sistema Operacional. Para que a distribuição do _software_ seja popular, o ideal é que ela possua o mínimo de etapas para sua utilização, ou seja, **quanto mais autossuficiente for seu instalador, mais prático e mais fácil vai ser para executar seu software.**

Quando temos uma aplicação que requer muitos recursos (bibliotecas adicionais, banco de dados ou até mesmo outros softwares), temos que garantir que essas dependências serão atendidas antes que a pessoa usuária possa executar nossa aplicação.

Além disso, nem sempre mandar somente o código fonte vai resolver o problema: precisamos preparar o ambiente para que aquele código funcione corretamente. É daí que vem a ideia de **empacotamento**!

A ideia de um pacote é que **ele possui informações e itens fundamentais para que sua aplicação funcione corretamente***. No Sistema Operacional(OS), um pacote precisa de um **desempacotador** que também é responsável por organizar e disponibilizar aquele conjunto de itens para que possamos executar aquela aplicação.

> * No caso do Linux (e sistemas _Unix_ em geral), pacotes podem possuir arquivos executáveis, mídias, outras bibliotecas e informações sobre bibliotecas adicionais que devem ser instaladas antes, caso esse software precise.

No **Docker**, trabalhamos com a ideia de `Containers` _(contêineres em português)_, que na prática funcionam como se fossem pacotes, porém numa dinâmica um pouco diferente, já que neles temos não só os arquivos fundamentais da aplicação (scripts, executáveis, mídias, etc), como também **todo o sistema operacional e suas bibliotecas*, além de instruções de como preparar e rodar sua aplicação naquele ambiente.**

> Um modelo que lembra _- mas não é o mesmo -_ de uma Máquina Virtual _(VM)_. _Falaremos mais adiante das diferenças entre os dois._

Dessa forma, com o Docker conseguimos **preparar** (como em um processo de desempacotamento e instalação) **e rodar esses `containers` na nossa máquina.** Isso reduz - e muito, principalmente em um ambiente de desenvolvimento - a quantidade de etapas que precisamos seguir para rodar nossa aplicação de maneira ideal.

Esse recurso também permite que consigamos rodar **várias instâncias _(`containers`)_ de aplicações ao mesmo tempo**. Isso é especialmente importante quando falamos em arquiteturas baseadas em [[Docker - 17 Conteúdo Extra - Microsserviços]].


## Capacidade de gestão e processamento de dados de um software na nuvem

Se estamos trabalhando com um **sistema na nuvem**, ou seja, um software que não é instalado no seu computador, mas que podemos ter acesso via navegador de internet, muito provavelmente estamos falando da relação entre **uma quantidade expressiva de clientes** (pessoas usuárias) **consumindo um servidor** (computador que hospeda sua aplicação) **ao mesmo tempo**, ainda que por um momento específico no dia.

Nesse contexto, voltemos a atenção para o servidor, já que ele é o responsável por rodar sua aplicação e processar essa demanda de requisições e manipulação de dados.

Se nossa aplicação tiver muito tráfego, ou seja, for um software muito utilizado, talvez esse servidor não dê conta da quantidade de requisições e, portanto, exigirá mais recursos para conseguir continuar trabalhando.

Esse problema ocorre muito com quem possui seus próprios servidores físicos. Nesses casos, uma primeira opção pode ser trabalhar no melhoramento do hardware daquele servidor: colocar mais memória ou processamento, por exemplo, aumentando fisicamente a escala de processamento daquela unidade - o que chamamos de **escalonamento vertical**.

No princípio esse processo pode parecer vantajoso, mas a medida que sua aplicação consome cada vez mais recursos, **essa opção se torna a mais cara de todas**. É aí que empresas optam por serviços na nuvem, já que é possível consumir recursos por demanda, o que reduz muito o custo pra manter o software, já que você só paga o que consome.

Nesses serviços, podemos automatizar a alocação de mais processos Docker referentes à aplicação, em mais de um computador - o que chamamos de **escala horizontal**.

_Lembra que falamos que o docker é capaz de rodar mais de uma instância ao mesmo tempo?_ Isso torna ele o candidato ideal para utilização **em escala horizontal**!

Isso é possível, já que podemos configurar esses serviços na nuvem, para que eles estejam preparados para lidar com picos de demanda (em qualquer tempo), ou até mesmo para garantir a disponibilidade do serviço (_uptime_), prevenindo quedas do mesmo, dado que podem haver vários processos da nossa aplicação ativos ao mesmo tempo!

Dessa forma, aumentamos o número de máquinas com processamento limitado (que vão processar nossa aplicação ao mesmo tempo) em vez de aumentar a capacidade de apenas uma máquina.

## Escalabilidade horizontal x vertical

Antigamente (e até hoje em alguns lugares), para conseguirmos lidar com uma demanda muito grande de processamento, era praticado o chamado **Escalonamento Vertical**!

![Diagrama de comparação entre escalonamento vertical ou horizontal](https://content-assets.betrybe.com/prod/Diagrama%20de%20compara%C3%A7%C3%A3o%20entre%20escalonamento%20vertical%20ou%20horizontal.png)
`Diagrama de comparação entre escalonamento vertical ou horizontal`

O processo consiste, basicamente, em aumentar os recursos de _hardware_ do computador, _(processador, Memória RAM, etc)_.

> Isso é algo que faz sentido somente até o ponto em que cada peça de _hardware_ começa a custar mais do que adquirir um computador novo!

Ou seja, **quanto mais processamento, mais caro fica de trabalhar nessa escala**, algo que se prova uma prática inviável em larga escala!

A **Escala Horizontal**, por outro lado, é feita criando aquilo que chamamos de `Cluster`, que na computação, é a aglomeração/combinação de vários computadores trabalhando com uma mesma finalidade.

Nesse caso, **quando há mais demanda por processamento, mais computadores são alocados naquele `Cluster`** para lidar com essa demanda. Da mesma forma, **quando há menos demanda, são retirados computadores do `Cluster`**.

Esse processo pode não parecer, mas quando trabalhamos com _softwares_ que são consumidos por dezenas de milhares de pessoas, **é a saída mais barata**,já que uma série de computadores mais baratos, **podem trabalhar juntos como um supercomputador**.

A **escala horizontal** também é a candidata perfeita pra quando estamos trabalhando em **ambientes complexos/ de alta dinâmica**.

# Diferenças entre um processo Docker e uma VM tradicional

Comentamos anteriormente que o _Docker_ “trabalha em um modelo que lembra _- mas não é o mesmo -_ de uma Máquina Virtual _(VM)_“. Isso porque temos uma característica específica encontrada numa instancia de _Docker_: **ela funciona como um processo, que compartilha da mesma estrutura de baixo nível do sistema operacional!**

Isso garante que **a aplicação “convidada” consuma somente os recursos de hardware necessários na máquina “hospedeira”**, e que, **entre a ponta do software (sua aplicação) e os recursos base necessários para que ela funcione*, haja o menor intermédio possível**. Tal qual um processo normal do sistema.

> * Entende-se aqui como recursos base de um Sistema Operacional Hospedeiro: Seu núcleo (_Kernel_), suas bibliotecas e seus arquivos fundamentais.

Em uma Máquina Virtual_, por outro lado, existe um **intermediário complexo**, uma espécie de [emulador](https://pt.wikipedia.org/wiki/Emulador)), que faz a tradução dos recursos do _hardware_ e sistema operacional hospedeiro, para esses mesmos recursos - só que _*virtualizados__ - no lado do convidado.

> * Exemplos populares de _VMs_ incluem o `Virtual Box` e o `VMware`. São utilizados por quem precisa utilizar sistemas operacionais completos dentro de um sistema base (como se fossem aplicativos, _numa espécie de “inception”_).
> 
> O processo de instalação de uma máquina virtual é praticamente idêntico ao de instalação numa máquina real, porém com opções como a limitação e definição de recursos utilizados por aquele S.O.

Assim, o computador que está hospedando a máquina virtual tem que alocar uma quantidade definida de recursos (que não são poucos) para aquele sistema convidado. Isso consome muito mais processamento do que utilizar um processo _Docker_ que trabalha nativamente, _além de não ser nada prático!_

A imagem a seguir ajuda a ilustrar a diferença entre os dois:

![Diagrama de comparação entre um servidor com VMs e um servidor utilizando Docker](https://content-assets.betrybe.com/prod/Diagrama%20de%20compara%C3%A7%C3%A3o%20entre%20um%20servidor%20com%20VMs%20e%20um%20servidor%20utilizando%20Docker.png)

Diagrama de comparação entre um servidor com VMs e um servidor utilizando Docker

> _Um detalhe interessante é que um processo Docker pode rodar dentro de uma VM!_

Dessa forma, é possível entender que, quando precisamos de uma solução rápida pra rodar nossos aplicativos, o _Docker_ ainda é a melhor alternativa, já que em comparação a um servidor rodando _VMs_, o custo de processamento, memória e tempo de inicialização é bem menor!

## Gerenciando Redes no Docker

Vimos como “expor” as portas de nossos _containers_ para acessá-los de fora, utilizando o parâmetro `EXPOSE` em nosso `Dockerfile`, e também como fazer a atribuição (_bind_) com as portas de nossa máquina _host_ utilizando o parâmetro `-p` no `docker container run`. Chamamos de mapeamento de portas esses recursos que vinculam ou tornam visíveis portas do _container_ para a nossa máquina _localhost_.

Já o _Docker network_, é uma espécie de rede virtualizada que permite que você conecte _containers_ a uma determinada rede ou quantas redes _Docker_ desejar, de forma que esses _containers_ possam compartilhar informações através dessa rede.

Por padrão, o _Docker_ possui 3 redes que são criadas junto com ele: `bridge`, `none` e `host`. Cada uma delas tem características específicas quanto a conectividade para seus _containers_. Podemos consultá-las executando:

```bash
docker network ls
```

Vamos entender o que é cada uma!

## Bridge

Ao ser iniciado, todo _container_ é associado a uma rede e, caso uma rede não seja especificada explicitamente por nós, ele será associado a rede `Bridge`.

Todos os _containers_ associados a essa rede poderão se comunicar via protocolo [TCP/IP](https://pt.wikipedia.org/wiki/TCP/IP) e, se soubermos o IP do container que queremos conectar, podemos enviar tráfego a ele. Porém, os IPs de um _container_ são gerados automaticamente, por isso não é muito útil fazermos a conexão dessa forma, pois sempre que o _container_ for reiniciado, o IP poderá mudar.

Uma maneira de fazermos a descoberta do IP automaticamente pelo nome, é utilizando a opção `--link`. No entanto, a própria documentação do _Docker_ desencoraja seu uso e alerta que essa flag (`--link`) pode ser removida eventualmente.

Para fins didáticos, vamos ver como isso funciona, utilizando uma imagem `busybox`, mas mais adiante veremos a melhor alternativa para fazer isso.

Digite no terminal:


```bash
docker container run -ti --name container1 busybox

docker container run -ti --link container1 --name container2 busybox
```

Agora, o `container2` poderá se conectar no `container1`. Para fazermos um teste simples, podemos fazer um `ping` no `container1`, dentro do `container2`, apenas digitando no terminal interativo do `container2`:

```bash
ping container1
```

É bom ressaltar que a opção –link **não** é necessária para permitir que os serviços se comuniquem, pois, por padrão, qualquer serviço pode alcançar qualquer outro serviço a partir de seu `IP`. Os links apenas permitem definir apelidos extras pelos quais um serviço pode ser acessado de outro serviço.

> ⚠️ Dica: Perceba que nos exemplos utilizamos uma imagem chamada `busybox`, ela é uma _suite_ que possui vários utilitários Unix, dessa forma é muito útil quando queremos explorar comandos como o _ping_ para testes.

## Host

Ao associarmos um _container_ a essa rede, ela passa a compartilhar toda _stack_ de rede do _host_, ou seja, da máquina que roda o ambiente _Docker_. O uso desta rede é recomendada apenas para alguns serviços específicos, normalmente de infra, em que o _container_ precisa desse compartilhamento. Caso contrário, a recomendação é evitá-la.

## None

Essa é uma rede que não possui nenhum _driver_ associado. Dessa maneira, ao atribuir um _container_ a ela, o mesmo ficará isolado. Ela é útil quando temos _containers_ que utilizam arquivos para a execução de comandos ou para se comunicar, por exemplo, um _container_ de backup ou que rode apenas um script localmente.

## Criando Nossa Rede

A forma mais recomendada de comunicarmos nossos containers é criando nossa própria rede. Através dela conseguimos, por exemplo, referenciar um _container_ a partir de outro, utilizando seu nome. Vamos ver um vídeo que exemplifica isso:

Ou seja, conseguimos criar nossas próprias redes utilizando:


```bash
docker network create -d bridge minha-rede
```

Para vincularmos nosso _container_ à rede criada durante sua execução, basta utilizarmos o parâmetro `--network`:


```bash
docker container run \
    -itd \
    --network minha-rede \
     --name meu-container \
     busybox
```

Agora, note a rede `minha-rede` e o driver `bridge`:

```bash
docker network ls
```

Para conectarmos um _container_ já criado, basta utilizarmos o parâmetro `connect`:

```bash
docker network connect minha-rede meu-container
```

E para desconectá-lo, basta utilizar o parâmetro `disconnect`:

```bash
docker network disconnect minha-rede meu-container
```

Importante lembrarmos que _drivers_ e _networks_ são objetos diferentes. Uma rede é associada a um ou nenhum _driver_, as redes padrões que mencionamos acima, possuem o mesmo nome de seu driver, porém não confunda. Por exemplo, a rede _bridge_ possui o driver _bridge_ e, quando ao criarmos nossa própria rede, também utilizamos esse driver, porém não há relação com a rede padrão de nome _bridge_, no caso não estaremos utilizando ela.

Da mesma forma acontece com a rede _host_, já a rede _none_ não possui um driver e, por isso, ao associarmos um _container_ a ela, ele fica isolado.

## Gerenciando Volumes no Docker

O que sabemos até o momento é que se removermos um _container_, todos os dados que manipulamos sobre ele também serão removidos. Isso acontece porque estamos escrevendo na camada criada pelo _container_ e que permite leitura e escrita.

Mas existe uma a possibilidade de persistir os dados em um _container_, que é a utilização de **volumes**!

Utilizar um volume significa mapear uma pasta do nosso Sistema Hospedeiro (`Docker Host`), para o Sistema Convidado (o _container_).

Assim, ela é vinculada ao _container_ e mesmo que esse _container_ seja removido, essa pasta permanecerá. Isso faz com que os dados não sejam perdidos.

Utilizando um exemplo com o _Apache_, pense na seguinte situação: Queremos desenvolver nossa página `HTML` de forma que ela rode dentro do servidor `http Apache`, que **não** está instalado em nossa máquina.

Assim, a medida que formos desenvolvendo nossa página `HTML`, precisamos que o nosso ambiente de desenvolvimento permaneça no _container_.

Para isso, a primeira coisa que vamos fazer é criar a seguinte página `HTML`:

```html
<!DOCTYPE html>
   <html>
      <head>
      <title>Docker é muito bom!</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   </head>
   <body>
      <h1>Minha primeira página rodando em Docker.</h1>
      <p>Estou começando minha primeira página em HTML.</p>
   </body>
</html>
```

Salve o arquivo com o seguinte nome e extensão `primeiro-teste.html` em alguma pasta local de fácil acesso*.

> * Aqui usaremos o caminho `/home/trybe/meu-site`.

Agora vamos criar um _container_, que manterá um volume vinculado a essa nossa pasta local, para que qualquer alteração que fizermos em nosso `HTML` seja refletida no servidor `http` em nosso `container`.

Para isso, vamos usar no comando `run`, o parâmetro `-v` (de ‘volume’) da forma `-v <PASTA-LOCAL>:<PASTA-CONTAINER>`:

```bash
docker run -d --name site-trybe2 -p 8881:80 -v "/home/trybe/meu-site/:/usr/local/apache2/htdocs/" httpd:2.4
```

Vamos entender esse comando que acabamos de executar nos concentrando na flag `-v`.

Essa flag cria um volume e é seguida pelo endereço do diretório em nossa máquina `/home/trybe/meu-site/` acompanhada do endereço no diretório do servidor `/usr/local/apache2/htdocs/`*, ao qual será vinculado.

> * Esse diretório é específico para armazenar os arquivos que vão ser acessados no servidor `http Apache` e pode ser diferente, caso você opte por usar outro aplicativo.

Dessa forma qualquer modificação que realizarmos no arquivo HTML em nossa máquina local será refletido pelo container, no endereço da pasta do nosso servidor apache.

Agora acesse o site mantido pelo servidor Apache acessando o endereço `http://localhost:8881/primeiro-teste.html` no navegador e lá estará o aquivo HTML que você acabou de criar.

Vamos fazer um teste! Acesse novamente o arquivo `primeiro-teste.html` que a acabamos de criar e edite-o da seguinte forma:

```html
<!DOCTYPE html>
   <html>
      <head>
      <title>Docker é muito bom!</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   </head>
   <body>
      <h1>Minha primeira página rodando em Docker, que maravilha!</h1>
      <p>Estou começando minha primeira página em HTML e estou muito feliz! #VQV</p>
   </body>
</html>
```

Salve seu arquivo e recarregue sua página no browser.

O que podemos concluir com isso? Podemos criar um ambiente de desenvolvimento baseado apenas no uso de _containers_, o que facilita bastante o trabalho dos times de desenvolvimento, já que o volume pode ser compartilhado entre o time, e acessado via diferentes _containers_.

Da mesma forma, tendo um volume na sua máquina, você pode utilizar outros _containers_ sem perder seus arquivos!

Com o uso do volume, mesmo que o _container_ seja excluído, o volume será mantido. Isso quer dizer que tudo que colocarmos na pasta `/usr/local/apache2/htdocs/`, do _container_, ficará preservado na pasta `/home/trybe/meu-site` em nossa máquina.

Para verificarmos se essa afirmativa é verdadeira, faça o seguinte.

```bash
docker inspect site-trybe2 #que é o nome que demos ao nosso container
```

Teremos uma saída com muitas informações, mas o mais importante nesse momento é o “Mounts” que nos mostra através da propriedade `Source` onde está o volume desse container em nosso _Docker Host_.

```bash
"Mounts": [
   {
      "Type": "bind",
      "Source": "/home/trybe/meu-site",
      "Destination": "/usr/local/apache2/htdocs",
      "Mode": "",
      "RW": true,
      "Propagation": "rprivate"
   }
]
```

Bem, agora que confirmamos que temos um volume criado em nosso _Docker Host_ faremos a exclusão de nosso container e verificaremos se junto com o container nossa pasta `/home/trybe/meu-site` também será excluída.

Para isso, em posse do id do nosso container primeiro precisamos pará-lo com o comando:


```bash
docker stop site-trybe2
```

Agora que paramos o nosso container, vamos excluí-lo com o comando:


```bash
docker rm site-trybe2
```

Agora vamos verificar se a pasta onde salvamos nosso arquivo html permanece no mesmo lugar ou foi removida junto com o container:

```bash
cd /home/trybe/meu-site && \
ls -la
```

Isso deve retornar a lista de arquivos na pasta, algo como:

```bash
drwxrwxr-x 1 trybe trybe   38 set 22 17:37 .
drwxr-xr-x 1 trybe trybe 1236 set 22 17:33 ..
-rw-rw-r-- 1 trybe trybe  354 set 22 17:43 primeiro-teste.html
```

E voilà! Nosso arquivo `primeiro-teste.html` permanece intacto.

Agora, pra reforçar um pouco mais seus conhecimentos sobre **volumes**, veja o vídeo abaixo sobre quando e como utiliza-los:

Também é possível especificar os volumes da nossa imagem no nosso `Dockerfile`. Para isso, basta utilizarmos o comando `VOLUME` e então, caso não especifiquemos outros comportamentos para o _container_, será criado o ponto de montagem especificado.

A sintaxe em nosso `Dockerfile` é bem simples, basta especificarmos qual diretório será utilizado como _volume_ por nossa imagem:


```bash
VOLUME ["/data"]
```

> ⚠️ **Importante:** Toda vez que criarmos um container que mapeia um volume, **ele alocará espaço para esse volume no seu sistema**.

Por tanto, é sempre importante verificar seus volumes utilizando `docker volume ls` e remover aqueles que você não utiliza, seja com o comando `docker volume rm <VOLUME NAME>`, seja com `docker volume prune` **(⚠️ esse comando remove todos os volumes que não estão sendo utilizados por containers)**;

Também é possível remover volumes automaticamente ao remover _containers_, utilizando o comando `docker container rm -v <CONTAINER ID || NAMES>`, onde o `-v` indica para o docker, que o volume associado ao container também deve ser removido.

## Multi-stage

Uma **imagem Docker** é um arquivo imutável a partir do qual um ou mais _containers_ podem ser gerados e sua criação pode ocorrer por meio do processo de `build` de um arquivo chamado `Dockerfile`.

Já um **container Docker**, é como se fosse um **contexto (ativo ou inativo) de uma aplicação e é baseado em uma imagem**.

Para criarmos esses _containers_ para nossas aplicações, precisamos iniciar criando sua imagem, o que nos leva outra vez ao _Dockerfile_.

O `Dockerfile` é um arquivo de configuração usado pelo _Docker_ com a descrição passo a passo do que desejamos fazer. Ele contém as instruções necessárias, _uma espécie de “script”_, para que rodemos uma aplicação: Sistema Operacional utilizado, bibliotecas que devem ser instaladas, arquivos que devem ser inicializados, etc.

Nesse contexto do _Dockerfile_, uma estratégia para tirarmos melhor proveito dos recursos disponíveis, é a de utilizar “multi-stage” _(multi-estágios em português)_. Com essa estratégia, como o nome diz, podemos dividir nosso “pipeline” _(fluxo do processo)_ em vários estágios. Vamos a alguns exemplos.

Imagine que temos um aplicação _React_, para criar sua imagem, precisamos:

1.  Instalar suas dependências (`npm install`);
2.  Fazer o _build_ (`npm build`);
3.  Servir seu conteúdo estático.

Perceba que nos passos 1 e 2 precisaremos de uma imagem com _NodeJS_, que já possui, internamente, aplicações essenciais para instalação e execução de suas aplicações, como `npm`.

Já no terceiro item, precisamos de algum _server_ para servir esse conteúdo gerado, como o `Nginx`, e não precisaremos mais do _NodeJS_.

Vamos então criar esse _Dockerfile_!

Primeiro, criaremos a imagem para o _build_:

```Dockerfile
### Estágio 1 - O processo de build
FROM node:10 as build-stage
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json", "./"]
RUN npm install
COPY ["./src", "./src"]
COPY ["./public", "./public"]
RUN npm build
```

Perceba que só há uma coisa diferente aqui, o parâmetro `as` no `FROM`, ele irá “nomear” nosso “step” como uma imagem separada.

Ao final dessa execução, teremos o diretório `build`, com o conteúdo que iremos servir. Vamos ao próximo “stage” para entender como utilizá-lo:

```Dockerfile
### ... Estágio 1 - O processo de build
### Estágio 2 - O ambiente de produção
FROM nginx:1.12-alpine
COPY --from=build-stage /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Perceba que no comando `COPY`, utilizamos o parâmetro `--from` para indicar que queremos copiar esse diretório da imagem anterior, ou seja, do “estágio 1”. A partir daí, podemos servi-lo utilizando o _Nginx_.

**Lembre-se que ambos estágios, ficam contidos em um único Dockerfile**, separamos apenas para facilitar a compreensão, o arquivo completo ficaria assim:

```Dockerfile
### Estágio 1 - O processo de build
FROM node:10 as build-stage
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json", "./"]
RUN npm
COPY ["./src", "./src"]
COPY ["./public", "./public"]
RUN npm build

### Estágio 2 - O ambiente de produção
FROM nginx:1.12-alpine
COPY --from=build-stage /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Além de separar as partes do projeto e podermos utilizar uma imagem específica para cada estágio, perceba que no final temos uma imagem muito mais leve!

Isso porque além da imagem base ter somente o que é necessário para servir nosso conteúdo, as dependências e todo o código fonte não são levados para a imagem final, apenas o conteúdo já _buildado_.

Dessa forma, sempre que tivermos lidando com aplicações que possuem um processo de “build”, seja em uma aplicação _TypeScript_ ou _GoLang_, podemos utilizar desses recursos para criar imagens mais leves.

## Docker Hub

O [Docker Hub](https://hub.docker.com/) _(Registry)_*, pelo qual requisitamos as imagens que queremos.

> * O `Registry` é um sistema de armazenamento e entrega, no qual podemos ter um usuário com nossas próprias imagens. Algo que lembra muito o GitHub, já que podemos dar `pull` nessas imagens para uso posterior.

A criação de uma nova conta no _Docker Hub_, não pode ser feita via terminal ainda, portanto, você deve ir até a página oficial do _Docker Hub_, selecionar a seção [_sign up_](https://hub.docker.com/signup) e inserir seus dados. O _docker id_ é o correspondente ao seu _user_.

Assim como no _GitHub_, você pode ter repositórios públicos ou privados no _Docker Hub_, mas há uma limitação da quantidade de repositórios privados de acordo com o plano optado.

Ao rodarmos o comando `docker images`, iremos ver listadas todas as nossas imagens, mas nosso _Docker id_ (ou _user_) ainda não aparece em lugar nenhum.

![Rodando o docker images](https://content-assets.betrybe.com/prod/Rodando%20o%20docker%20images.gif)

Rodando o docker images

Para subir a imagem `minha-imagem` para sua conta, ela precisa estar _taggeada_ (campo `TAG`) de modo que seu _Docker id_ esteja no início de seu nome. Fazemos isso utilizando o comando _tag_, da seguinte maneira:

Copiar

```bash
1docker image tag <id-da-imagem> <user>/<image>:<tag>
```

![Renomeando a tag e rodando o docker images novamente](https://content-assets.betrybe.com/prod/Renomeando%20a%20tag%20e%20rodando%20o%20docker%20images%20novamente.gif)

Renomeando a tag e rodando o docker images novamente

O próximo passo para subir nossa imagem para o _Docker Hub_ é fazer _login_ na conta que criamos, utilizando o terminal. Para isso, basta digitar o comando:

Copiar

```bash
1docker login
```

Seu _Docker id_ e senha serão solicitados e, se tudo ocorrer conforme o esperado, uma mensagem de “_Login Succeeded_“ aparecerá no seu terminal.

A seguir, é só fazer o `push`, como quando mandamos algo pro _GitHub_ com o _git_. A sintaxe para isso é:

Copiar

```bash
1docker push <docker-id>/<image>:<tag>
```

Agora, você pode ir na sua página do _Docker Hub_ e ver sua imagem listada.

![Rodando o docker push e acessando a lista de repositórios no docker id do Docker Hub](https://content-assets.betrybe.com/prod/Rodando%20o%20docker%20push%20e%20acessando%20a%20lista%20de%20reposit%C3%B3rios%20no%20docker%20id%20do%20Docker%20Hub.gif)

Rodando o docker push e acessando a lista de repositórios no docker id do Docker Hub

De forma análoga, você também pode fazer o processo contrário e baixar uma imagem do seu repositório remoto para a sua máquina com o `docker pull`*.

> * Caso você já tenha a imagem que está querendo dar pull em sua máquina, nada acontecerá, portanto, se você gostaria de testar o comando, remova a imagem local com o comando `docker rmi -f <IMAGE-ID>`.

O comando para baixar a imagem é:

Copiar

```bash
1docker pull <docker-id>/<image>:<tag>
```

Agora, você pode listar todas as imagens com o `docker images ps` e ver que a imagem baixada já está junto com as demais em sua máquina.

Prontinho, agora além de usar imagens oficiais do _Docker Hub_, agora você também pode criar, enviar e baixar suas próprias imagens de lá!

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/4a9c025a-d8d9-4a87-92ac-0903a07407b6/lesson/50140c0d-e359-4f95-9847-96699ac52449)