[[Git]]


- [Instalando o Git](#Instalando%0do%0dGit)
- [3 ferramentas gráficas para usar em Git](#3%0dferramentas%0dgráficas%0dpara%0dusar%0dem%0dGit)
- [Download e instalação do Git](#Download%0de%0dinstalação%0ddo%0dGit)
- [Git config: como configurar o seu git?](#Git%0dconfig%0dcomo%0dconfigurar%0do%0dseu%0dgit?)
- [Conheça 17 comandos Git e saiba para que servem](#Conheça%0d17%0dcomandos%0dGit%0de%0dsaiba%0dpara%0dque%0dservem)
	1. [Git Init](#1.%0dGit%0dinit%0dcriando%0dseu%0drepositório%0dlocal!)
	2. [Git Add](#2.%0dGit%0dadd%0dadicionando%0dalterações%0dno%0drepositório!)
	3. [Git Commit](#3.%0dGit%0dcommit%0dconfirmando%0de%0dsalvando%0das%0dalterações%0dno%0drepositórios!)
	4. [Git Status](#4.%0dGit%0dStatus%0dverificando%0dse%0dhá%0dalterações%0dna%0dbranch)
	5. [Git Log](#5.%0dGit%0dlog%0dverifique%0dquais%0dcommits%0dforam%0dfeitos%0daté%0dagora)
	6. [Git Reset](#6.%0dGit%0dreset%0ddesfazendo%0das%0dalterações%0dde%0dum%0drepositório%0dpara%0dum%0dcommit%0danterior!)
	7. [Git Revert](#7.%0dGit%0drevert%0dDesfazendo%0dum%0dcommit%0dsem%0dexcluir%0dos%0ddados%0dexistentes!)
	8. [Git Diff](#8.%0dGit%0ddiff%0dverificando%0das%0ddiferenças%0dentre%0darquivos%0de%0drepositórios!)
	9. [Git Remote](#9.%0dGit%0dremote%0dligando%0dseu%0drepositório%0dlocal%0da%0dum%0drepositório%0dremoto!)
	10. [Git Push](#10.%0dGit%0dpush%0denviando%0das%0dalterações%0ddo%0drepositório%0dlocal%0dpara%0do%0drepositório%0dremoto!)
	11. [Git Branch](#11.%0dGit%0dbranch%0dlistando%0de%0ddeletando%0dbranches)
	12. [Git Checkout](#12.%0dGit%0dcheckout%0dcriando%0duma%0dnova%0dbranch%0de%0drestaurando%0darquivos!)
	13. [Git Marge](#13.%0dGit%0dmerge%0dmesclando%0das%0dalterações%0dem%0dsua%0dbranch%0dà%0dbranch%0dmaster)
	14. [Git Pull](#14.%0dGit%0dpull%0datualizando%0do%0drepositório%0dlocal%0dcom%0da%0dversão%0ddo%0drepositório%0dremoto!%0d)
	15. [Git Rebase](#15.%0dGit%0drebase%0dintegrando%0dtodas%0das%0dalterações%0dde%0dum%0dbranch%0dem%0doutro%0dbranch)
	16. [Git Stash](#16.%0dGit%0dstash%0dcriando%0dum%0dbackup%0ddas%0dalterações%0datuais%0ddo%0dseu%0dprojeto)
	17. [Git Clone](#17.%0dGit%0dclone%0dbaixando%0do%0dcódigo%0dfonte%0dde%0dum%0drepositório!)


## Instalando o Git

#### Instalação em Linux

Para instalar o Git, abra seu terminal e digite o comando:

```bash
sudo apt-get install git-all
```

Confira se a instalação foi efetiva digitando o comando `git --version`, que mostra a versão instalada do Git. O retorno do seu terminal deve ser parecido com este:

```bash
git version 2.38.0
```

#### Instalação em macOS

Para instalar o Git, abra seu terminal e digite o comando:

```bash
brew install git
```

Confira se a instalação foi efetiva digitando o comando `git --version`, que mostra a versão instalada do Git. O retorno do seu terminal deve ser parecido com este:

```bash
git version 2.38.0
```

Caso você não tenha o `brew` instalado, digite o comando abaixo no seu terminal e, após a instalação, execute novamente os comandos anteriores:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```



## 3 ferramentas gráficas para usar em Git

Existem algumas ferramentas gráficas que ajudam você a usar o Git. Há diferentes tipos de ferramentas no mercado, pagas e não pagas, mas vamos te mostrar 3 alternativas multiplataformas que tem planos gratuitos. 

### 1. [Git Kraken](https://www.gitkraken.com/)

Além de eficiente e visualmente agradável, o GitKraken faz com que as operações do Git sejam mais compreensíveis e simples de entender. 

### 2. [Git-cola](https://git-cola.github.io/downloads)

É uma ferramenta mais simples, porém bem poderosa para você executar seus comandos Git.

### 3. [SmartGit](https://www.syntevo.com/smartgit/download/)

Como o próprio nome já diz, é uma ferramenta inteligente e fácil de usar. Independentemente do sistema operacional que estiver usando, ele funciona da mesma maneira. 

## Download e instalação do Git

### Como instalar o Git no Windows

Para instalar o Git no Windows, basta baixar o instalador mais recente [aqui](https://gitforwindows.org/) e seguir os passos da instalação.

### Como instalar o Git no Linux

Se você tem um Debian/Ubuntu, pode baixar via **apt-get**, usando o comando: 

```
$ sudo apt-get install git
```

Agora, se você usa Fedora, pode usar o comando:

```
$ sudo dnf install git
```

Para verificar se está instalado, basta rodar:

```
$ git --version
```

### Como instalar o Git no MacOS

Existem várias formas de instalar o Git no seu Mac. Talvez ele já esteja até instalado, caso você já tiver instalado o Xcode ou suas ferramentas de linha de comando. Para saber se ele já está em sua máquina, abra o seu terminal e digite: 

```
$ git --version
```

Se não tiver instalado, aparecerá uma janela para instalar. Agora, se você quiser instalar a versão mais recente, pode ver todas as opções de como instalar [neste site](https://git-scm.com/download/mac). Você pode instalar via Homebrew, usando o comando: 

```
$ brew install git
```

Ou também usar o instalador mais recente, que você pode encontrar [aqui](https://sourceforge.net/projects/git-osx-installer/).

## Git config: como configurar o seu git?

Agora que você já tem ele instalado no seu computador, você pode **configurar ele com seus dados**. Abra um terminal e rode os seguintes comandos lembrando de alterar o que está em aspas pelo seu nome e seu e-mail:

```
$ git config --global user.name "Seu Nome"
$ git config --global user.email "exemplo@seuemail.com.br"
```

Essas configurações ficam em um arquivo chamado **.gitconfig**. No Linux e Mac, esse arquivo fica em **~/.gitconfig,** enquanto no [Windows](https://blog.betrybe.com/tecnologia/comandos-windows/) fica em **`c:\ Usuarios \ username \.gitconfig`**.

## Conheça 17 comandos Git e saiba para que servem!

### 1. Git init: criando seu repositório local!

O **git init** serve para que você crie o seu repositório localmente, no seu computador. Para isso, se você quiser criar um novo repositório, crie uma pasta (ou se você quiser iniciar um repositório em uma pasta que já existe, vá até ela) e digite o comando **git init** e pronto, seu repositório Git foi criado! 

![criando repositório local Git](https://lh6.googleusercontent.com/o1iGV5ZL81I7r5x77_BS11l0sQt2PRupgVUbKJpmk5iRZ1V2wg3eI734AiF_dUjBDZLZJkMzysbfvjill-7ZgkmK9KLl8nv_WPyuCdnXr2pz0NygNGjgIflL8P_QSNlHcVy1MzUw)


### 2. Git add: adicionando alterações no repositório!

Quando você cria ou modifica arquivos, você precisa adicionar eles para a área de _staging_, para isso você usa o comando **git add*** para adicionar todos os arquivos ou **`git add<nome-do-arquivo>`**. Dessa forma, os arquivos estarão prontos para serem _commitados_.

### 3. Git commit: confirmando e salvando as alterações no repositórios!

Após você usar o **git add**, os arquivos vão para a área de _commit_. Você pode empacotar todas essas alterações em um único _commit_ com uma mensagem que resume aquelas alterações. Para isso você usa o comando **git commit-m “Mensagem das alterações”**.

### 4. Git Status: verificando se há alterações na branch

O **git status** mostra o status do seu repositório naquele momento. Ele mostra o _working directory_, a _staging area_ com todos os arquivos em cada uma das áreas e qual o estado de cada um deles. Isso ajuda muito quando precisamos pensar em fazer um _commit_ ou até mesmo verificar quais foram todos os arquivos modificados.  

![Verficando se há alterações na branch do Git](https://lh5.googleusercontent.com/V-ag7LOd9Z1QPvRSr9dHH0fRtA0FM30Q4igMGXYz12hlGo9UZMhA-z_Ch42729wEF0Fq2N0EgsqGypKowyJcu7uarYi_T5-XTXbgJb8f_V-JOYKZ4OtnzdN7CFZdWJ6e3HllRtV1)

### 5. Git log: verifique quais commits foram feitos até agora

O **git log** ajuda a saber quais foram os commits feitos no seu repositório, quem fez, quando e também qual a mensagem de cada um. Além disso, esse comando te mostra a hash de cada um dos commits, o que pode ajudar a executar alguns outros comandos também. 

![Verficando os commits feitos até então](https://lh5.googleusercontent.com/Mk4y9TX3oDkaBy6TKBn91HZhefcALHWDq8h2uOTfFT78Tj6WbuV-C9bjH82ef-E-1B4xIPsKs3EvECbFbHskYZFANngfqyUabKwd6Gab4QNSR470aH6lPpd8gDxwYTPWHOTWUWhY)

### 6. Git reset: desfazendo as alterações de um repositório para um commit anterior!

O **git reset** é uma forma bem complexa para desfazer alterações. Teremos um post totalmente focado para falar dele, mas para falar sobre a forma mais usada dele, vamos dar dois exemplos. O primeiro deles é quando, localmente, precisamos voltar um commit. No exemplo da imagem abaixo, temos dois commits e queremos voltar para o primeiro. Para isso, usamos o comando:

```
git reset <hash do commit que queremos voltar>
```

Se você perceber, após rodar esse comando, o último commit sumiu e as alterações voltaram para o _working directory_. 

![Diretório após desfazer uma alteração para um commit anterior](https://lh5.googleusercontent.com/GON_64dRForX0sHEEPo3Ftwzs2y3vm1vSRfM4fXms0NUshggh_BKIIiqm9yddHVtO_jkEnskIZJJGIu26BPh7zu4W1XQ3C1-DJlt3RhHa9ZKz3J2tmoCrBbgcvS48PdhD2auceGd)

Um outro exemplo bem usado é quando você quer voltar ao estado original que estava no repositório remoto. Importante lembrar que ao rodar esse comando, você perderá o que está localmente! Logo, rodando esse comando, você recuperará o histórico mais recente da branch main do servidor e apagará todas as alterações e commits locais.

```
git reset --hard origin/main
```

### 7. Git revert: Desfazendo um commit sem excluir os dados existentes!

O **git revert** faz parte de comandos do tipo “desfazer”. Mas ele não é uma opção tão tradicional. Basicamente, ele cria um novo _commit_ desfazendo o _commit_ que você especificar.

Criei um arquivo, adicionei um texto “primeiro conteúdo” e depois adicionei outro texto “conteúdo errado”. Fiz o _revert_ do “conteúdo errado” e como pode ver, ele adicionou um novo _commit_ fazendo o _revert. N_esse _commit,_ ele desfez as alterações do último _commit_. Ou seja, no final, o meu arquivo ficou apenas com o texto “primeiro conteúdo”.

![Desfazendo um commit sem excluir dados existentes](https://lh6.googleusercontent.com/VYpVOJYCRKEbAc_svzklxlekG2Pfge1xoTph0UNouYdIJwlm7q7Lxsx60qztx7CyutNwqzHOHaTdqoaoPgP3HjojWbt1MiBUf-5dGD-NOPX66bOdnDTWvQIJA64_-kTjNRBQYJIQ)

### 8. Git diff: verificando as diferenças entre arquivos e repositórios!

Você pode ver as diferenças dos seus arquivos ou também entre os repositórios local e remoto. Para isso, você pode rodar o comando **git diff** depois das alterações que você fizer no seu repositório local ou, se você precisar ver antes de um _merge,_ por exemplo, você também pode executar **`git diff <branch origem> <branch destino>`**.

![Diferenças entre arquivos e repositórios](https://lh3.googleusercontent.com/-4EaK9jLzHeWN064Ise_2cbvoiboqkpwcXUwNX7UyOjQGxDz2Wrtq0g1Yz0HBJeVegY6PcRP0Zb5nC2hcZwPdwW1SPzRI5j-yl_pb_B6uXSQ1bZmpaxPnyDz_6rodaJ2yKl4NEH9)

### 9. Git remote: ligando seu repositório local a um repositório remoto!

Se você não clonou um repositório, você pode ligar o seu repositório local a um servidor com o comando _remote._ Para isso, basta usar **`git remote add origin <servidor>`**.

### 10. Git push: enviando as alterações do repositório local para o repositório remoto!

Depois que você fez as alterações, adicionou para a área de _staging_, fez os _commits_, você pode fazer o _push_. Ou seja, você consegue mandar todas essas alterações do seu repositório local para um remoto. Para isso, use o comando **git push origin main**, no qual _main_ pode ser substituúida por qualquer outra _branch_ que você estiver trabalhando. 

### 11. Git branch: listando e deletando branches 

Para listar todas as branches que estão em um repositório, basta rodar **git branch**. Para deletar uma branch específica basta rodar **git branch -d nome_da_branch**.

### 12. Git checkout: criando uma nova branch e restaurando arquivos!

Para criar uma nova branch, você deve rodar o comando **git checkout -b nome_da_branch**. E, para alternar entre _branches,_ basta rodar **git checkout nome_da_branch**.

Agora, se você tiver feito algo errado e quiser restaurar o arquivo ao seu estado original, você pode rodar **git checkout — nome_do_arquivo**. Mas, isso só funcionará se o arquivo ainda estiver no _working directory_. Caso já esteja na área de _staging_, você terá que, primeiro, fazer um _reset_ para depois conseguir fazer um _checkout_.

### 13. Git merge: mesclando as alterações em sua branch à branch master

Quando você precisa trazer as atualizações da _branch main_, a principal, para a _branch_ que você está trabalhando, basta rodar da sua _branch_: **git branch main**. Se não tiver nenhum conflito nos arquivos que você mexeu na sua _branch_ com as alterações da _main_, você não terá que fazer mais nada. Agora se tiver algum conflito, vai aparecer no seu [terminal](https://blog.betrybe.com/tecnologia/tudo-sobre-cli/) que houve um conflito e quais os arquivos conflitantes. Você precisará abrir cada um deles e escolher qual versão do código você vai querer manter.  

### 14. Git pull: atualizando o repositório local com a versão do repositório remoto! 

Quando você precisa atualizar o seu repositório local com a mais nova versão do repositório remoto, basta usar o comando **git pull**. Dessa forma, ele verificará se tem uma versão mais recente e, se tiver, vai baixar as diferenças para o seu computador.  

### 15. Git rebase: integrando todas as alterações de um branch em outro branch

O **git rebase** move e combina sequências de _commits_ para uma nova _branch_ de uma forma mais linear. Uma das diferenças do _rebase_ para o _merge_ é que o _rebase_ mantém esse histórico do projeto de uma forma mais linear e organizada. O comando é simples, mas todo o conceito de como ele funciona é mais complexo. Para rodar, basta usar **`git rebase <branch>`**. Na imagem abaixo, mostramos o que acontece com o histórico quando fazemos um rebase:

![Exemplo de branch após rebase](https://lh3.googleusercontent.com/ZOPOVHFY0oJwwjLFtDa6AZkG1kVMZoHEVGCnL_nE2ctay6TeBRE0fpP7d2rxZHEzJ6IcUD7XAdfV3he92Hs9nGGDQ-jojWWMQ-fHf52TP8SJvljuHNAWgBVaysbWGMzwqIeEDI8k)

### 16. Git stash: criando um backup das alterações atuais do seu projeto

O **git stash** serve para guardar ou arquivar as alterações que você fez por um determinado tempo. Ele é bem útil quando você precisa mudar de contexto rápido e ainda não está pronto para fazer um _commit_, ou também quando você precisa fazer um teste de uma nova [linha de pensamento](https://blog.betrybe.com/carreira/pensamento-sistemico/) e não quer perder tudo que já fez antes de ter certeza que a nova abordagem funcionará. Para usar o comando **git stash** e para recuperar as alterações, basta usar **git stash pop**.

### 17. Git clone: baixando o código fonte de um repositório!

Você consegue clonar, ou copiar, o projeto para o seu computador. Você pode clonar um repositório [localmente](https://blog.betrybe.com/tecnologia/tudo-sobre-localhost/), fazendo uma cópia dele. Para isso, basta rodar **git clone /caminho/para/o/repositório**. Ou você também pode clonar um repositório remoto e para isso usar **git clone “url”**.

Git é algo essencial no [universo da programação](https://blog.betrybe.com/carreira/tudo-sobre-tecnologia-da-informacao/) nos dias de hoje! Você pode achar um pouco difícil de entender no início, mas vai perceber o quanto ele vai ajudar você e seu time no dia a dia. Além de você não precisar mais ter medo de perder código ou de algo dar errado e não conseguir desfazer. Independentemente de qual área da programação você seguir, é uma ferramenta muito importante em qualquer uma delas! 

Gostou de aprender sobre Git? Aprenda agora sobre [Python e saiba tudo sobre essa linguagem de programação](https://blog.betrybe.com/python/)!





###### Fonte [Blog Trybe](https://blog.betrybe.com/git/)