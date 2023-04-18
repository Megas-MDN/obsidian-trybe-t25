[[Git]]

Um repositório é uma pasta do seu computador na qual você pode armazenar arquivos, projetos etc. Quando se trata de versionamento, o repositório é uma pasta que contém o seu projeto. É nessa pasta que você consegue criar versões, isto é, as _branches_. Todo esse processo pode ser feito pelo terminal utilizando linhas de comando. Os comandos podem variar de acordo com os seguintes tipos de repositório:

-   **Repositório local**: é o repositório do seu computador. Pode ser baixado da internet ou criado por você.
-   **Repositório remoto**: é o repositório que pode ser acessado via internet, em uma plataforma de hospedagem de código, como o **GitHub**.

> **Atenção ⚠️**: Você vai aprender mais sobre _repositório remoto_ mais adiante. Para chegar lá, é necessário praticar bastante os comandos deste conteúdo. Vamos ver, na prática, como criar um repositório local?

## Criando um repositório local

Agora, é hora de praticar! Você vai criar um repositório no seu computador utilizando os comandos do **Git**. Para criar o seu primeiro repositório versionado, você vai precisar:

-   Criar uma pasta e inicializar o versionamento;
-   Realizar uma modificação na _branch main_ para ter um projeto inicial;
-   Criar uma nova _branch_ e realizar novas alterações;
-   Mesclar as alterações da _branch_ criada por você na _branch main_.

Vamos nessa?

### Primeiro passo: Crie uma pasta no seu computador

Abra seu terminal e escolha o local em que você vai criar o seu repositório, esse local precisa ser uma **pasta nova** e portanto não pode ser a própria raiz do sistema (`/`) ou o diretório da pessoa usuária (`%`). Em seguida, acesse essa pasta que foi criada.

> **Relembrando 🧠**: Veja, a seguir, alguns comandos do terminal do computador.
> 
> -   `ls`: verifica as pastas e os arquivos que estão no caminho.
> -   `cd nome-da-pasta`: acessa a pasta.
> -   `mkdir`: cria uma pasta.
> -   `touch`: cria um arquivo novo.

### Segundo passo: Inicie o repositório Git com o comando `git init`

Utilize o comando `git init` dentro da pasta que você criou para que ela se torne um repositório Git.

