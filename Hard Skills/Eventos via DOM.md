[[DOM]]
[[JavaScript]]

Uma das funcionalidades mais poderosas do _JavaScript_ é a capacidade de _“reagir”_ a eventos que acontecem em uma página web.

Praticamente qualquer interação da pessoa usuária com a página pode ser considerada um evento: o _rolar da tela_, o _passar do mouse_ por um elemento, o _click do mouse_, o _digitar do teclado_, entre outros.

Você vai aprender a criar um tipo específico de código, chamado _escutador de eventos_, ou _event listener_, em inglês.

Ele tem esse nome porque é um código colocado em um elemento que tem uma única razão de ser: ficar ali esperando que um evento específico ocorra (um click, por exemplo) e, quando isso acontecer, executar uma função pré-determinada pela pessoa programadora.

Você viu que pode usar o `onload`, que é um event listener que vem no objeto `window` do browser, e viu também que pode utilizar o _atributo_ `onclick` para esperar por eventos de clique em um elemento.

No entanto, utilizar _atributos HTML_ de escutadores de eventos não é uma prática recomendada, por alguns motivos. Um deles é que o ideal é não misturar o seu código HTML com o código JavaScript. Outro motivo é que, se você precisar adicionar events listeners em muitos elementos, ou mesmo precisar mudar qual função é adicionada como resposta a esses eventos nesses elementos depois, fica complicado ter de adicionar manualmente a propriedade em cada um dos elementos. Por essas razões, utilizar eventos _inline_ (como são chamados eventos adicionados diretamente no HTML) é considerado uma má prática.

Mas, então, como utilizar um evento de clique em um elemento? Bem, é para essas e outras coisas que utilizamos o `addEventListener`, que você verá a seguir. 😉

# Conheça o addEventListener

O código mais comum para criar um escutador de eventos em um elemento é através de uma função nativa do _JavaScript_, chamada `addEventListener`. Funções nativas são funções que já existem prontas dentro da linguagem e, como toda função, podem receber parâmetros.

No seu uso mais comum, `addEventListener` recebe dois parâmetros:

1.  O evento que estamos esperando escutar: Exemplos: `click`, `change`, `mouseover` etc.;
2.  A função (criada por você) que será executada quando o evento acontecer.

A seguir, você vai aprender a utilizar essa função:

