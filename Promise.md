[[Fetch API]]
[[JavaScript]]
[[Then() e Catch()]]


Promises é **um objeto em JavaScript que permite a execução de processamentos de forma assíncrona dentro do seu código**, uma vez que é definido como um objeto onde é possível guardar valores que poderão ser usados em outro momento no seu código enquanto você executa outras tarefas. Desse modo, tudo isso será necessário para retratarmos processamentos de sucesso ou falhas dentro do nosso código.

Além disso, é importante sabermos que uma Promise estará em diferentes estados.

## Como funcionam as promises?

Quando estamos programando, nem sempre sabemos definir quais as variáveis ou valores que deverão ser utilizados no código. Dessa forma, surge uma Promise em JavaScript. Logo, são criados métodos que permitem ações assíncronas para gerir os eventos no código. 

A Promise será uma ação executada no futuro do código, podendo assumir vários estados. Ou seja, ela poderá ser resolvida (obter sucesso)  ou retornar algum erro (rejeitada). Dessa maneira, o método `Then`  verificará se houve um caso de erro ou sucesso na execução do código, no qual retornará o método `resolve` quando houver sucesso e `reject` no caso de erros. O fluxo de execução do código se dará da seguinte forma:

![[promise.jpg]]

## Quando e por que utilizar uma promise?

Na estruturação de um código, a criação de funções assíncronas auxiliam no fluxo do código. A exemplo disso, ela pode ser utilizada no momento de processamento de imagens no programa. 

Nesse sentido, manter uma padronização no código também é fundamental para manter a organização, uma vez que em uma implementação que demanda o auxílio de diferentes pessoas a legibilidade torna-se essencial. 

**Sintaxe**

Agora, vamos falar um pouco sobre como funciona a sintaxe na criação de uma Promise. 

Para criar objetos em JavaScripts, chamamos a palavra reservada new, logo, o código ficaria da seguinte maneira

```javascript


 Promise();
```

No entanto, antes de executar essa linha de código, é importante lembrar que é necessário passar os parâmetros do seu objeto para que a execução tenha êxito. No caso, precisamos escrever uma função que seja capaz de resolver ou rejeitar a Promise. 

```javascript


new Promise((resolve: Function, reject: Function) => void)
```

Pronto, agora você já sabe como funciona a sintaxe na criação de uma Promise.

## Quais os 4 principais estados de uma promise?

Agora, vamos falar um pouco sobre os 4 estados de uma Promise

-   **Pending**

Como a própria tradução da palavra, o estado da Promise ainda é pendente. Ou seja, é quando a sua Promise não passou pelo processo de ser fulfilled (sucesso) ou rejected (rejeitada).

-   **fulfilled**

No inglês, também é conhecida como “resolved”, ou seja, é quando nossa Promise foi realizada com sucesso.

-   **rejected**

Nesse estado, a Promise é rejeitada, ou seja, a operação falha.

-   **Settled**

Essa é a etapa final da Promise, uma vez que vemos a conclusão e saberemos se ela foi resolved (realizada) ou rejected (rejeitada).

## **Métodos e Propriedades das promises**

### a) Propriedades

-    Promise.length

A propriedade length é responsável pelo número de argumentos do construtor, o valor sempre será 1.

-   Promise.prototype

Propriedade protótipo responsável pelo método construtor da Promise.

### b) Métodos 

-   Promise.all  

Esse método retornará todas as promisses que estiverem presentes no argumento. Por exemplo, no caso de uma promisse.all(lista), o argumento será responsável por retornar sempre que a Promise for resolvida ou rejeitada. Nesse sentido, se Promise for resolvida, será aplicado um array para mostrar as promises dessa lista.

-   Promise.race  

Esse método retornará o valor de uma Promise ou motivo pelo qual ela está sendo resolvida ou rejeitada. 

-   Promise.reject 

Esse método é responsável por retornar os objetos promises que foram rejeitados e o seu motivo.

-   Promise.resolve  

Esse método é responsável por retornar os objetos do promises que foram resolvidos e o seu valor. Uma curiosidade legal na construção do seu código é que você pode consultar se o valor é uma promise. Para isso, você só precisa utilizar o comando “promise.resolve(valor) para visualizar o valor de uma promise. 

## Criando a primeira Promise: aprenda na prática!

Agora que nós já estudamos um pouco sobre a teoria de uma Promise, que tal começarmos a criar os nossos códigos?

Então, venha conosco e vamos colocar a mão na massa! Para exemplificar, primeiro vamos criar uma função teste para simular:

```javascript

function teste()

}
```

Logo, poderemos criar a nossa Promise e para isso utilizamos a palavra reservada _new_. Então, atenção! É importante lembrar que Promise é um objeto em JavaScript, portanto seguirá a mesma nomenclatura. 

```javascript


new Promise ();
```

Agora, não esqueça! Apenas chamar a função no seu código retornaria um erro, pois precisamos definir os parâmetros que serão responsáveis por resolver (resolve) ou rejeitar (reject) a nossa Promise. Desse modo, o nosso código ficará com essa aparência:

```javascript
function teste() { 

new Promise((resolve, reject) => { 

});

}
```

## Promises javascript: Exemplos práticos!

Agora que a gente já conversou um pouco sobre a estruturação de uma Promise e mostramos como é o funcionamento assíncrono dos fluxos, vamos ilustrar um exemplo de código prático para fixar mais ainda como eles atuam no código.

Imagine o cenário em que você quer resolver (resolve) ou rejeitar (reject) a sua Promise. Aqui criaremos funções de retorno de chamada em que podemos usar o valor para outros fins.

Para que isso ocorra, criaremos as condições responsáveis por resolver ou rejeitar a Promise. Para a criação da função de sucesso, criamos uma string chamada “vermelho” e para a função de falha, criamos uma string que diz “azul” (lembrando que são casos representativos):

```javascript
//caso de sucesso

const promise = new Promise((resolve, reject) =>{

var twoMinutes = 2 * 60 * 1000 // 2mins

setTimeout(()=>{ resolve ("vermelho")}, twoMinutes)

})

//caso de falha

const promise = new Promise((resolve, reject) =>{

var twoMinutes = 2 * 60 * 1000 // 2mins

setTimeout(()=>{ resolve ("azul")}, twoMinutes)

})
```

Nesse momento, a Promise iniciará automaticamente o processamento do argumento para resolvê-lo para o onFullfilled e também trará o argumento de rejeição para o OnFailure.

```javascript
//caso sucesso

const onFulfilled = (result) => {

console.log(result, "proximo passo")

}

//caso falha

const onFailure = (error) => {

console.log(error, "mais uma vez")

}
```

Esses dois casos no retorno da chamada recebem parâmetros que serão retornados quando a Promise for processada.

```javascript
//caso de sucesso

promise.then(onFulfillment)

output> vermelho proximo passo

//caso de falha(onFailure)

output> azul mais uma vez
```

Em outros cenários, poderíamos ter vários modelos de resultados, como uma matriz, um objeto (JSON), ou outros tipos de dados retornados em operações assíncronas.