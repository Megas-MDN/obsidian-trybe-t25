[[Node]]
[[Teste Assincrono]]

- [Testar já faz parte da sua rotina](#Testar%0djá%0dfaz%0dparte%0dda%0dsua%0drotina)
- [Tipos de teste](#Tipos%0dde%0dteste)
	- [Testes unitários](#👉%0d**Testes%0dunitários**)
	- [Testes de integração](#👉%0d**Testes%0dde%0dintegração**)
	- [Testes de Ponta-a-ponta](#👉%0d**Testes%0dde%0dPonta-a-ponta**)
- [Testes automatizados](#Testes%0dautomatizados)
	- [Ferramentas](#Ferramentas)
		- [Estruturando testes com o Mocha](#Estruturando%0dtestes%0dcom%0do%0dMocha)
		- [Aferindo testes com o Chai](#Aferindo%0dtestes%0dcom%0do%0dChai)
- [Testes de Integração](#Testes%0dde%0dIntegração)
- [Contratos de APIs](#Contratos%0dde%0dAPIs)
- [Definindo os cenários de teste](#Definindo%0dos%0dcenários%0dde%0dteste)



## Testar já faz parte da sua rotina

Antes de falarmos de testes automatizados e das ferramentas que podemos utilizar para testar nossos códigos em Node.js, vamos pensar sobre algumas das experiências que já tivemos até aqui.

Muitas vezes, realizamos o mesmo teste alterando os dados de entrada _(input)_ para garantir que a saída _(output)_ era condizente com aquilo que foi codificado. Com certeza, muitas vezes o resultado não era o esperado né? Às vezes faltava um `if`, precisava de mais um parâmetro ou até mesmo um retorno não tratado como deveria. Esse processo pode ser chamado de **“testes manuais”**, mas existem diversos tipos de testes, cada um com suas características e objetivos.

> Nos testes manuais, reexecutamos o código algumas vezes, buscando validar se o comportamento do programa está ocorrendo conforme esperado. Além disso, também alteramos os parâmetros de entrada para tentarmos garantir que tal funcionamento se mantenha mesmo com essas variações.

**⏰ Hora da prática**: imagine que queremos criar uma função a qual receba a média das notas de uma pessoa e responda se ela foi aprovada ou não, seguindo a seguinte regra:

![Cenarios](https://content-assets.betrybe.com/prod/Cenarios.png)

Cenários!

O primeiro passo é pensar na estrutura da nossa função. Para isso, podemos fazer as seguintes perguntas:

-   Quantos e quais parâmetros ela vai esperar?
    
-   Qual é o tipo de resposta que ela vai retornar?
    

Nesse caso, nossa função deverá receber **um parâmetro “média”** e responder com **“reprovação” ou “aprovação”**.

Tendo em mente esses questionamentos, podemos partir para a implementação e chegar no seguinte código:

> examples/calculaSituacao.js

```js
function calculaSituacao(media) {
  if (media > 7) {
    return 'aprovação';
  }

  return 'reprovação';
}

module.exports = calculaSituacao;
```

Tendo o código da função implementado, precisamos garantir que seu comportamento é o esperado e que ele não mudará sem aviso - Para isto, devemos testar seus casos de uso e verificar se ela exibe, para cada caso, o comportamento esperado. Algumas das coisas que precisamos garantir são:

-   Se passado um valor **menor que 7**, por exemplo **4**, a resposta deve ser **“reprovação”**;
    
-   Se passado um valor **maior que 7**, por exemplo **9**, a resposta ser **“aprovação”**;
    
-   Não podemos esquecer do “OU”, sendo assim, se passado **7**, a resposta deve ser **“aprovação”**;
    

Para validar esses cenários que pensamos, podemos escrever algumas chamadas na nossa função:

```js
const calculaSituacao = require('./examples/calculaSituacao');

console.log(calculaSituacao(4));
// console: reprovação
```

👉 Se pensarmos nessa forma manual de testar aplicações, precisamos de três cenários de testes distintos:

1️⃣ quando a média for **menor que sete**;

2️⃣ quando a média for **maior que sete**;

3️⃣ quando a média for **igual a sete**.

De olho na dica 👀: podemos programar um script simples com esses testes e adicionar algumas mensagens para nos ajudar a verificar se a resposta dada é aquela que esperamos:



```js
const calculaSituacao = require('./examples/calculaSituacao');

console.log('Quando a média for menor que 7, retorna "reprovação":');

const respostaCenario1 = calculaSituacao(4);
if (respostaCenario1 === 'reprovação') {
  console.log(`Ok 🚀`);
} else {
  console.error('Resposta não esperada 🚨');
}
// console:
// Quando a média for menor que 7, retorna "reprovação":
// Ok 🚀

console.log('Quando a média for maior que 7, retorna "aprovação":');

const respostaCenario2 = calculaSituacao(9);
if (respostaCenario2 === 'aprovação') {
  console.log(`Ok 🚀`);
} else {
  console.error('Resposta não esperada 🚨');
}
// console:
// Quando a média for maior que 7, retorna "aprovação":
// Ok 🚀

console.log('Quando a média for igual a 7, retorna "aprovação":');

const respostaCenario3 = calculaSituacao(7);
if (respostaCenario3 === 'aprovação') {
  console.log(`Ok 🚀`);
} else {
  console.error('Resposta não esperada 🚨');
}
// console:
// Quando a média for igual a 7, retorna "aprovação":
// Resposta não esperada 🚨
```

**Espere, temos um bug aqui!** 🐞

Você observou que um dos casos de teste falhou - fizemos isso propositalmente para simular uma situação normal do dia a dia de uma pessoa programadora. Nesse caso, pode ser um detalhe em uma função simples, mas em sistemas mais complexos, onde temos diversos pontos diferentes interligados e várias pessoas trabalhando no mesmo código, um cenário de falha é ainda maior. Que tal tentar encontrar o erro antes de mostrarmos ele pra você? ;)

> O que poderíamos fazer em uma situação dessas é implementar a correção e chamar as funções novamente, garantindo que dessa vez todos os cenários estão cobertos, inclusive aqueles que já estavam funcionando antes da correção.

Vamos aproveitar para implementar esta correção no código.

> examples/calculaSituacao.js

```js
// function calculaSituacao(media) {
  if (media >= 7) {
//     return 'aprovação';
//   }

//   return 'reprovação';
// }

// module.exports = calculaSituacao;
```

E por fim vamos executar novamente os testes e observar que todos são aprovados.

Para nos ajudar na atividade de teste, existem etapas bem definidas que tem como objetivo garantir que diferentes aspectos do nosso código estão sendo cobertos (testados). Como exemplo, os tipos de teste apresentam diferentes perspectivas sobre o nosso código que devem ser observadas durante o teste.

Bora dar uma olhada nesses tipos de teste? 🤓


# Tipos de teste

Uma questão importante para se ter em mente ao criar cenários de teste é o **escopo** e a **interação** dos testes. Para isso, existem algumas divisões arbitrárias que nos ajudam a pensar em uma ordem de desenvolvimento de testes, as mais comuns são:


### 👉 **Testes unitários**:

Consideram um escopo limitado a um pequeno fragmento do seu código com interação mínima entre recursos externos.

⚠️ Aviso: Para exemplificar esse tipo de teste, vamos imaginar o teste unitário de um carro. 🚗

> O motor precisa ser testado para saber se ele tem potência e torque; já os pneus são testados para saber se têm boa aderência no asfalto. Além disso, testamos o assento do motorista para saber se é confortável e ergonômico e também o volante para saber se é fácil manusear e esterçar.

![Teste de unidades do carro](https://content-assets.betrybe.com/prod/Teste%20de%20unidades%20do%20carro.png)

Teste de unidades do carro.

### 👉 **Testes de integração**:

Presumem a junção de múltiplos escopos (que tecnicamente devem possuir, cada um, seus próprios testes) com interações entre eles.

> Voltando ao exemplo do carro, agora nos testes de integração, ao acelerar testamos se o motor permanece em uma velocidade constante e se, ao esterçar o volante, os pneus dianteiros são orientados corretamente para a direção desejada. Além disso, testamos se, ao se acomodar no assento da pessoa motorista, é fácil manusear o volante e o câmbio.

![Teste de integração do carro](https://content-assets.betrybe.com/prod/Teste%20de%20integra%C3%A7%C3%A3o%20do%20carro.png)

Teste de integração do carro.

### 👉 **Testes de Ponta-a-ponta**: 

Também chamados de Fim-a-fim _(End-to-End; E2E)_, pressupõem um fluxo de interação completo com a aplicação, de uma ponta a outra.

Aqui, poderíamos pensar em uma API que utiliza nossa calculadora - assim como diversas outras funções mais complexas - na hora de realizar uma operação de venda de produtos.

De olho na dica 👀: Esse teste é o mais completo, pois necessita que todos os demais testes tenham sido desenvolvidos.

> Ainda no exemplo do carro, no teste Ponta-a-Ponta (PaP) podemos fazer um test-drive de impacto para avaliar todos os aspectos, realizando, por exemplo, uma corrida com vários carros em um circuito.

![Teste End-to-End do carro](https://content-assets.betrybe.com/prod/Teste%20End-to-End%20do%20carro.png)

Teste End-to-End do carro.

⚠️ Aviso: É importante ressaltar que nenhum tipo de teste é mais importante que o outro, é a combinação entre eles que vai garantir a qualidade do seu código.

Agora que você já conhece os tipos de teste, podemos seguir pensando em formas mais eficientes para executá-los.

> Executar os testes “manualmente” toda vez que uma nova funcionalidade é desenvolvida, é uma tarefa árdua, repetitiva e propensa à erros.

**⏰ Hora da reflexão**: Como pessoas desenvolvedoras, somos capazes de construir soluções para tornar processos mais eficientes e rápidos, sendo menos repetitivos e sujeitos a erros humanos. Com isso, por que não automatizamos esse processo também, colhendo essas e outras vantagens?


# Testes automatizados

Automatizar testes é uma necessidade tão presente no dia a dia dos times de desenvolvimento, que é assunto constante de discussões e evoluções.

Hoje, já é um assunto amplamente difundido sendo possível encontrar diversos tipos, técnicas, implementações e ferramentas diferentes. Essa base sólida sobre o assunto nos ajuda bastante durante o processo de aprendizagem, já que temos diversas ferramentas consolidadas prontas para serem utilizadas.

Vamos conhecer algumas delas?

## Ferramentas

Existem várias ferramentas com o propósito de teste, como o **`Jest`** e o **`assert`**.

O `Jest`, que aprendemos no módulo de Fundamentos, foi originalmente projetado para o React, mas funciona em outros projetos Javascript. Outra característica do `Jest` é que ele é focado principalmente em testes de unidade e na simplicidade e não requer nenhuma configuração, ou seja, após sua instalação, ele está preparado para ser utilizado. Os testes são paralelos e executados em seus próprios processos para maximizar o desempenho. Possui suporte integrado para execução automática de testes a cada alteração no código. Mas não oferece suporte a testes assíncronos.

A nova ferramenta para teste que vamos aprender é o `Mocha`. Ele foi originalmente projetado para o **Node.js**. É focado em vários tipos de testes, como unidade, integração e ponta a ponta (E2E). Diferente do `Jest`, requer outras bibliotecas para funcionar, como o `chai` e o `sinon`. E, apesar de demandar mais trabalho para configurar e adicionar funcionalidades, esta enorme flexibilidade e uma variedade de recursos adicionais prontos para uso, fornecem ferramentas para um desenvolvedor experiente, principalmente em grandes projetos **Node.js**. Além disso o Mocha suporta testes assíncronos e é um framework mais antigo e mais maduro do que o `Jest`, presente em diversos projetos.

Os testes do `Mocha` são executados em série, permitindo relatórios flexíveis e precisos, enquanto mapeia exceções não capturadas para os casos de teste corretos. E para complementar os testes do `Mocha` temos o `chai`, que é uma biblioteca de asserção, e o `sinon`, que implementa dubles de teste, como: _spies_, _stubs_ e _mocks_.

Para utilizarmos essas ferramentas, precisamos começar **fazendo a instalação.**

> Utilizaremos a flag `-D`. Apesar de essenciais durante o desenvolvimento, esses módulos (ferramentas) não serão utilizados para executar a nossa aplicação quando ela for publicada.

Dessa forma, evitamos instalar pacotes desnecessários em nossa versão de produção:

```bash
npm install mocha@8.4.0 chai@4.3.4 --save-dev --save-exact
```

Feita a instalação, já podemos importar o mocha e o chai em um arquivo `.js` e escrever nossos testes.

Bora fazer isso? 💪

## Estruturando testes com o Mocha

O **[mocha](https://mochajs.org/) é um _framework_ de testes para JS**, isso significa que ele nos ajuda a arquitetar os nossos testes fornecendo a estrutura e interface para escrevermos eles.

Vamos começar pelos comportamentos: precisamos definir o que estamos testando em um caso específico. Para isso, o `mocha` nos fornece duas palavras reservadas: o **_describe_** e o **_it_**.

-   O **_describe_**, como o próprio nome já diz, nos permite adicionar uma descrição para um teste específico ou um grupo de testes.
    
-   O **_it_** nos permite sinalizar exatamente o cenário que estamos testando naquele ponto.
    

Nos testes que escrevemos “na mão”, o mocha substitui aqueles logs que utilizamos para descrever cada teste. Bora ver na prática como podemos fazer isso com a ajuda do `mocha`!

No exemplo que utilizamos para criar uma função que recebe a média das notas de uma pessoa, utilizamos o log abaixo para “descrever” nosso cenários de teste.


```js
console.log('Quando a média for maior que 7, retorna "aprovado":');
```

Agora, usando o `describe` podemos definir a seguinte representação para descrever o mesmo cenário:

```js
describe('Quando a média for menor que 7', function () {
  //
});
```

> **Perceba que o `describe` aceita dois parâmetros:**(I) o primeiro é uma string, onde podemos passar a descrição, (II) o segundo é uma função para executar o cenário de teste.
> 
> Outro ponto de atenção é, que não é necessário importar o `mocha` em nosso arquivo, pois suas palavras reservadas serão interpretadas quando executarmos os testes, mas veremos mais adiante como fazê-lo.

De olho na dica 👀: Veja que usamos a sintaxe `function` ao invés de _arrow functions_. Essa sintaxe é uma recomendação da própria documentação do mocha. O uso da _arrow function_ pode restringir o acesso ao contexto de como o mocha trabalha por baixo dos panos. para mais informações acesse esse [link](https://mochajs.org/#arrow-functions) da documentação oficial.

Descrito nosso comportamento, vamos adicionar o que será testado de fato, ou seja, o que é esperado. Para isso, usamos o `it`:

```js
describe('Quando a média for menor que 7', function () {
  it('retorna "reprovação"', function () {
    //
  });
});
```

Anota aí 🖊: A sintaxe do `it` é bem semelhante a do `describe`: ela aceita uma string, que define o comportamento a ser testado, e uma função que executa os testes de fato.

Até agora, nós já vimos como descrever os cenários de teste, mas como verificar se o nosso código está de acordo com esse cenário? 🤔

É o que veremos a seguir!

---

## Aferindo testes com o Chai

O **`chai` nos ajudará com as asserções, ou seja, ele nos fornece maneiras de dizermos o que queremos testar** validando se o resultado condiz com o esperado.

Até aqui, não estamos testando nada de fato, apenas descrevemos o teste.

Anota aí 🖊: Para de fato testar nossa função, precisamos chamá-la passando o input desejado e então validar se a resposta é aquela que esperamos. Essa validação é o que chamamos de _assertion_, **“asserção”** ou, em alguns casos, **“afirmação”**.

Para nos ajudar com essa tarefa, o `chai` nos fornece diversos tipos de validações diferentes.

⚠️ Aviso: Usaremos a interface `expect` do `chai` em nossos exemplos, que significa de fato o que é **esperado** para determinada variável:

```js
const { expect } = require('chai');
const resposta = calculaSituacao(4);

expect(resposta).equals('reprovação');
```

No código acima, estamos chamando nossa função. Logo em seguida, **afirmamos** que seu retorno armazenado na constante `resposta`, deve ser _igual_ (`equals`) a `reprovação`.

Muito mais legível e simples, não é mesmo!?

> Observe que o `chai` foi importado no início do arquivo e o `expect` foi desconstruído a partir dele. Agora, perceba como o `chai` nos fornece uma função pronta, a `equals` que vai comparar se o valor “esperado” na _resposta_ é **igual** ao passado para ele, ou seja, igual a “reprovação”.

De olho na dica 👀: a asserção `equals` é uma das diversas asserções disponíveis no chai. A lista completa pode ser encontrada na [documentação oficial do chai](https://www.chaijs.com/api/bdd/).

Para tornar nosso teste ainda mais legível e elegante, o chai nos fornece outros _getters_ encadeáveis que possuem um papel puramente estético.

Por exemplo, o `to` e o `be`, que nos permitem escrever nossa _assertion_ da seguinte maneira:

> tests/calculaSituacao.js

```js
const { expect } = require('chai');

const calculaSituacao = require('../examples/calculaSituacao');

describe('Quando a média for menor que 7', function () {
  it('retorna "reprovação"', function () {
    const resposta = calculaSituacao(4);

    expect(resposta).to.be.equals('reprovação');
  });
});
```

> Perceba que o `to` e o `be` não alteraram em nada a validação realizada, porém a leitura fica muito mais fluida e natural. É como se estivéssemos dizendo que nosso teste espera a resposta **ser igual** a “reprovação”.

De olho na dica 👀: podemos encontrar um pouco mais sobre esse getters na documentação oficial do _chai_, em [language chains](https://www.chaijs.com/api/bdd/#method_language-chains).

Agora que já vimos um pouco sobre testes automatizados e ferramentas, precisamos pensar sobre qual o melhor momento para estabelecer os cenários e automatiza-los.

**⏰ Hora da reflexão**: em qual momento você deveria começar a pensar nos seus testes? Imagine que seu código é um novo tipo de material desenvolvido para a sustentação de um prédio. Você só iria pensar nos testes após a finalização do prédio? 🤔

É sob esse ponto de vista que iremos conhecer uma nova forma para construir nossas aplicações, priorizando a qualidade do nosso código e melhorando nossa experiência de desenvolvimento.

# Testes de Integração

Como vimos, nos testes manuais há uma espécie de “retrabalho” com a implementação, pois primeiro escrevemos uma primeira versão do código para depois identificar o erro e aí corrigi-lo. Em contrapartida a isso, temos o **`TDD` (Test Driven Development)**, em tradução livre, _Desenvolvimento Orientado a Testes_, cuja ideia principal consiste em começar a escrever os testes, que traduzem e validam os comportamentos esperados para aquele código, antes de iniciar a implementação. Contudo, como no _TDD_ estamos escrevendo testes para códigos que ainda não existem, é completamente normal que um detalhe ou outro possam _“escapulir”_ à mente e que haja a necessidade de fazer algum ajuste nos testes.

A prática do TDD pode ser empregada nos diferentes tipos de teste, por enquanto, iremos focar nos **testes de integração**. Empregando esses testes, em conjunto com a metodologia TDD, iremos construir nosso código de forma mais fácil e com maior garantia de que estamos considerando todos os cenários.

Relembrando🧠: Os testes de integração, ou _integration tests_, servem para verificar se a comunicação entre os componentes de um sistema está ocorrendo da forma esperada. Diferentemente dos testes unitários, onde isolamos as unidades, a ideia aqui é juntar todas elas e ver a mágica acontecer.

> Isso não que dizer que os testes de integração são melhores que os testes unitários. Ambos são importantes, porém, cada um tem um objetivo diferente.

![Testes Unitarios VS Testes de Integracao](https://content-assets.betrybe.com/prod/Testes%20Unitarios%20VS%20Testes%20de%20Integracao.gif)

Testes Unitários VS Testes de Integração

Da mesma forma que definir uma unidade é subjetivo, não existe um nível de granularidade específico de integração para ser testada, sendo possível adaptar esse conceito de acordo com os objetivos de teste desejados. Em outras palavras, isso irá depender do objetivo de teste para definir se uma unidade é composta por apenas uma função, um conjunto de funções relacionadas ou até mesmo um único _endpoint_.

⚠️ Aviso: Nossa integração, por enquanto, partirá do recebimento do objeto da requisição (`request`) em uma API, seguindo por funções incorporadas pelo _endpoint_ até a devolução do objeto de resposta (`response`) dessa requisição.

> Veja que estamos fazendo a integração de poucas unidades até este momento (_endpoint_ e funções). Posteriormente, iremos evoluir um pouco mais essa integração para abordar diferentes quantidades e tipos de unidades.

Você pode estar se perguntando: “Mas onde o TDD entra nessa história?” 👀

> Para melhor exemplificar a prática do TDD com testes de integração, mais adiante, iremos construir uma API empregando esses dois conceitos. Começaremos pela definição dos cenários de teste e à medida que os testes falharem, desenvolveremos funcionalidades necessárias para que o teste seja executado com sucesso. Vamos repetir esse processo até que todos os cenários tenham sido desenvolvidos.


# Contratos de APIs

Sempre que consumimos ou fornecemos um serviço, como por exemplo uma API REST, precisamos ter os comportamentos predefinidos. Esses comportamentos são definidos de acordo com **as regras de entrada e saída de dados da API**.

> Por exemplo: ao chamar um endpoint `GET /users/:userId`, passamos um ID de pessoa usuária e esperamos receber os dados referentes àquele pessoa com um código http `200 - OK`. Caso a pessoa usuária não seja encontrada, esperamos receber um status http `404 - Not Found`, por exemplo.

Perceba que podemos ter diversos padrões definidos e comportamentos esperados. Dessa forma, é importante testar se esses comportamentos estão sendo cumpridos por nossas APIs, retornando uma resposta compatível com o cenário.

Anota aí 🖊: Em uma API, o conceito definido por essas regras é chamado de **contrato**. O contrato define aquilo que foi previamente acordado, ou seja, como a API deverá se comportar em um determinado cenário.

Para ficar ainda mais nítido, vamos utilizar novamente o endpoint `GET /users/:userId`. Podemos dizer que o contrato dele é: **quando a pessoa usuária existe, retornar a seguinte resposta**:

-   Código HTTP: `200 - OK`;
-   Body:

```json
{
  "id": "123",
  "name": "Dwight",
  "fullName": "Dwight Schrute",
  "email": "dwightschrute@dundermifflin.com"
}
```

Esse conceito trabalha muito bem junto com os testes de integração, pois podemos testar se cada contrato está sendo cumprido após o processamento de todas as funções internas de um _endpoint_.


# Definindo os cenários de teste

Para exemplificar como funciona o teste de integração, iremos construir uma nova API chamada Cacau Trybe, uma API que fornece _endpoints_ para gerenciar uma lista de chocolates de diferentes marcas da França 🍫.

Seguindo as premissas do TDD, a primeira questão que devemos nos preocupar são os cenários de teste. Esses cenários, além de validar o nosso código, irão representar os contratos definidos para essa API.

Bora conhecer esses contratos? 📄

A API Cacau Trybe será composta por três _endpoints_, representados pelos seguintes contratos:

👉 **GET** _`/chocolates`_

-   Objetivo: Retornar uma lista com todos os chocolates cadastrados.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):

```json
  [
    { "id": 1, "name": "Mint Intense", "brandId": 1 },
    { "id": 2, "name": "White Coconut", "brandId": 1 },
    { "id": 3, "name": "Mon Chéri", "brandId": 2 },
    { "id": 4, "name": "Mounds", "brandId": 3 }
  ]
```

👉 **GET** _`/chocolates/:id`_

-   Objetivo: Buscar um chocolate específico pelo ID.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):


```json
  [
    {
      "id": 4,
      "name": "Mounds",
      "brandId": 3
    }
  ]
```

👉 **GET** _`/chocolates/brand/:brandId`_

-   Objetivo: Buscar uma lista de chocolates pelo ID (brandId) da marca.
-   Código HTTP: `200 - OK`;
-   Body (exemplo):

```json
[
  {
      "id": 1,
      "name": "Mint Intense",
      "brandId": 1
  },
  {
      "id": 2,
      "name": "White Coconut",
      "brandId": 1
  }
]
```

Com os contratos definidos, é hora de escrever nossos testes.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/4684c963-8015-41ad-a901-eb37076d9ff5/lesson/32ad61bd-476f-4877-826d-a3b127ba89e6)
