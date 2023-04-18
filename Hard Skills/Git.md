## O que é Git?

Git é o **sistema de controle de versão** open source mais usado no mundo atualmente! Ele é usado para controlar o **histórico de alterações** de arquivos e principalmente de [projetos de desenvolvimento de software](https://blog.betrybe.com/tecnologia/aprenda-tudo-sobre-programacao/). Ele permite mais flexibilidade no fluxo de trabalho, segurança e desempenho. 

### O que é um sistema de controle de versão?

Um sistema de controle de versão é uma ferramenta que ajuda equipes a **gerenciar alterações em** [**código fonte**](https://blog.betrybe.com/tecnologia/codigo-fonte/) ao longo do tempo. Além disso, ele ajuda os [times](https://blog.betrybe.com/carreira/squad/) a trabalharem de forma mais rápida e inteligente. Isso acontece pois a ferramenta de controle de versão mantém um registro de todas as versões do código, ou seja, de todas as modificações. Isso ajuda a [pessoa que desenvolve](https://blog.betrybe.com/carreira/o-que-faz-um-programador/) a conseguir voltar para qualquer versão anterior ou compará-las, ajudando a descobrir e corrigir erros muito mais rápido.

## Como surgiu o sistema de controle de versão Git? História!

O Git foi desenvolvido pelo **criador do kernel do** [**Linux**](https://blog.betrybe.com/tecnologia/comandos-linux/)**, Linus Torvalds,** em 2005. Tudo começou com o rompimento de relações entre a comunidade que desenvolvia o kernel do Linux e a BitKeeper, que é um sistema de controle de versão que foi usado dentro do projeto do kernel. Com esse rompimento, a ferramenta do BitKeeper passou a ser paga.

Com tudo isso, Linus Torvalds decidiu construir um sistema de controle de versão que tivesse a **melhor performance** e usou a experiência que teve com a BitKeeper para construir o Git, que se tornou o sistema de controle de versão **mais utilizado no mundo**. Linus tinha como principais metas para o seu projeto:

-   velocidade;
-   suporte para desenvolvimento não-linear;
-   distribuído;
-   lidar com projetos grandes de forma eficiente.

Desde sua criação em 2005, o Git conseguiu amadurecer, tornar-se simples de usar e ainda manter esses pontos iniciais.

## Onde o Git pode ser usado?

O Git pode ser usado em **todo e qualquer** **projeto que tenha arquivos** de diferentes tipos, podendo ser código, texto, imagens, vídeos, áudios, entre outros. O objetivo principal é permitir o controle de histórico e versão desses projetos, melhorar o trabalho em time e o fluxo de trabalho, proporcionar a segurança dos seus arquivos e outras tantas vantagens faladas nesse post. 

## Quais as vantagens e desvantagens de usar Git?

### Vantagens: porque usar Git?

Você já deve ter percebido algumas vantagens em usar Git até aqui, mas vamos falar mais sobre elas:

#### **Desempenho**

O Git pode ser considerado um dos melhores softwares de controle de versão quanto a performance. Todas as operações são pensadas para trazer praticidade e desempenho. Como ele também é distribuído, isso traz ainda mais [agilidade para o desenvolvimento](https://blog.betrybe.com/carreira/gestao-do-tempo-dicas-essencias/), já que você consegue fazer alterações no seu projeto sem uma conexão à [internet](https://blog.betrybe.com/tecnologia/como-melhorar-a-internet/).

#### **Flexibilidade**

Uma das grandes vantagens do Git é você conseguir adaptar formatos de trabalho não lineares e ainda conseguir rastrear cada uma dessas ramificações. Independente se o seu projeto é grande ou pequeno, você consegue adaptá-lo para o seu fluxo.

#### **Segurança**

Uma das prioridades é a integridade do código fonte do seu projeto. Todas as informações, conteúdos de código, versões, commits, tudo é protegido com SHA1, que é um [algoritmo](https://blog.betrybe.com/tecnologia/algoritmo/) seguro de hash de criptografia. Isso proporciona mais [segurança](https://blog.betrybe.com/tecnologia/seguranca-da-informacao/) contra alterações acidentais ou [maliciosas](https://blog.betrybe.com/carreira/hacker/) e também permite que o histórico de alterações seja totalmente rastreável.

### Desvantagens

Como toda e qualquer decisão, precisamos olhar as desvantagens, e na escolha de um controle de versão não seria diferente. As principais desvantagens no uso do Git são:

#### **Maior complexidade**

O Git pode ser **mais complexo** de se entender no início, por conta da enorme possibilidade de combinações e de ramificações do seu código. Todo esse entendimento pode ficar mais complicado de entender. 

Além disso, exige que as [pessoas desenvolvedoras](https://blog.betrybe.com/carreira/desenvolvedor-de-software/) tenham um **conhecimento maior** sobre o seu uso. Mas, depois dessa [curva de aprendizado](https://blog.betrybe.com/carreira/passos-fundamentais-para-aprender-a-programar/), agiliza o desenvolvimento e a entrega do time. Isso faz com que necessite de uma **maior preparação** tanto da equipe quanto dos processos do time.

![Imagem que representa os branchs dentro do Git](https://lh4.googleusercontent.com/hDZ7C2NQmOEeApDyPXFfjEfJyyIcmI8AfA8m-8loF8I2QKNrn4_Mw_IQKzoyj7O6SoKi2h6vTrKwZV5GL2uTJKSx_Kz8hSEpLAuhp7R_kpUYlW4H0oQbM34zo3fOZDtFU2PPtPr3)

## O que são repositórios, commits e branches?

### Repositórios

Um repositório, ou repo, é um **diretório onde você** **armazena os arquivos** do seu projeto, que podem ser códigos, imagens, áudios, vídeos ou qualquer coisa relacionada a esse projeto. Ele pode ficar armazenado no seu computador, um **repositório local**, ou também ser armazenado em alguns serviços como [GitHub](https://github.com/), [BitBucket](https://bitbucket.org/) ou [GitLab](https://about.gitlab.com/), ou seja, um **repositório remoto**.

### Branches

Branch significa “ramo”, ou seja, uma **ramificação** do seu código. Imagine a seguinte situação: você tem o seu código que já está funcionando em produção e precisa desenvolver uma nova funcionalidade (“feature”). Mas você não pode mexer direto no código em produção. 

Para isso, você cria **uma ramificação do seu código, uma branch**, em que você pega o estado atual daquele código e cria um novo ambiente para desenvolver a nova feature a partir dali. 

Dessa forma, você não altera a versão principal do seu código, consegue desenvolver sua funcionalidade com segurança, e quando esse código estiver funcionando, você poderá colocar ele na principal (ou fazer o merge, que falaremos mais adiante nesse post).

![Esquema de implementação de uma feature na branch main](https://lh4.googleusercontent.com/5Cp1saujw_U6VX2b_KPpx7AlRC_wBtY5s3WPQmiELGgAsWPu-M5cfhQrqQmWc4oCCkHVwsbSAc2vWALxPVAG31wuUn5Z6SYCYnUH9uC2rF51l5LiefKfZAjvGM3MKEWyGJBNAN9K)

### Commits

Um commit é um **conjunto de alterações** que você fez em um projeto. Ele marca uma versão do seu código. Um commit guarda as alterações feitas nos arquivos, quem fez essas alterações e uma **mensagem** que resume essa alteração. 

Além disso, cada commit tem um hash único SHA1 que pode ser usado para acompanhar todas as alterações feitas no passado e inclusive pode ser usado para voltar em alguma alteração específica ou em algum ponto no tempo específico do seu código.

## Porque usar vários branches?

A grande vantagem na possibilidade de ter várias _branches_ é conseguir **ter mais de uma “área de trabalho”** sem alterar a _branch_principal. Vamos trazer um exemplo: imagine que você tenha um sistema que está funcionando e já está em produção. Agora você vai precisar implementar uma nova feature para ele. Você não pode alterar direto o código que está lá em produção, por isso, você cria uma nova _branch_ (a feature por exemplo), e você vai partir do código que estava funcionando em produção.

Mas enquanto você estava implementando essa nova feature (lá pelo commit 4 da imagem abaixo), apareceu um [bug no sistema](https://blog.betrybe.com/tecnologia/o-que-e-bug/) e você tem que parar o que está fazendo e consertá-lo. Para isso, você novamente cria uma nova branch a partir do que está em produção para corrigir o problema. Depois de pronto, você consegue voltar para a sua feature sem problemas. 

Essa é uma das maiores vantagens de você trabalhar em _branches_. Poder focar em pequenas implementações, sem afetar o que já está funcionando, e poder **trocar esses contextos**, voltar e criando essas ramificações, enquanto a sua _branch main_ continua funcionando. 

![Fluxo de implementação de feature e arrumar bugs na branch main com commits](https://lh6.googleusercontent.com/nuI1gbRQMPP43osLUkpoUVjEl7yiPY2P5jRbE6adbJ1S_8i5MPfoHuXI3mXKrefqIKKe4t0EWHl66vkp_ilSPiZROrrt_ubDIBMOke7ufaYgD0EhialTgYja8zwK_JvpHnXTDR4K)

## Como funciona um repositório local e quais suas zonas virtuais?

Quando estamos trabalhando em um repositório, temos três diferentes tipos de zonas virtuais:

-   Working directory; 
-   Staging area;
-   Commit area.

O **_Working Directory_**, também conhecido como _Working Tree_, é a área em que você está trabalhando. **Onde estão todos os seus arquivos**, onde você criará novos arquivos, deletará os velhos ou alterará os que já existem. Também é onde estão os arquivos _untracked._

Após alterações nos arquivos, o próximo passo é adicionar essas alterações na **área de _staging_**. Também conhecida como _index,_ é quando o Git passa a salvar aquele estado dos seus arquivos. É como se fosse uma **prévia do seu commit**. O interessante é que se você fizer uma alteração em um arquivo, adicionar ele na _staging area_ e depois fizer uma nova alteração nesse mesmo arquivo, essa alteração estará no _working directory_ novamente. E a alteração anterior continuará na _staging area_.

O próximo passo é pegar todas as alterações de _staging_ e fazer um _commit_ com elas. Quando você faz isso, esse commit vai para a _commit area_ ou também conhecida como _local repository_. Aqui fica tudo do seu repositório. É por isso que você consegue trabalhar de maneira offline, podendo executar suas tarefas e fazer commits sem precisar se conectar a nenhum repositório remoto.  

![Esquema de diretórios do Git](https://lh3.googleusercontent.com/TdWr_adbpR8lw_VAH-d6ll0_Rdt2vZivX9DWcbQp0vqZnJDxqBm14zOb98TT6mm0M4eVztPrLzIhYfwLTM6m1BnuguKmoIDHHXCgBqOZN1dPLcAhaeRRwNAsocKYddOxJyva-6iS)

## Quais as diferenças entre Git e GitHub?

Basicamente, o [**Github**](https://blog.betrybe.com/tecnologia/git-e-github/) é uma **plataforma** usada para gerenciar, hospedar códigos e arquivos, além de facilitar a criação de ambientes de colaboração entre pessoas desenvolvedoras. O GitHub usa como sistema de controle de versão o Git. Ou seja, o GitHub facilita e auxilia a usar o Git no dia a dia. 

O Git é um **sistema de controle de versão local**, ele ajuda quem desenvolve a manter o histórico das versões ao longo do tempo, e traz vantagens para o desenvolvimento individual. Já o GitHub usa os recursos dele para serem usados de forma colaborativa, auxiliando o gerenciamento desses projetos e também dos times, além de também ser uma rede social e contribuir para o universo open source.


###### Fonte [Blog Trybe](https://blog.betrybe.com/git/)