[[API]]
[[JavaScript]]
[[React]]
[[Then() e Catch()]]

o contexto do Front-end, a maioria dos casos em que você precisa utilizar funções assíncronas ocorrem em requisições.

Um bom exemplo é a função `fetch()` da _Fetch API_!

A _Fetch API_ contém uma série de recursos desenvolvidos para lidar com **requisições http** no JavaScript. A função primária é a `fetch()`, utilizada para fazer chamadas às _URL’s_ das _APIs_. Trata-se de uma função assíncrona, baseada em uma promise.

A função `fetch` pode receber dois parâmetros:

**1 -** _URL_ do serviço alvo da requisição;

**2 -** E, opcionalmente, pode ser passado um objeto contendo algumas informações sobre requisição de API. Esse objeto contém chaves com informações específicas para aquela chamada. Essas especificações estão sempre presentes na documentação de uso daquela API específica. **Não se preocupe muito em como obter essas informações por agora**; nesse início, daremos essas informações para que você se acostume a usar o `fetch()`.

O retorno da chamada varia conforme a _API_ utilizada, não só em conteúdo, mas também em formato. Como nosso maior foco é JavaScript, lidaremos principalmente com respostas em formato JSON ou respostas que possam ser reformatadas para tal.

A função `fetch` é responsável por enviar requisições a _APIs_. Porém essa não é sua única responsabilidade. Ela também possui ferramentas para tratar os dados recebidos e devolvê-los, além de lidar com os erros.

