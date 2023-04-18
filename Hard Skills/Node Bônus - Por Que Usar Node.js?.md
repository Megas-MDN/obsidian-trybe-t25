[[Node]]
[[JavaScript]]

O Node.js cresceu muito nos últimos anos e isso se deve a uma série de fatores:

-   Node.js é o primeiro ambiente que suporta JavaScript tanto do lado da pessoa cliente quanto do lado do servidor.

> Uma pesquisa com pessoas desenvolvedoras em Node.js revela que essa tecnologia teve um impacto positivo em suas atividades, principalmente por meio do aumento da produtividade/satisfação e da redução dos custos de desenvolvimento.

-   A possibilidade de usar JavaScript para escrever tanto o front-end quanto o back-end está no centro de várias vantagens do Node.js.

> Em 2020, o Node.js [registrou a marca de 98.9 milhões](https://nodesource.com/blog/node-by-numbers-2020#:~:text=js%20Versions%20Downloads%20in%202020,js%20Binary%20Downloads%20in%202020.) de downloads na plataforma oficial.

-   Entre as várias companhias que possuem aplicações implementadas em Node.js destacam-se: **Amazon**, **Netflix**, **eBay**, **Nasa**, **LinkedIn** e **PayPal**.
    
-   O site [ModuleCounts.com](http://www.modulecounts.com/) aponta que o NPM, onde os pacotes Node.js são disponibilizados, está entre os repositórios com maior número de pacotes.
    

> Isso nos dá uma ideia de que o Node.js tanto tem uma comunidade extremamente ativa, quanto uma grande quantidade de ferramentas para resolver os mais diversos tipos de problema.

## Performance

Quando comparado a outras grandes tecnologias, **o Node.js nos permite escrever softwares servidores de requisições HTTP de forma muito mais eficiente**. Isso se dá pelo fato de que toda leitura e escrita que ele realiza, tanto no disco quanto na rede, é feita de forma **não bloqueante**. Ou seja, quando o servidor recebe uma requisição e precisa, por exemplo, buscar dados no banco de dados, as demais requisições não precisam esperar que a primeira termine para que possam ser atendidas.

-   **Resumindo**: em outras palavras, o Node.js realiza todas as suas operações de entrada e saída de dados de forma **assíncrona**, utilizando processamento concorrente (veremos mais sobre fluxo assíncrono nos próximos dias).

Por serem mais eficientes e otimizadas que outras tecnologias, as aplicações feitas em Node.js acabam por consumir menos recursos dos servidores que as executam, tornando o Node.js uma tecnologia, em geral, mais barata que suas concorrentes. Portanto, uma das principais vantagens do uso do `Node.js` é a performance.

## Aplicações em tempo real

A natureza não bloqueante do Node.js permite que alguns recursos sejam implementados na plataforma para facilitar o trabalho com operações em tempo real.

Bibliotecas como o [socket.io](https://socket.io/) permitem que, com poucas linhas de código, aplicações em tempo real relativamente complexas (como chats com suporte a múltiplos usuários, conversas privadas etc.) sejam criadas por completo.

Em um mundo em que a tecnologia está cada vez mais inserida em diversas áreas, ter suporte nativo da plataforma que utilizamos para aplicações em tempo real com certeza é muito bem-vindo e nisso o Node.js nos oferece uma grande vantagem!

![Pessoa assoprando uma língua de sogra em comemoração](https://content-assets.betrybe.com/prod/1da75c7a-49d3-4970-baa8-609597bc60c1-Pessoa%20assoprando%20uma%20l%C3%ADngua%20de%20sogra%20em%20comemora%C3%A7%C3%A3o.gif)

## Node.js <> JavaScript

Muitas das vantagens do Node.js vêm do fato de que a linguagem executada por ele é o JavaScript.

Relembrando 🧠: O JavaScript tem se mostrado uma linguagem extremamente versátil, estando presente em diversos ambientes, como a Web, Desktop, Mobile, dispositivos IoT (internet das coisas) e até mesmo em aparelhos televisores! Com isso, a versatilidade e baixa curva de aprendizado do JavaScript conferem ao Node um poder incrível para resolver as mais diversas situações.

## Então, Node.js é a melhor tecnologia para solução de problemas?

Você acabou de ler alguns dos motivos pelos quais o Node.js é a ferramenta ideal para vários tipos de projeto. No entanto, é importante lembrar que **não existe** _bala de prata_ quando o assunto é tecnologia, ou seja, não há uma única solução para todos os problemas.

De olho na dica 👀: A melhor ferramenta **sempre** dependerá do caso de uso e dos recursos disponíveis para desempenhar uma determinada tarefa.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/ebe36715-6046-4a12-813b-3a897bb97caa)
