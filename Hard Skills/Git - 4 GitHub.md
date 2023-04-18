[[Git]]


Sabemos que o **GitHub** é uma plataforma de hospedagem de código, mas o que isso significa em termos práticos? O GitHub possibilita a você que salve e gerencie arquivos de código de maneira remota e que acesse o código de outras pessoas, além de permitir a outras pessoas que acessem seu código. Tudo isso é feito utilizando o **Git** como sistema de versionamento.

> **Anote aí 📝**: Não podemos esquecer que o Git é um sistema de versionamento de código, e o GitHub é uma plataforma que hospeda esse código. Para enviar ou acessar informações na plataforma do GitHub, são utilizados os comandos do Git.

Além disso, o GitHub possui ferramentas para auxiliar no trabalho em grupo e manter a qualidade do código, como o _Code Review_ (revisão de código, em português). Isso significa dizer que os times conseguem revisar um código antes de realizar o _merge_.

> **De olho na dica 👀**: No decorrer de sua trajetória em desenvolvimento, você pode se deparar com a seguinte frase: “Faz um CR?”. O **_CR_** significa **_C_**ode **_R_**eview.

O GitHub não é a única plataforma de hospedagem de código. Você também pode entrar em contato com _GitLab_, _BitBucket_ etc.

## Como o GitHub funciona?

