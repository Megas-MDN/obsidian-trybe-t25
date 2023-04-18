[[Docker]]

## Containers vs. Máquinas Virtuais

É comum que as pessoas relacionem os containers com **máquinas virtuais** leves, pois, na teoria, parecem ter as mesmas funcionalidades.

Entretanto, as **máquinas virtuais possuem uma característica bem distinta**: elas precisam ter a instalação completa de um **sistema operacional convidado** por cima do sistema operacional já existente na máquina hospedeira! Veja a figura abaixo para comparação:

![[Pasted image 20230111151353.png]]

**Mas o que isso significa na prática? 🤔** Isso significa que existe um espaço em disco perdido, pois precisamos instalar um novo Sistema Operacional (SO) para cada máquina virtual, além da instalação do _Hypervisor_, que é um programa responsável pela tradução dos comandos entre o SO convidado e o SO hospedeiro.

> _Isso significa que máquinas virtuais serão sempre uma escolha ruim?_ 🤔
> 
> Não! Existem aplicações muito interessantes onde aplicar a arquitetura de máquinas virtuais é a melhor opção. Quer ler mais sobre isso? Confira a seção de **Recursos adicionais**.

## Como o Docker consegue fazer isso?

Parece muito bom pra ser verdade que uma ferramenta pode fornecer tantas funcionalidades, proteções, isolamentos, tudo ao mesmo tempo! _Mas qual o segredo da implementação do Docker?_ 🤔

O segredo está no jeito que o **_kernel_ do Linux** foi implementado! Existem funções especiais, chamadas de _syscalls_, que permitem a possibilidade de se criar um processo no Linux e “mentir” pra ele! Podemos criar um novo processo e:

-   Isolá-lo de se comunicar usando a rede:
    
    -   A máquina pode ter comunicação com a Internet, mas o processo não consegue!
-   Isolá-lo de se comunicar com outros processos do sistema:
    
    -   Para ele, o processo parece estar **sozinho** e com máquina inteira só pra ele!
-   Limitar seu uso de recursos computacionais, por exemplo:
    
    -   A máquina pode ter 4 _cores_ de processador, mas o processo pode ver apenas 1 _core_;
    -   A máquina pode ter 16 GB de memória RAM, mas o processo pode ver apenas 2 GB;
    -   A máquina pode ter 500 GB de espaço em disco, mas o processo pode ver o disco com apenas 100MB.

➡️ O Docker garante um isolamento tão grande entre os processos que ele cria, que a gente dá um _nome especial_ para estes processos isolados: `containers`! Legal isso, não? 🐋

## Imagens vs. Containers

Você já deve ter percebido que citamos várias vezes como podemos utilizar o Docker para trabalhar com `imagens` e `containers`.

**Mas quais são as diferenças entre esses conceitos?**:

-   **A `imagem` é a nossa aplicação “empacotada” com todas as dependências necessárias já instaladas dentro dela.**
    
    -   Imagine a imagem Docker como um arquivo `zip`, que contém o código-fonte e tudo o que é necessário para a execução correta do projeto.
    -   Não é possível entrar no “terminal” de uma imagem, já que ela não está em execução.
    -   O Docker possui um arquivo especial chamado **Dockerfile**, que nos ajuda a criar imagens. _Falaremos mais sobre isso adiante!_
-   **O `container` é um processo que representa a execução de uma `imagem` já construída anteriormente.**
    
    -   Imagine o container Docker como um programa que você executa após “descompactá-lo” de um arquivo zipado, que já veio com todas as dependências necessárias.
    -   Apesar de ser um processo isolado, é possível entrar no terminal **dentro do container**!
    -   É possível parar e continuar a execução de um container sem precisar recriá-lo.

**Agora vamos para a prática!** 💪

## Preciso instalar tudo o que é necessário dentro da imagem?

Sim, porém lembre-se que não precisamos **reinventar a roda**. Vamos comparar os dois cenários abaixo:

🔺**Problema**: você precisa executar um código JavaScript usando Node. O que você faz?

1️⃣ **Cenário 1**: Cria uma receita que, partindo de uma **imagem Docker vazia**:

-   Faz a instalação de um sistema operacional Linux
-   Faz a instalação das dependências para poder instalar o Node
-   Faz a instalação do Node
-   Copia seu código-fonte para dentro da imagem
-   **Feito!**

2️⃣ **Cenário 2**: Cria uma receita que, partindo de uma **imagem Docker com Linux e Node já instalados**:

-   Copia seu código-fonte para dentro da imagem
-   **Feito!**

_Percebeu a diferença?_

Muitas pessoas já usam o Docker para executar aplicações em Node, por exemplo. Se já existe uma “receita” de como construir uma Imagem Docker com Linux e Node já instalados, podemos usar essa imagem como **base** para criarmos uma **nova imagem**!

_Agora, como vamos obter essas imagens já construídas? Será que existe algum tipo local de compartilhamento ou catálogo de imagens Docker prontas?_ 🤔 Sim, já existe e se chama **Registry**.

## Registry

Registry é um local remoto onde podemos enviar e baixar imagens Docker. Podemos utilizá-lo como um **catálogo** de imagens Docker, onde é possível criar novas imagens usando outras imagens do catálogo como base. Com isso, temos uma biblioteca completa de aplicações e ferramentas já prontas para uso em uma imagem Docker! 🌟

Normalmente, este serviço é oferecido em duas categorias:

![[Pasted image 20230111154110.png]]

▶️ Veja alguns exemplos de _registries_ públicos:

-   [Docker Hub](https://hub.docker.com/): a própria **Docker Inc.** oferece um serviço de registry público;
-   [Quay Container Registry](https://quay.io/): a empresa Red Hat também oferece um serviço semelhante.

As grandes empresas de serviços em nuvem, como Amazon, Google Cloud Platform e Microsoft Azure, possuem seus próprios serviços de Registry! Entretanto, são **serviços pagos**. Acesse os links abaixo caso queira conhecer melhor cada um deles:

-   [Amazon Elastic Container Registry](https://aws.amazon.com/pt/ecr/) (ECR), oferecida pela Amazon.
-   [Google Container Registry](https://cloud.google.com/container-registry) (GCR), oferecido pelo Google Cloud Platform.
-   [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) (ACR), oferecido pela Microsoft Azure.

Até agora já aprendemos vários conceitos novos, mas não tivemos mão na massa! Vamos conhecer nossos primeiros comandos do Docker pra ficar mais interessante?

Bora continuar mergulhando no incrível mundo de Docker! 🐋

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/a852c0dd-0602-4357-88e8-707352e97927/lesson/0056b951-211d-4d9f-8913-8cb9955815d5)