Para conhecer mais eventos, acesse [este link](https://www.w3schools.com/jsref/dom_obj_event.asp), no qual são listados vários eventos diferentes para você utilizar. Os mais comuns são: `click`, `change`, `mouseover` e `keyup`.

Outra coisa que vale a pena se lembrar sempre é que **todos os elementos** podem receber eventos. Tudo depende apenas de sua necessidade. Você pode usar eventos em caixas de texto, botões e até mesmo elementos estáticos, como `div` e `p`.

Agora que você já tem entendimento sobre o funcionamento de alguns eventos, acesse [este link](https://codepen.io/johnatas-henrique/pen/jOEQQvZ) e veja um exemplo interativo. Nele você verá a diferença entre o evento `change` e o evento `keyup`.

Para finalizar o conteúdo do dia, que tal alguns exercícios para treinarmos o que você acabou de aprender?! Mas, antes disso, uma dica importante:

-   **Você pode colocar quantos _event listeners_ quiser em um mesmo _elemento_;**
-   **O navegador passa para a função chamada no addEventListener _o evento_ como um _parâmetro_, podendo ser acessado pela função. Veja mais sobre o assunto [aqui](https://developer.mozilla.org/pt-BR/docs/Web/API/Event), especialmente a parte sobre event.target**

Para os exercícios, copie os códigos HTML, CSS e JS abaixo e salve-os todos no mesmo diretório, com os nomes `index.html`, `style.css` e `main.js`, respectivamente.

Faça o que se pede no arquivo `main.js`. Você não precisará alterar os arquivos HTML e CSS. Para facilitar, os seletores já foram dados no início do arquivo `main.js`.

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
  <meta charset="UTF-8">
  <title>addEventListener</title>
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;900&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <header> 
      <h1>Spotrybefy</h1>
    </header>
    <main>
      <h3 id="my-spotrybefy">Meu top 3 do Spotrybefy</h3>
      <ul class="container">
        <li class="tech" id="first-li">Aqui está a primeira tecnologia que mais gostei.</li>
        <li id="second-li">Aqui está a segunda tecnologia que mais gostei.</li>
        <li id="third-li">Aqui está a terceira tecnologia que mais gostei.</li>
      </ul>
      <input type="text" id="input" placeholder="Alterar a primeira tecnologia">      
    </main>
    <script src="main.js"></script>
  </body>
</html>
```

Lembrando que você pode alterar o arquivo `style.css` como quiser, deixando o exercício com a sua cara!

```css
body {
  align-items: center;
  background-color: #333;
  color: white;
  display: flex;
  flex-flow: column wrap;
  font-family: Montserrat, sans-serif;
  height: 100vh;
  justify-content: center;
  margin: 0;
  padding: 0;
  width: 100vw;
}

.container {
  display: flex;
  flex-flow: row wrap;
}

.container li {
  align-items: center;
  display: flex;
  flex-flow: column wrap;
  height: 200px;
  justify-content: center;
  margin: 2px;
  padding: 15px;
  text-align: center;
  transition: all 0.25s ease;
  width: 200px;
}

h1 {
  font-size: 48px;
  color: #2fc18c;
}

.container li:nth-of-type(1) {
  background-color: #2fc18c;
  color: #333;
}

.container li:nth-of-type(2) {
  background-color: #006dfb;
}

.container li:nth-of-type(3) {
  background-color: #41197f;
}

input {
  border: 1px solid #333;
  margin: 10px 0;
  padding: 5px;
  text-align: center;
  width: 200px;
}

input:hover {
  border: 1px solid #2fc18c;
}

input:focus {
  border: 1px solid #006dfb;
  outline: 2px solid #006dfb;
}

.tech {
  transform: translateY(-20px);
}
```

E agora, nosso código JavaScript, com as instruções e um exemplo prático do `event.target`.

```jsx
const firstLi = document.getElementById('first-li');
const secondLi = document.getElementById('second-li');
const thirdLi = document.getElementById('third-li');
const input = document.getElementById('input');
const myWebpage = document.getElementById('my-spotrybefy');


// - Copie esse arquivo e edite apenas ele;
//  - Note que uma das caixas está um pouco acima das outras. Por que isso ocorre?

// - Crie uma função que adicione a classe 'tech' ao elemento `li` quando for clicado.
//  - Deve existir apenas um elemento com a classe 'tech'. Como você faz isso?

// - Crie uma função que, ao digitar na caixa de texto, altere o texto do elemento
// com a classe 'tech';

// - Crie uma função que, ao clicar duas vezes em 'Meu top 3 do Spotrybefy', ele
// redirecione para alguma página;
//  - Que tal redirecionar para seu portfólio?

// - Crie uma função que, ao passar o mouse sobre 'Meu top 3 do Spotrybefy', altere
// a cor do mesmo;

// Segue abaixo um exemplo do uso de event.target:


function resetText(event) {
  // O Event é passado como um parâmetro para a função.
  event.target.innerText = 'Opção reiniciada';
  // O event possui várias propriedades, porém a mais usada é o event.target,
  // que retorna o objeto que disparou o evento.
}

firstLi.addEventListener('dblclick', resetText);

// Não precisa passar o parâmetro dentro da callback resetText. O próprio
// navegador fará esse trabalho por você, não é legal? Desse jeito, o
// event.target na nossa função retornará o objeto 'firstLi'.
```

#### **Solução**

```jsx
const firstLi = document.getElementById('first-li');
const secondLi = document.getElementById('second-li');
const thirdLi = document.getElementById('third-li');
const input = document.getElementById('input');
const myWebpage = document.getElementById('my-spotrybefy');

// 1. Copie esse arquivo e edite apenas ele;
// 1.1. Antes de começar os exercícios, use o LiveServer para dar uma olhada em como está a página no navegador.
// 1.2. Note que uma das caixas está um pouco acima das outras. Por que isso ocorre?

// 2. Crie uma função que adicione a classe 'tech' ao elemento `li` quando for clicado.
// 2.1. Deve existir apenas um elemento com a classe 'tech'. Como você faz isso?
function handleChangeTech(event) {
  const techElement = document.querySelector('.tech');
  techElement.classList.remove('tech');
  event.target.classList.add('tech');
  input.value = '';
}

firstLi.addEventListener('click', handleChangeTech);
secondLi.addEventListener('click', handleChangeTech);
thirdLi.addEventListener('click', handleChangeTech);


// 3. Crie uma função que, ao digitar na caixa de texto, altere o texto do elemento
// com a classe 'tech';
input.addEventListener('input', function(event) {
  const techElement = document.querySelector('.tech');
  techElement.innerText = event.target.value;
});

// 4. Crie uma função que, ao clicar duas vezes em 'Meu top 3 do Spotrybefy', ele
// redirecione para alguma página;
// 4.1. Que tal redirecionar para seu portifólio?
myWebpage.addEventListener('dblclick', function() {
  window.location.replace('https://blog.betrybe.com/');
});

// 5. Crie uma função que, ao passar o mouse sobre 'Meu top 3 do Spotrybefy', altere
// a cor do mesmo;

myWebpage.addEventListener('mouseover', function(event) {
  event.target.style.color = 'red';
});

myWebpage.addEventListener('mouseout', function(event) {
  event.target.style.color = 'unset';
});
```

Não se preocupe se cada fragmento dessa resolução não estiver totalmente claro, pois iremos passar por uma explicação mais detalhada.

```js
const firstLi = document.getElementById('first-li');
const secondLi = document.getElementById('second-li');
const thirdLi = document.getElementById('third-li');
const input = document.getElementById('input');
const myWebpage = document.getElementById('my-spotrybefy');
```

Essa primeira parte se dedica a uma boa prática de colocar nomes que irão se repetir muito em variáveis. Além disso, evita que algumas linhas de código que veremos futuramente fiquem muito extensas.

Também podemos observar que, com essas constantes, nós temos poder de acesso e edição sobre essas Li’s e Inputs.

```js
function handleChangeTech(event) {
  const techElement = document.querySelector('.tech');
  techElement.classList.remove('tech');
  event.target.classList.add('tech');
  input.value = '';
}

firstLi.addEventListener('click', handleChangeTech);
secondLi.addEventListener('click', handleChangeTech);
thirdLi.addEventListener('click', handleChangeTech);
```

A seção acima atribui uma função ao evento de clique nas nossas Li’s. Essa função, primeiramente recebe o “event” como parâmetro, que é um objeto que contém informações sobre o evento que foi disparado no momento. Dentro dele existe a chave “target”, que é uma referência ao elemento que deu início ao evento.

Na primeira linha dentro da função, atribuímos o elemento com a classe “tech” a uma variável e, na linha seguinte, removemos essa classe do elemento. E, após isso, atribuímos essa classe ao “event.target”, que é a propriedade que discutimos no parágrafo anterior. Por fim, limpamos nosso input, inserindo uma string vazia em seu campo de texto.

Resumindo, tiramos a classe “tech” da Div que possuir ela, inserimos essa mesma classe na Li em que a gente clicou e aí limpamos nosso input.

Isso funciona como se estivéssemos selecionando a Li em que queremos escrever o título da música.

```js
input.addEventListener('input', function(event) {
  const techElement = document.querySelector('.tech');
  techElement.innerText = event.target.value;
});

myWebpage.addEventListener('dblclick', function() {
  window.location.replace('https://blog.betrybe.com/');
});

```

Vimos no bloco de código anterior que primeiro criamos uma função e depois chamamos seu nome no segundo parâmetro do “addEventListener”. Mas é possível criarmos uma função diretamente nesse campo, inclusive isso foi feito nessas duas funções. Percebe que elas não têm um nome? Isso é permitido, e o nome desse recurso é “função anônima”. Mais adiante no curso você aprenderá outras formas de criar funções como essa.

A primeira função adiciona um evento “input” na nossa caixa de texto. Isso vai disparar uma função que irá adicionar o valor do input na Li que atualmente está com a classe “tech”.

Pedimos uma atenção ao nome do evento da segunda função, que é “dblclick”, que significa que a função apenas será acionada quando houver dois cliques em sequência. E a ação disparada é pegar a URL atual com `window.location` e substituir por outro link usando `.replace('https://blog.betrybe.com/')`.

```js
myWebpage.addEventListener('mouseover', function(event) {
  event.target.style.color = 'red';
});

myWebpage.addEventListener('mouseout', function(event) {
  event.target.style.color = 'unset';
});
```

Agora temos mais duas funções: a primeira faz com que o texto do elemento fique com a fonte vermelha quando o mouse passar por ele, e a segunda adiciona o valor “unset” para a cor da fonte. Isso significa que esse estilo irá “resetar” a cor do elemento quando o mouse sair dele.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/353d541f-9b31-4a51-bdc1-37b126ded6c7/lesson/4617d0d3-b461-4898-af7c-0f37c4b567cd)
