[[React]]
[[DOM]]

**O ReactDOM é o responsável por renderizar e atualizar seu código dentro do HTML, exibindo seus elementos React.**

Para entendermos como ele funciona, vamos fazer o seguinte: Criaremos um novo projeto React usando o create-react-app, ou usemos o projeto criado na seção inicial.

Em seguida, vamos abrir o projeto e procurar pelo arquivo index.js. Esse é o arquivo raiz das nossas aplicações React e é nele que fazemos o vínculo dos nossos componentes React com o DOM do navegador, utilizando o ReactDOM.

Com o React, a forma como manipulamos os elementos vai mudar. Inclusive é considerado uma má prática manipular o DOM no React diretamente como no JavaScript puro. Ou seja, não vamos mais utilizar as funções que manipulam o DOM, tais como appendChild, removeChild, querySelector, etc.

Então como fazemos para, por exemplo, mudar o estilo de elementos se não podemos manipular o DOM diretamente?

Resumidamente, no JavaScript puro é possível pegar os elementos via querySelector, por exemplo, e com algum addEventListener escutar um evento, chamar uma função e atribuir ou mudar uma propriedade desse elemento, certo? E no React como funciona?

No React, cada componente pode receber um conjunto de informações (chamadas de props), ou ter informações contidas internamente (chamadas de estado). Toda vez que qualquer uma dessa informações for atualizada, a função ReactDOM.render irá aplicar as mudanças necessárias e o DOM será atualizado automaticamente.