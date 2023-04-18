[[Carreira]]
[[Git]]


## O que é?

Um portfólio de uma pessoa desenvolvedora é mais do que um simples currículo. Em essência, é uma vitrine que prova que você pode fazer o que fala em seu currículo.

Em vez de contar às pessoas recrutadoras sobre suas habilidades, você pode criar um portfólio de pessoas desenvolvedora de software para mostrá-las. Como já vimos no conteúdo [exercícios](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/52bf729e-7389-4f30-8b48-1fb3de822cd2/lesson/292cde5b-4528-4dd9-b42d-a03c1405f2d2).

## Por que isso é importante?

Então, por que você deve criar um site de portfólio de pessoa desenvolvedora? Vale a pena o esforço?

Um site de portfólio de pessoa desenvolvedora não apenas atua como uma vitrine para seus exemplos de trabalho anteriores, mas o próprio site é um exemplo do que você pode fazer!

Bora ver como podemos criar um e o que devemos usar ?

## Criando seu portfólio com GitHub Pages

[GitHub Pages](https://pages.github.com/) é um serviço grátis disponibilizado pelo próprio GitHub, no qual você pode hospedar aplicações web e publicá-las por meio do GitHub. Existe a possibilidade de modificar o conteúdo e o estilo das suas páginas do GitHub remotamente, pela web ou localmente em seu computador.

### Como organizar meus projetos em meu portfólio ?

A ideia é que cada um de seus projetos seja um repositório para que você possa subi-los individualmente no `GitHub Pages`. Porém, o seu portfólio deve ser criado em um repositório com seu nome de usuário, `username.github.io`.

![create_portfolio](https://content-assets.betrybe.com/prod/create_portfolio.png)

Em seguida, basta fazer um clone do repositório criado em sua _maquina_ e começar a desenvolver seu portfólio!

### Pontos chaves para abordar

Um portfólio deve sempre incluir os seguintes pontos:

-   `Sobre mim`: as pessoas não te conhecem ainda, então certifique-se de que seu portfólio inclua alguns detalhes sobre isso. Inclua seu nome, uma foto e uma breve sinopse sobre o que você fez e onde espera chegar em sua carreira. É uma boa ideia refinar essa narrativa ao longo do tempo, à medida que sua carreira progride. Desenvolver a história da sua marca leva tempo, mas é um ativo único que você pode cultivar para ajudar no crescimento de sua carreira;
    
-   `Projetos`: o ponto crítico de qualquer portfólio de programação será o lar dos melhores exemplos de seu trabalho. Esta seção deve ser o mais cativante possível, então seja criativo com suas habilidades, _GIFs_, _design_ e texto atraentes são bem vindos aqui;
    
-   `Contato`: sem isso você pode estar prejudicando suas chances de obter ofertas de emprego. Idealmente você deve incluir um formulário de contato e seus canais de mídia social. Se você não fizer isso, no mínimo, adicione seu endereço de e-mail e links para seus perfis do LinkedIn e GitHub.
    

## Subindo projetos GitHub Pages

Agora que já sabemos como criar nosso portfólio, como podemos colocar nossos projetos nele? Bom, então esse é o motivo pelo qual cada projeto deve estar em um repositório separado, dessa forma, você hospeda cada um em uma `URL` diferente!

Exemplos:

-   `https://username.github.io/app-recipes/`;
    
-   `https://username.github.io/trybeer/`;
    
-   `https://username.github.io/tech-news/`.
    

### Subindo seu projeto React no GitHub Pages

Mas afinal de contas, como fazemos isso? Bora por a mão na massa!

![giphy](https://content-assets.betrybe.com/prod/giphy.gif)

#### Passo a Passo

1.  Instale o pacote [gh-pages](https://github.com/tschaub/gh-pages) no seu projeto:
    

Copiar

```bash
1$ npm install gh-pages
```

-   Adicione os as seguintes propriedades no seu arquivo `package.json`:
    

Copiar

```js
1"homepage": "https://username.github.io/app-toot-name",
2"scripts": {
3  "predeploy": "npm run build",
4  "deploy": "gh-pages -d build",
5},
```

-   Execute o deploy da sua aplicação:
    

Copiar

```bash
1$ npm run deploy
```

-   Por fim, é necessário habilitar a configuração do `GitHub Pages` em seu repositório. É importante que a branch habilitada seja a **gh-pages**.![github_pages_config](https://content-assets.betrybe.com/prod/github_pages_config.png)
    
-   E _voilá_, basta acessar a **URL** do seu portfólio `github_user_name.github.io`
    

![giphy](https://media.giphy.com/media/iILWthRkRKiSEs06Bo/giphy.gif)

### Exemplos

Nessa seção você encontra alguns portfólios de projetos de Trybers, desse modo você poderá ver as possibilidades e também ter uma noção do resultado que obterá.

-   [Portfólio de Projetos - Johnatas Henrique (SD-02);](https://johnatas-henrique.github.io/)
    
-   [Portfólio de Projetos - Douglas Henrique (SD-02).](https://douglas-he.github.io/)

# Publicando projetos feitos na Trybe


## Porque isso é importante

Os projetos da Trybe realizados por você durante o curso são uma ótima demonstração da sua capacidade técnica. Muitas empresas querem ver esses projetos no seu GitHub, e é essencial que o código apresentado esteja no seu perfil pessoal.

**Para se destacar na busca pelo primeiro trabalho em tecnologia**, é essencial que a pessoa desenvolvedora demonstre sua experiência com projetos. Ao longo da formação da Trybe, você realizará mais de 30 projetos aplicando conceitos e tecnologias desejadas no mercado de trabalho.

Entretanto, como os repositórios dos projetos de cada turma são privados, pessoas recrutadoras podem ter a impressão de que você não colocou seus conhecimentos em prática. Isso seria péssimo! 😰

Para resolver isso, temos esse tutorial oficial para que você publique seu trabalho de forma correta em seu GitHub pessoal, preservando todo seu histórico de _commits_, e respeitando os [Termos de Uso da Trybe](https://www.betrybe.com/termos-de-uso). 🎉

É possível transferir seu código para um repositório pessoal de várias formas! Mas para que seja possível aproveitar melhor o Git como ferramenta de versionamento, não perder o seu histórico de _commits_, limpar commits feitos pelo time da Trybe, e fazer isso de forma rápida, construímos nossa própria ferramenta!

Ah, e sabe o que é mais legal? Essa ferramenta foi construída com a colaboração de estudantes como você!

Nossa ferramenta é a [student-repo-publisher](https://github.com/tryber/student-repo-publisher), e ela já passou por diversas evoluções. Mas antes de mostrar como usar a versão mais recente, precisamos instalar algumas dependências externas necessárias.


Para que todo o processo funcione bem, usamos 2 dependências externas:

1.  **`GitHub CLI`** - precisa ser instalada e configurada manualmente, como é feito no vídeo, utilizando os passos a seguir. Usamos ela para criar oo novo repositório onde ficará seu código, além de facilitar outras etapas da automação
2.  **`git-filter-repo`** - será instalada automaticamente no passo **Instalação #2: nossa ferramenta**. Usamos ela para garantir a limpeza de arquivos sensíveis da Trybe, inclusive do histórico de _commits_

Configurar o **GitHub CLI**, a interface para linha de comando oficial do GitHub, pode ser um pouco demorado.

1.  Siga as instruções do [site oficial](https://cli.github.com/) para a instalação adequada ao seu Sistema Operacional
2.  Após a instalação, faça login com o comando a seguir.

```sh
gh auth login
```

Esse processo de login pode ser um pouco confuso 😵 mas, seguindo nossas dicas, tudo deve correr bem! 💚

#### Confira as dicas para o comando `gh auth login`

-   Você receberá a opção entre `Github.com` e `Enterprise Server`: escolha `Github.com`;
-   Você receberá a opção entre `HTTPS` e `SSH`: escolha `SSH`;
-   Você receberá a opção de escolher o arquivo com a chave `SSH` configurada no seu computador, que deve ser algo semelhante a `~/.ssh/id_rsa.pub` ou `~/.ssh/id_ed25519`: escolha o arquivo oferecido;
-   Você receberá a opção de definir um título para a chave SSH: aperte `Enter` para escolher a opção padrão;
-   Você receberá a opção entre `Login with a web browser` e `Paste an authentication Token`: escolha `Login with a web browser`;
-   Você receberá um código no formato `XXXX-XXXX` e a ferramenta aguardará você apertar `Enter`;
-   Após apertar `Enter` será aberta uma janela no seu navegador para inserir o código anterior, e seguir com o login padrão do GitHub;
-   Após finalizar o login no navegador, o terminal aguardará você apertar `Enter`;
-   Fim. 🎉

✅ Para garantir que a autenticação funcionou, utilize o comando a seguir

```sh
gh auth status

# Resultado esperado:
# github.com
#  ✓ Logged in to github.com as <username> (oauth_token)
#  ✓ Git operations for github.com configured to use ssh protocol.
#  ✓ Token: *******************
```

### Instalação #2: nossa ferramenta

Além das dependências externas, também é necessário instalar a própria ferramenta `trybe-publisher`. É muito rápido e, assim como o passo anterior, você só precisará fazer uma vez!

1.  Faça o clone do repositório;
2.  Entre na pasta gerada;
3.  Execute o script de configuração _(e siga as instruções)_.

Para executar os 3 passos anteriores de forma rápida, basta copiar o comando a seguir:

```sh
git clone git@github.com:tryber/student-repo-publisher.git ~/student-repo-publisher && \
cd ~/student-repo-publisher && \
bash publisher-config.sh
```


♻️ Para garantir que o _auto-complete_ funcionará corretamente, reinicie o terminal.

### Executando a nossa ferramenta

#### Alguns alinhamentos importantes

1.  Nossos scripts farão uma limpeza parcial do histórico de _commits_ do projeto, o que impossibilitará um novo _push_ ao repositório da Trybe. Por isso, recomendamos que você **só prossiga se já possuir aprovação no projeto escolhido**. Para interagir com o repositório original da Trybe novamente, você precisará fazer um novo `clone` do repositório da sua turma.
2.  **As configurações de limpeza de cada projeto foram construídas em meados do ano de 2022**, então podem não ser compatíveis com projetos mais antigos. Caso perceba alguma incompatibilidade (_ex: arquivos apagados indevidamente_), avise o time da Trybe.
3.  **Se o projeto não foi feito individualmente**: garanta que as outras pessoas que contribuíram estão de acordo com a publicação do trabalho, dê os devidos créditos a elas no `README`, e também sinalize no `README` quais partes do código foram implementadas por você. Se as pessoas envolvidas **não concordarem** com a publicação do trabalho, você ainda pode usar a ferramenta com o parâmetro `--private`.
4.  Após a execução da ferramenta, **alguns arquivos fornecidos pela Trybe serão mantidos**. Não se preocupe: são arquivos que autorizamos você a compartilhar, desde que você informe no `README` que eles são de autoria da Trybe. A ferramenta deve excluir apenas o `README` original e os testes da Trybe que avaliam os requisitos do projeto, assim como arquivos e pastas auxiliares ao avaliador da Trybe ( `trybe.yml` , `.github/*` e `.trybe/*`).
5.  **Ao final da execução, sua pasta local estará sincronizada com o novo repositório criado**. Se você (i) editar um arquivo, (ii) fizer um _commit_ e depois (iii) fizer o _push_, a alteração irá refletir no novo repositório!

#### Passo-a-passo

Chega de enrolação, vamos lá! Após realizar as instalações, esse é o passo-a-passo que você irá executar para cada projeto:

1.  Acesse na sua máquina o diretório do projeto desenvolvido. Exemplo:

```sh
cd trybe/projetos/sd-00-x-project-zoo-functions
```

2.  Garanta que você não possui nenhuma alteração pendente no repositório
3.  Execute o seguinte comando, substituindo os parâmetros

```sh
trybe-publisher -b sua_branch -p nome_novo_repositorio
```

-   `sua_branch` é o nome da branch que possui seu código no projeto escolhido;
    -   Obs1: Se a instalação ocorreu sem problemas, você conseguirá usar `<tab>` para auto-completar o nome da branch;
    -   Obs2: Você não precisa inserir o nome completo da sua branch. Por exemplo, conseguiremos encontrar a branch `mike-wazowski-zoo-functions` se você inserir apenas `wazowski`.
-   `nome_novo_repositorio` é o nome do repositório que será criado no seu GitHub pessoal.

Nossa ferramenta também possui outros parâmetros opcionais:

-   `-h`: Exibe todos os parâmetros (_obrigatórios e opcionais_)
-   `-d "Descrição do projeto"`: Descrição do novo repositório criado em seu GitHub. O padrão é vazio
-   `-r nome_remote`: Nome para o remote referente ao novo repositório criado. O padrão é `origin`
-   `--private`: Define o novo repositório como _privado_. Por padrão, o novo repositório será criado como _público_

🎉 **Pronto!**

Ao final da execução você receberá o link para o repositório criado, que terá apenas a _branch_ `main` com a versão do seu projeto. Todos os seus _commits_ estarão registrados, e os arquivos sensíveis da Trybe removidos. O novo repositório estará sincronizado com o diretório local, o que significa que você pode fazer _commits_ e _push_ sem preocupações.

![Comemoração](https://content-assets.betrybe.com/prod/7508618d-ffb7-4503-88e5-44dce75c19e2-Comemora%C3%A7%C3%A3o.gif)


### E agora?

Aproveite nossas dicas no conteúdo de **“GitHub e Carreira”** para construir um bom README e compartilhe seu trabalho no LinkedIn!

## Atualizando a ferramenta e solucionando problemas

### Erros inesperados na execução do `trybe-publisher`

Ao executar o `trybe-publisher` para algum projeto você receber um erro inesperado, ou seja, um erro que a ferramenta não informou nitidamente o motivo. Nesse caso, você provavelmente precisará fazer um novo `clone` do repositório da sua turma.

### Atualização simples

Se houver alguma atualização na ferramenta do repositório [student-repo-publisher](https://github.com/tryber/student-repo-publisher), basta executar o seguinte comando:

```sh
cd ~/student-repo-publisher && \
git pull origin main && \
bash publisher-config.sh
```

Se você apagou o diretório `~/student-repo-publisher` gerado na instalação, o comando anterior irá mostrar uma mensagem de erro por tentar acessar uma pasta que não existe. Nesse caso você deve executar novamente os passos descritos em “**Instalação #2: nossa ferramenta**“.

### Atualização profunda

Durante a execução do `trybe-publisher`, a ferramenta cria uma **pasta oculta** para gerenciar parte da execução. Remover essa pasta não afetará a execução da ferramenta, mas pode corrigir alguns problemas.

Para isso, além do passo de “**Atualização simples**“, execute o comando a seguir:

```sh
rm -rf ~/.student-repo-publisher
```



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/a3cac6d2-5060-445d-81f4-ea33451d8ea4/section/d4f5e97a-ca66-4e28-945d-9dd5c4282085/day/b47cff7f-f239-4143-a713-1b9aaa7cc089/lesson/35fa3c3c-38f2-40cd-84a8-5b369ae786a5)