![Criando o repositorio versionado com git init](https://content-assets.betrybe.com/prod/a5307822-62e0-433b-a933-1d8b4f7f84b9-Criando%20o%20repositorio%20versionado%20com%20git%20init.png)

Criando o repositório versionado com o comando `git init`.

### Terceiro passo: Troque o nome da _branch_ principal para _main_

Após usar o `git init`, a resposta do seu terminal deve ser parecida com esta:

```bash
Initialized empty Git repository in /Users/leticia/Desktop/meu-primeiro-repositorio-git/.git/
```

Ao iniciar um repositório local, o Git inicia sua _branch_ principal com o nome **_master_**, mas esse nome foi descontinuado. O ideal é chamá-lo de **_main_**.

> **Observação 🔎**: Você pode verificar em qual _branch_ você está por meio do comando `git branch`. Atenção: nas versões mais recentes do _Git_, antes do primeiro `commit` o comando `git branch` não mostrará nada, isso é normal.

Caso este aviso apareça para você…

```bash
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
```

… em seu terminal, configure a _branch_ principal para que ela sempre se chame _main_, o que fará esse aviso desaparecer. Para isso:

-   Renomeie a _branch_ atual para _main_ por meio do comando `git branch -m main`;    
-   Configure o nome _main_ com o comando `git config --global init.defaultBranch main`.

### Quarto passo: Verifique o _status_ do repositório com `git status`

Execute o comando `git status` no seu terminal para verificar a situação atual do seu repositório.

O comando `git status` retorna o _status_ do repositório e informa quais arquivos foram modificados, quais estão sendo monitorados etc. No contexto de um repositório recém-criado, no qual nenhuma modificação foi feita, você vai ter a seguinte resposta:

```bash
On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

### Quinto passo: Configure seu nome e _e-mail_ do Git

Antes de adicionar as alterações dos seus arquivos, o Git precisa saber seu nome e _e-mail_ para associar seus dados às alterações que fizer. Para fornecer essas informações, execute o comando `git config --global user.name "Nome Sobrenome"` e substitua `Nome Sobrenome` pelos seus dados.

Em seguida, execute o comando `git config --global user.email "SEU_EMAIL"` e substitua `SEU_EMAIL` pelo seu _e-mail_. Lembre-se desse _e-mail_ e de inserir o domínio (`@gmail.com`, por exemplo), pois na próxima aula você criará uma conta no GitHub com ele.

Para conferir se a operação funcionou, execute os comandos `git config user.name` e `git config user.email`. Seu terminal deve mostrar os dados que usou na configuração:

```bash
git config user.name
Nome Sobrenome
git config user.email
seuemail@email.com
```

Você está quase lá! Chegou o momento de utilizar os comandos `git add`, `git commit` e `merge`.



## Adicionando e comitando arquivos

Depois de ter inicializado seu repositório local, é hora de iniciar as alterações. Para isso, vamos criar um arquivo chamado `README.md`.

> **Anote aí 📝**: O `README.md` é um arquivo de marcação de texto responsável por informar e orientar sobre como utilizar o projeto.

### Primeiro passo: Crie um arquivo chamado `README.md`

Para criar um arquivo utilizando o terminal, execute o comando: `touch README.md`.

Adicione, também, um arquivo inicial a essa pasta para ter a estrutura inicial do projeto.

### Segundo passo: Abra seu repositório no VS Code

Para abrir o repositório no VS Code utilizando o terminal, execute o comando `code .`.

Para configurar o VS Code como editor-padrão, acesse a página [Git e GitHub](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/876a615b-f578-4d65-a820-de9f3e5e57db/lesson/e758e1be-f8cc-4824-98c5-9f39c8969258).

> **Atenção ⚠️:** Caso utilize macOS, o comando `code` precisa ser configurado. Veja como fazer essa configuração acessando o _link_ a seguir, mais especificamente em [Lauching from the command line](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).
> 
> Se precisar traduzir, clique com o botão direito do _mouse_ na página e, em seguida, em “Traduzir para o português”.

Após executar o comando, o VS Code vai abrir no seu computador já dentro do repositório.

### Terceiro passo: Faça uma alteração no arquivo `README.md`

Abra o arquivo `README.md` e escreva este texto:


```bash
Meu primeiro repositório git!!
```

> **De olho na dica 👀**: Ao iniciar um repositório local e antes de criar novas _branches_, é necessário fazer uma alteração na _branch main_.

### Quarto passo: Adicione a alteração na _branch main_

Para que o Git adicione sua alteração a uma zona de **_stage_**, prepare as alterações para torná-las uma versão do projeto, desta forma:

-   Abra o terminal no VS Code. Você pode acessar a aba `Terminal > Novo Terminal`;
-   Garanta que você está dentro da pasta do repositório e utilize o comando `git add README.md` ou o `git add .`:

```bash
git add README.md
```

Caso você queira adicionar todos os arquivos modificados, utilize o comando `git add .`:

```bash
git add .
```

> **De olho na dica 👀**: Uma boa prática é utilizar o comando `git status` antes de `git add` para checar quais arquivos foram modificados. Dessa forma, você consegue visualizar quais arquivos sofreram alteração e garantir que vai executar o comando `git add .` sem enviar arquivos indesejados.
> 
> Você também pode usar o `git status` após o `git add`. Essa ação vai mostrar quais arquivos estão na zona de _stage_ ou _staging_, isto é, a área de arquivos que estão preparados para serem enviados no próximo _commit_.

### Quinto passo: Escreva uma mensagem com `git commit`

Após adicionar as alterações realizadas em _stage_, é necessário informar, em uma mensagem, o que foi alterado. Dessa maneira, você consegue criar um _ponto de acesso_ na sua linha do tempo, ou seja, você cria uma versão do seu projeto e consegue acessá-la sempre que precisar.

A mensagem de _commit_ é muito importante, pois descreve o que foi modificado. Para registrá-la, digite no seu terminal um texto que descreva a alteração que você fez. Por exemplo:

```bash
git commit -m "Cria README.md"
```

> **Anote aí 📝**: Não é possível realizar um _commit_ em um repositório vazio. É necessário que haja dentro dele ao menos um arquivo criado, ainda que em branco.

![Felicidade em fazer o primeiro commit](https://content-assets.betrybe.com/prod/a5307822-62e0-433b-a933-1d8b4f7f84b9-Felicidade%20em%20fazer%20o%20primeiro%20commit.gif)

Pronto! Suas primeiras alterações foram realizadas. Fonte: gifer.com

Os comandos ficam da seguinte forma:

-   `git add .` ou `git add nome-do-arquivo nome-do-outro-arquivo` adicionam as modificações em _staging_ e informam ao Git que as modificações realizadas vão estar no próximo _commit_;
    
-   `git commit -m "Mensagem sobre as alterações realizadas"` informa quais alterações foram realizadas e cria uma versão do projeto que pode ser acessada a qualquer momento;
    
-   `git status` pode ser utilizado sempre que você quiser verificar o que foi alterado.
    

> 👀 **De olho na dica**: O hábito de realizar _commits_ com frequência é considerado uma boa prática, pois facilita o acompanhamento das alterações e a correção de possíveis erros em seu código. Evite _commits_ muito extensos e/ou com muitas alterações.

## Relembrando 🧠

Resumidamente, o processo acontece na seguinte ordem:

-   Crie uma pasta para armazenar um repositório local: `mkdir <nome da pasta>`;
-   Acesse a pasta criada: `cd <nome da pasta criada>`;
-   Inicie um repositório local nessa pasta, em que é possível ter o controle de versionamento: `git init`;
-   Faça uma modificação inicial, por exemplo: `touch README.md`;
-   Faça uma verificação de quais arquivos foram alterados: `git status`;
-   Adicione os arquivos modificados e selecionados ao que será a próxima versão: `git add` (`git add README.md` ou `git add .`);
-   Crie uma nova versão desse repositório local, com uma descrição das diferenças dessa versão em relação à antiga: `git commit -m "Mensagem desejada"`.


## E o `git merge`?

Ao iniciar um repositório local, é necessário realizar pelo menos uma modificação inicial na _branch main_ (e _commitar_), que vai ser a sua primeira versão. Feita essa modificação, você pode criar uma nova _branch_ para realizar outras alterações. Então, a partir da _branch main_ você vai criar uma nova _branch_ e realizar novas alterações para só então realizar o _merge_. Acompanhe os seguintes passos:

### Primeiro passo: Crie uma _branch_ nova com `git checkout -b nome-da-branch`

Para criar uma nova _branch_ e acessá-la, você pode utilizar o comando `git checkout -b` e escolher o nome que quiser para a sua _branch_:

```bash
git checkout -b atualiza-readme
```

> **Anote aí 📝:** Você pode criar quantas _branches_ (ramificações) forem necessárias, bem como criar novas _branches_ a partir de _branches_ já existentes. Para verificar em qual _branch_ você está, utilize o comando `git branch` ou, se preferir, verifique o lado **inferior esquerdo** do seu VS Code, local em que há a informação da _branch_ em que você está atualmente.

![Exemplo da branch atual no VSCode](https://content-assets.betrybe.com/prod/a5307822-62e0-433b-a933-1d8b4f7f84b9-Exemplo%20da%20branch%20atual%20no%20VSCode.png)
> Exemplo da _branch_ atual no VS Code.

### Segundo passo: Realize uma nova modificação no `README.md`

-   Escreva algo novo no seu arquivo `README.md`;
-   Utilize o comando `git status`;
-   Adicione e envie as alterações para _staging_ por meio do comando `git add README.md` ou do `git add .`;
-   Utilize o `git status` novamente;
-   Realize o _commit_ por meio do comando `git commit -m "Atualiza README.md"`.

### Terceiro passo: Realize o _merge_ na _branch main_

Chegou o momento de unir as alterações realizadas na _branch_ que você criou à _branch main_. Para isso:

-   Acesse a _branch main_ por meio do comando `git checkout main`;
-   Digite o comando `git merge nome-da-branch`, em que `nome-da-branch` é o nome que você deu para a sua _branch_. Por exemplo: `git merge atualiza-readme`.

Esse comando vai fazer as alterações da _branch_ que você criou serem “mergeadas” na _branch main_, ou seja, você unirá a alteração feita na sua _branch_ com a _branch main_.

São muitos comandos, não é mesmo? Mas não se preocupe, pois alguns se encontram resumidos na imagem a seguir.

![comandos do git](https://content-assets.betrybe.com/prod/a5307822-62e0-433b-a933-1d8b4f7f84b9-comandos%20do%20git.jpg)

Comandos do Git.

Com o tempo, esses comandos ficarão cada vez mais naturais. Porém, para que isso aconteça, você precisa praticar bastante!


# Recursos adicionais (opcional)

-   [_Pro Git_, livro oficial sobre o Git, de Scott Chacon e Ben Straub](https://git-scm.com/book/pt-br/v2)
-   [Como conectar com o repositório no GitHub via SSH](https://help.github.com/en/articles/connecting-to-github-with-ssh)
-   [Reforço sobre o aprendizado do Git em um guia rápido](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/)
-   [Instalando o Git (Git setup)](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Instalando-o-Git)
-   [Configuração inicial (Git config)](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Configura%C3%A7%C3%A3o-Inicial-do-Git)
-   [Como adicionar uma chave SSH na sua conta do GitHub](https://medium.com/@rgdev/como-adicionar-uma-chave-ssh-na-sua-conta-do-github-linux-e0f19bbc4265)
-   [Tutorial para iniciar o Git e o GitHub](http://www.devfuria.com.br/git/tutorial-iniciando-git/)
-   [Documentação Oficial](https://git-scm.com/docs)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/fe827a71-3222-4b4d-a66f-ed98e09961af/day/35e03d5e-6341-4a8c-84d1-b4308b2887ef/lesson/d65eb0da-e361-4bb4-8714-c7ccc8c364a4)
