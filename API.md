[[JavaScript]]
[[React]]
[[Operações Assíncronas]]
[[Fetch API]]


## Application Programming Interface (API)
  
Uma **_API_** permite que aplicações se comuniquem umas com as outras, servindo de “ponte” para elas. Ela não é um banco de dados ou um servidor, mas a responsável pelo controle dos pontos de acesso a eles, por meio de um conjunto de rotinas e padrões de programação.
No momento, vamos focar em APIs baseadas na web, como esta vista no modelo abaixo. Essas APIs retornam dados em **_response_** (resposta) a um **_request_** (requisição) do cliente, nos permitindo acesso a dados de fontes externas.

![[api.webp]]
> Imagem que demonstra o funcionamento de uma API no contexto da web.

APIs também nos permitem compartilhar dados com outros sites ou aplicações. Você já deve ter observado a opção de “Compartilhar no Facebook” ou “Compartilhar no Twitter”. No momento em que você clica nessa opção, a aplicação que você está visitando se comunica com sua conta do Twitter ou Facebook e altera os dados do seu status, por exemplo, através de uma API.

#### Por que precisamos de APIs?

Imagine a seguinte situação: você está trabalhando em um blog e gostaria de exibir para os visitantes os tweets que fazem referência a ele.

Uma estratégia seria contatar o Twitter e solicitar os tweets por e-mail. Entretanto, esse processo seria extremamente manual e o número de solicitações muito alto. Não teríamos também nossos dados atualizados em tempo real.

Por esse motivo, o Twitter cria uma forma de fazermos consultas a esses dados através de uma API. Ela vai controlar quais dados podemos requisitar, preparar nosso pedido no servidor e nos enviar uma resposta.

#### Quem precisa criar e manter APIs?

APIs públicas e baseadas na web são desenvolvidas e aprimoradas constantemente por grandes empresas de tecnologia (principalmente de mídias sociais), organizações governamentais, startups de software ou qualquer outra empresa ou pessoa que colete dados e precise disponibilizá-los de algum modo.

#### Como uma API se diferencia de um back-end padrão de um site?
> Toda API é um back-end, mas nem todo back-end é uma API.


Um back-end padrão de um site retorna templates (um arquivo HTML pronto, por exemplo) para o front-end de uma única aplicação, através de rotas definidas. Por exemplo, quando você acessa uma página da nossa plataforma, está fazendo um **_request_** ao servidor, que te retorna um template como **_response_**.

As APIs também possuem rotas de acesso que permitem a comunicação com o servidor, mas não precisam retornar templates. Geralmente, retornam dados no formato **_JSON_**.

#### Como utilizar APIs na minha aplicação?

APIs podem incrementar as funcionalidades da sua aplicação e colocá-la em um outro patamar. Você pode adicionar mapas, receber dados sobre o tempo e outras informações úteis.

Para utilizá-las siga as boas práticas a seguir:

-   Encontre uma API pública que seja bem documentada e mantida;
-   Leia a documentação para ter certeza de que aquela API resolve o problema que você deseja solucionar;
-   Entenda o formato dos dados disponíveis;
-   Faça _requests_ e receba _responses_ da API com os dados que você deseja receber.

#### Fazendo uma requisição a uma API

Você pode fazer requisições a uma API de várias formas. Uma delas é no terminal.

No exemplo a seguir, vamos fazer um **_request_** para uma **_API_** que retorna um **_JSON_** como **_response_**.

```js
wget 'https://pokeapi.co/api/v2/pokemon/ditto' -O - -q
```

### Promises
O foco nesta seção é o consumo de APIs utilizando o `fetch` e, por esse motivo, vamos explicar de forma básica o conceito de _Promise_, já que o retorno de um `fetch` é uma Promise.

As promises se comportam de forma muito parecida com as funções que já conhecemos, mas existem três pontos de destaque das Promises em relação a outras funções:

1.  As Promises são **_assíncronas_**, ou seja, elas têm um espaço especial para sua execução sem que travem o fluxo de outras funções;
    
2.  As Promises têm “superpoderes”, isto é, funções extras que facilitam o controle do fluxo assíncrono;
    
3.  As Promises são construídas de uma forma distinta: para criar uma nova Promise, usamos um **_Construtor_**.
    

Como não vamos nos aprofundar em Promises neste momento, não vamos detalhar o processo de construção de Promises. Mas tenha tranquilidade, você irá ver como fazer isso no módulo de Back-end, onde é mais utilizado.

Outro ponto importante é que as Promises possuem três estados:

-   _Pending_ (pendente): estado inicial. Significa que ela está em execução;
-   _Fulfilled_ (resolvida): estado de sucesso. Significa que tudo deu certo e foi retornado o valor de sucesso;
-   _Rejected_ (rejeitada): estado de rejeição. Significa que algo deu errado e foi retornado o erro que gerou essa rejeição.

Então, quando você se deparar com um `Promise { <[estado]> }` em um `console.log()`, pode significar que você tentou acessar o valor de uma Promise antes de ela ter finalizado sua execução.

E o que você precisa saber sobre Promise para usar o `fetch`?

Quando utilizamos o `fetch` recebemos uma Promise, o que significa que temos uma “promessa” de que aquilo vai retornar algo para você. No caso do `fetch`, temos dois possíveis retornos: em caso de sucesso, recebemos a _response_ (que também é uma Promise e contém o dado final que queremos acessar), e caso algo dê errado com a nossa requisição, recebemos as informações sobre o erro. Mas toda promessa é assíncrona e, para termos o retorno dela, devemos esperar um tempo até essa promessa ser resolvida. Então, como fazemos isso?

Para resolver esse problema temos duas opções: `.then() .catch()` e `async/await` com `try/catch`. Esses métodos vão garantir que o código que estamos desenvolvendo aguarde o retorno de uma Promise antes de executar os próximos passos.