O GitHub pode ser acessado por meio do [site](https://www.github.com/). É preciso ter uma conta e fazer a autenticação dessa conta para que seja possível realizar a conexão entre os repositórios local e remoto.

> **Atenção ⚠️**: Se você ainda não fez sua conta no GitHub, crie agora para conseguir acompanhar o conteúdo e a aula ao vivo.

Para criar uma conta no GitHub, acesse a página de [_login_](https://github.com/login) e vá em _Create an account_ (criar uma nova conta).

> **De olho na dica 👀**: O seu _username_ deve te identificar e tem destaque nos seus repositórios para todas as pessoas e empresas, então prefira utilizar nome e sobrenome, por exemplo guilhermemachado e mariaclaudiamelo.

Após criar sua conta, é importante que você faça as configurações de segurança para que sua conta fique bem protegida!


## Autenticação de segurança

#### Como funciona a conexão entre local e remoto?

Tudo o que você vai fazer ao longo do curso terá o GitHub como _workspace_ principal. Sabendo disso, é necessário estabelecer uma **ponte** entre o Git (_local_) e o GitHub (_remoto_), ou seja, você precisa ter uma conexão entre o repositório que está no seu computador e esse mesmo repositório que está remoto.

Para essa conexão entre local e remoto, faça primeiramente uma autenticação do GitHub, que permitirá a você **proteger suas informações pessoais e enviar comandos para o GitHub** diretamente do seu terminal. Quando esse processo é feito, você informa ao sistema remoto que é necessário utilizar as credenciais da sua conta para executar algum comando do Git e, ao mesmo tempo, comprova para o GitHub que você é quem diz ser.

E como fazer essa autenticação? Existem duas maneiras de realizá-la: **_HTTPS_** (_Hypertext Transfer Protocol Secure_) ou **_SSH_** (_Secure Shell_).

## Autenticar via SSH ou HTTPS?

HTTPS e SSH são as duas formas pelas quais você pode acessar o GitHub pelo terminal. Ambas são válidas, mas possuem algumas diferenças entre si.

-   **SSH**, ou _Secure Shell_, é um protocolo de criptografia de rede que transfere dados de forma segura, mesmo em redes inseguras. Por meio do protocolo SSH, você pode se conectar ao GitHub sem precisar digitar nome e chave de acesso pessoal a cada comando executado.
    
-   **HTTPS**, ou _Hypertext Transfer Protocol Secure_, é uma extensão do protocolo de internet _HTTP_, que resumidamente é um protocolo de comunicação entre sistemas e utiliza certificados digitais para autenticar dados e permitir que eles sejam criptografados de forma segura.
    

No caso do HTTPS, você precisará criar um _token_ de acesso pessoal para usar no lugar da sua senha. No entanto, **recomendamos o uso do SSH**, pois com ele podemos pular a etapa de digitar _login_ e senha do GitHub a cada comando, e ao longo do curso serão muitos comandos. Portanto, vamos utilizar o SSH como modelo padrão de autenticação.

Além de fazer essa conexão com SSH, você também vai precisar da Autenticação de Dois Fatores (_Two Factor Authentication_). Agora, você vai aprender o que é esse tipo de autenticação e como fazer toda essa configuração.

## Two Factor Authentication

_Two Factor Authentication_, ou _2FA_, é um processo de autenticação que combina dois ou mais fatores. Imagine que você está acessando sua conta em algum lugar, você precisará digitar sua senha, certo? Isso é um processo de autenticação. Contudo, quando falamos de _2FA_, existe uma camada a mais de autenticação. Por quê?

Por segurança. O processo de _Two Factor Authentication_ torna muito mais difícil de sua conta ser acessada, pois é preciso passar por mais de um processo de autenticação.

## Adicionando chave SSH e _Two Factor Authentication_

Ao trabalhar com desenvolvimento, é muito importante aprender a ler documentações e seguir tutoriais. Portanto, para realizar as autenticações necessárias que o GitHub pede, vamos disponibilizar alguns _links_ para você acessar e seguir esse passo a passo.

> **Atenção ⚠️:** Se por um acaso você encontrar algum texto em inglês e precisar de tradução, clique com o botão direito do _mouse_ na página e vá em “Traduzir para o português”.

### Primeiro passo

Adicione a chave SSH em sua conta do GitHub. Para isso, acesse este [link](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

### Segundo passo

Adicione o _Two Factor Authentication_. Para realizar a autenticação de dois fatores, acesse este [link](https://docs.github.com/pt/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication).

### Terceiro passo

Configure sua identidade. Para que o histórico de _commits_ fique registrado em seu nome, você precisa informar ao Git seu _e-mail_ e sua senha. Abra seu terminal e digite seu nome e o _e-mail_ que você utilizou para se cadastrar no GitHub:


```bash
git config --global user.name "Seu nome"
git config --global user.email seuemail@exemplo.br
```

> **Atenção ⚠️:** Caso você enfrente algum problema com as autenticações ou com a configuração de identidade, acesse o _Slack_ de sua tribo e peça ajuda. O time estará de prontidão para ajudá-lo.


## Criando um repositório no GitHub

Você pode armazenar uma variedade de projetos nos repositórios do GitHub, incluindo projetos de código aberto. Com os projetos de código aberto, você pode compartilhar o código para tornar um software melhor e mais confiável. Você pode usar repositórios para colaborar com outras pessoas e acompanhar seu trabalho. Para obter mais informações, confira "[Sobre os repositórios](https://docs.github.com/pt/repositories/creating-and-managing-repositories/about-repositories)". Para saber mais sobre projetos de código aberto, visite [OpenSource.org](https://opensource.org/about).


Você pode armazenar uma variedade de projetos nos repositórios do GitHub, incluindo projetos de código aberto. Com os projetos de código aberto, você pode compartilhar o código para tornar um software melhor e mais confiável. Você pode usar repositórios para colaborar com outras pessoas e acompanhar seu trabalho. Para obter mais informações, confira "[Sobre os repositórios](https://docs.github.com/pt/repositories/creating-and-managing-repositories/about-repositories)". Para saber mais sobre projetos de código aberto, visite [OpenSource.org](https://opensource.org/about).

**Observações:**

-   você pode criar repositórios públicos para um projeto de código aberto. Ao criar seu repositório público, lembre-se de incluir um [arquivo de licença](https://choosealicense.com/) que determina como deseja que o seu projeto seja compartilhado com outras pessoas. Para obter mais informações sobre código aberto, especificamente como criar e expandir um projeto de código aberto, criamos os [Guias de Código Aberto](https://opensource.guide/), que ajudarão você a promover uma comunidade de código aberto benéfica, recomendando melhores práticas para criar e manter repositórios no seu projeto de código aberto.
-   Você também pode fazer um curso gratuito de [GitHub Skills](https://skills.github.com/) sobre como manter comunidades de código aberto.
-   Você também pode adicionar arquivos de integridade da comunidade aos seus repositórios para definir diretrizes sobre como contribuir, manter seus repositórios seguros e muito mais. Para obter mais informações, confira "[Como criar um arquivo padrão de integridade da comunidade](https://docs.github.com/pt/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)".

1.  No canto superior direito de qualquer página, use o menu suspenso  e selecione **Novo repositório**.

 ![Menu suspenso com a opção para criação de um repositório](https://docs.github.com/assets/cb-11427/images/help/repository/repo-create.png)

2.  Digite um nome breve e memorável para o repositório. Por exemplo, "olá mundo".


![Campo usado para inserir um nome de repositório](https://docs.github.com/assets/cb-25139/images/help/repository/create-repository-name.png)


3.  Opcionalmente, adicione uma descrição do repositório. Por exemplo, "Meu primeiro repositório no GitHub".


 ![Campo usado para inserir uma descrição do repositório](https://docs.github.com/assets/cb-26377/images/help/repository/create-repository-desc.png)

 
 1. Escolha uma visibilidade do repositório. Para obter mais informações, confira "[Sobre os repositórios](https://docs.github.com/pt/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)".![Botões de opção usados para selecionar a visibilidade do repositório](https://docs.github.com/assets/cb-20877/images/help/repository/create-repository-public-private.png)

 
 1. Selecione **Inicializar este repositório com um LEIAME**.![Caixa de seleção Inicializar este repositório com um LEIAME](https://docs.github.com/assets/cb-49938/images/help/repository/initialize-with-readme.png)

 
 1. Clique em **Criar repositório**.![Botão usado para criar um repositório](https://docs.github.com/assets/cb-19887/images/help/repository/create-repository-button.png)

Parabéns! Você criou com sucesso seu primeiro repositório e o inicializou com um arquivo _LEIAME_.

#### Fazer commit da primeira alteração

Um _[commit](https://docs.github.com/pt/get-started/quickstart/github-glossary#commit)_ é como um instantâneo de todos os arquivos do seu projeto em determinado momento.

Na criação do repositório, você o inicializou com um arquivo _LEIAME_. Os arquivos _LEIAME_ são um ótimo lugar para descrever o projeto com mais detalhes ou adicionar alguma documentação (por exemplo, como instalar ou usar o projeto). O conteúdo do arquivo _LEIAME_ é mostrado automaticamente na página inicial do repositório.

Vamos fazer commit de uma alteração no arquivo _README_.

1.  Na lista de arquivos do repositório, clique em **_README.md_**.
 
![Arquivo README na lista de arquivos](https://docs.github.com/assets/cb-44661/images/help/repository/create-commit-open-readme.png)


2.  Acima do conteúdo do arquivo, clique no icone `Editar`.
3.  Na guia **Editar arquivo**, digite algumas informações sobre você mesmo.
 
 ![Novo conteúdo no arquivo](https://docs.github.com/assets/cb-15835/images/help/repository/edit-readme-light.png)


1. Acima do novo conteúdo, clique em **Visualizar alterações**.

![Botão Visualização de arquivo](https://docs.github.com/assets/cb-23166/images/help/repository/edit-readme-preview-changes.png)


4.  Revise as alterações feitas no arquivo. Você verá o novo conteúdo em verde.

![Exibição de visualização de arquivo](https://docs.github.com/assets/cb-33561/images/help/repository/create-commit-review.png)



1. No final da página, digite uma mensagem de commit curta e significativa que descreva a alteração feita no arquivo. Você pode atribuir o commit a mais de um autor na mensagem de commit. Para obter mais informações, confira "[Como criar um commit com vários coautores](https://docs.github.com/pt/articles/creating-a-commit-with-multiple-authors)".![Mensagem de commit para a alteração](https://docs.github.com/assets/cb-9378/images/help/repository/write-commit-message-quick-pull.png)



1. Abaixo dos campos de mensagem do commit, opte por adicionar o commit ao branch atual ou a um novo branch. Se seu branch atual for o branch-padrão, você deverá optar por criar um novo branch para seu commit e, em seguida, criar um pull request. Para obter mais informações, confira "[Como criar uma solicitação de pull](https://docs.github.com/pt/articles/creating-a-pull-request)".![Opções de commit no branch](https://docs.github.com/assets/cb-32137/images/help/repository/choose-commit-branch.png)



1. Clique em **Propor alteração de arquivo**.![Botão Propor alteração de arquivo](https://docs.github.com/assets/cb-13681/images/help/repository/propose-file-change-quick-pull.png)


![[Pasted image 20230302225919.png]]


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/fe827a71-3222-4b4d-a66f-ed98e09961af/day/1a530297-e176-4c79-8ed9-291ae2950540/lesson/e36c0c50-21bf-43c9-b6b5-177b0a1293e4)
[Documentação Oficial do GitHub](https://docs.github.com/pt/get-started/quickstart/create-a-repo)

