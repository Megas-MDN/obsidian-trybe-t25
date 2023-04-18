[[Node]]

- [O que são rotas?](#O%0dque%0dsão%0drotas?)

Até agora, conseguimos configurar nosso projeto e criar o servidor Node.js que tanto desejamos.

Lembremos que nosso objetivo é uma aplicação de gerenciamento de times de futebol! Então o que nos falta fazer?🤔

A aplicação propriamente dita!

Precisamos dar a possibilidade de cadastrar um novo clube, listar clubes, alterar um clube e deletar um clube de futebol, o famoso **C.R.U.D.**.

Todo mundo que está estudando na Trybe fez uma inscrição no curso, correto?

Quando você se inscreveu no curso, uma API da Trybe **criou** seu cadastro. Toda vez que você tenta se logar em sua conta, a API da Trybe **lê** (pesquisa) seus dados de algum lugar e quando pedimos para você atualizar o endereço, por exemplo, a API **altera** o dado. A única coisa que a API da Trybe não faz,neste caso, é **deletar**, pois você é muito importante para nós. 🥰💚

Relembrando 🧠: Queremos ligar o **Front-end** com o **Banco de dados**. Para isso, você irá criar APIs que vão receber **requisições** e **devolver dados**.

Já que estamos em um dia de metáforas culinárias, podemos dizer que isso é como um restaurante. O **Front-end** é a área das mesas, chamada de “Salão”. A pessoa que te atende é a comunicação direta entre clientes e cozinha, é quem envia as requisições do **Front-end**. O **Back-end**, por sua vez, é a cozinha, onde uma pessoa cozinheira, mediante o recebimento de um pedido, vai prepará-lo e devolvê-lo para ser entregue à área das mesas, ou seja, ao **Front-end**.

> É no Back-end que os dados serão **filtrados**, **manipulados** e **preparados** para envio ao Front-end. Esse, por sua vez, se encarrega de apresentá-los a quem fez o pedido.

Ainda na analogia da cozinha, uma API seria o quadro de pedidos, no qual os setores de “Cozinha” e “Salão” se comunicam em duas ocasiões:

-   Quando o `client` envia uma `requisição` para o `back-end`; (aqui a pessoa anota seu pedido e leva para cozinha);
    
-   Quando o `server` envia a `resposta` para o `front-end`; (aqui novamente a pessoa que anotou o pedido, agora devolve o prato pronto).
    

A imagem abaixo ilustra esse funcionamento:

![Imagem que demonstra o panorama de uma aplicação web](https://content-assets.betrybe.com/prod/Imagem%20que%20demonstra%20o%20panorama%20de%20uma%20aplica%C3%A7%C3%A3o%20web.jpeg)

Imagem que demonstra o panorama de uma aplicação web

Mas, como que essa comunicação acontece? 🤔

Isso varia de acordo com ~~a API~~ o restaurante, entretanto, temos algo como uma comanda: uma forma já combinada de se anotar e enviar os pedidos, com a informação necessária para entregá-lo. Em uma API, essa forma combinada se materializa nas **rotas** e nos **parâmetros** delas.

## O que são rotas?

Sabia que você já viu uma rota e já a usou? Na verdade, você faz isso o tempo todo 😁

Anota aí 🖊: No contexto de Back-end, **rotas** representam as portas de entrada para a sua API.

Imagine que nosso restaurante é um que oferece pratos feitos. Em uma janela você pega o seu prato, na outra a sua bebida e em uma terceira janela você paga. No nosso caso, podemos criar as rotas que quisermos.

Mas, já demos a dica de um padrão precioso e muito útil, lembra? As **ações** do **C.R.U.D.**: Criar, ler, atualizar e remover. Pois é, nossa API terá quatro rotas.

De olho na dica 👀: Rotas podem ser chamadas de **caminhos**, **paths** e **endpoints** de uma API.

Você pode estar se perguntando: “Quando de fato vou conseguir ver o código”? 🙄

Chegaremos lá! Mas antes, para falar de rotas, precisamos falar de URLs. Uma URL tem uma anatomia, assim como mostra a figura abaixo:

![Anatomia de uma URL](https://content-assets.betrybe.com/prod/Anatomia%20de%20uma%20URL.png)

Anatomia de uma URL

E eis que temos a rota! No exemplo da URL acima, temos o caminho, do inglês _path_, `/login`, para o qual queremos enviar ou pedir algo.

> Em suma, queremos fazer uma requisição para que esse caminho receba e processe algo ou nos dê algo.

Anota aí 🖊: **uma rota é a parte de uma URL que usamos para acessar uma API e fazer uma requisição a ela.** Por meio da rota, na nossa aplicação, requisitaremos acesso, criação, leitura ou remoção de informações da nossa API de gerenciamento de times. Em suma, quando você digita uma URL no navegador, por “trás dos panos” ele está fazendo uma requisição àquela rota. Quando uma aplicação Front-end faz uma requisição para uma URL, ela quer algo de alguma rota da API. Precisamos saber como as requisições chegam para podermos criar nossas próprias rotas e processá-las!

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4982a599-9832-419e-a96b-3fe1db634c3e/lesson/1b67ccb4-29ae-4b0f-8bd6-8cab9a75312d)