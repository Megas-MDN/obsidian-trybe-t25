[[JavaScript]]
[[HTML]]

## O DOM. Ou: como o _HTML_ e o _JavaScript_ se comunicam?

O `DOM` (Document Object Model) é uma interface que representa como os `HTML` e `XML` são lidos pelo browser. Após a leitura do documento `HTML` pelo browser, o `DOM` cria um objeto que faz uma representação do documento e define meios de como essa estrutura pode ser acessada. Dessa forma, podemos utilizar o `JavaScript` para manipular o `DOM` e, assim, alterar o estilo e o conteúdo de nossa página.

No `DOM` nossa página é representada por nós e objetos, e é através deles que iremos realizar a comunicação do nosso `HTML` com o `JavaScript`. Sendo assim, podemos dizer que o `DOM` é uma representação orientada a objetos da página da web, que pode ser modificada com uma linguagem de script como JavaScript.
![[Pasted image 20221024211738.png]]
> Estrutura DOM

Nessa imagem temos um exemplo da árvore do `DOM`, suas marcações e como ela é montada pelo browser. Vejamos um pouco mais sobre os objetos que a imagem apresenta:

-   `Window`: Representa uma janela que contém um elemento DOM, sendo possível acessar o documento que a janela contém através de `Window`;
    
-   `location`: Representa a localização do objeto ao qual ele está associado, isto é, o documento atual;
    
-   `document`: Representa qualquer página da web carregada no navegador e serve como um ponto de entrada para o conteúdo na página da web. Sendo assim, o `document` contém todos os documentos `HTML`;
    
-   `history`: Permite a manipulação do histórico da sessão do navegador, ou seja, as páginas visitadas na guia ou quadro em que a página atual está carregada;
    
-   `element`: É a classe base mais geral da qual todos os objetos em um `Document` herdam, isto é, são todas as tags que estão em arquivos `HTML` e se transformam em elementos da árvore `DOM`;
    
-   `text`: Texto que vai entre os elementos, é todo o conteúdo das tags;
    
-   `atribute`: São todos os atributos que um nó específico possui, como uma `class` ou `id`.
    

Ficou nítido? Ou a ideia do que é o DOM ainda está um pouco abstrata?

Pense assim: a página _HTML/CSS/JS_ que você faz é um programa. O navegador é quem interpreta esse código e, a partir dele, gera a página que você vê na Internet.

Pois bem, o DOM é uma estrutura da sua página que o navegador monta quando lê. O seu intuito é justamente permitir ao programa acessar os elementos da página usando código e dar a ele o poder de manipulá-los.

Se, ainda assim, o conceito de DOM estiver um pouco abstrato, não se preocupe! Tudo vai ficar mais nítido quando você começar a interagir com ele.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/859613ad-86a2-42f2-ab66-2264d723686f/lesson/c5ed1d4b-1a63-426e-a638-861e60f0a352)
