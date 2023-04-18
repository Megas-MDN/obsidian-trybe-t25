
[[Node]]
[[Operações Assíncronas]]
[[Throw e Try...Catch]]


Agora que você já conhece um pouco sobre Node, vamos relembrar um conceito importante e que precisa estar bem consolidado: **assincronicidade!**

Relembrando🧠: Assim como no front-end, as operações assíncronas são essenciais para as rotinas do back-end. Essas operações permitem que **tarefas independentes** sejam executadas em **segundo plano**, sem que o fluxo de execução aguarde pela finalização dessas tarefas. Essa prática contribui, principalmente, para tarefas que demandam maior tempo de execução.

![Fluxograma node.js para mostrar sua performance](https://content-assets.betrybe.com/prod/2571e2cc-6038-4d92-9b9d-544910e2d7e5-Fluxograma%20node.js%20para%20mostrar%20sua%20performance.png)

Para ilustrar esse cenário, vamos imaginar a operação em um restaurante onde clientes solicitam algo ao Atendente. O Atendente possui as atribuições de _**anotar o pedido**_, _**receber pagamento**_ e repassar para a Pessoa da Cozinha (ambiente assíncrono) _**realizar o pedido**_.

![restaurante-2](https://content-assets.betrybe.com/prod/restaurante-2.png)

Veja que, enquanto o Atendente anota os pedidos, a Pessoa da Cozinha já pode ir preparando os pedidos solicitados anteriormente. Por outro lado, em um cenário síncrono, após receber **um pedido**, o Atendente iria até a cozinha e esperaria até que o pedido solicitado fosse finalizado. Enquanto isso, todos os demais clientes ficariam esperando para solicitar um novo pedido. Já imaginou que confusão? 😨

Sendo assim, para que possamos escrever aplicações com boa performance trazendo uma experiência agradável para a pessoa usuária, é importante sabermos como realizar operações demoradas de forma **assíncrona**. Essa habilidade pode ser, muitas vezes, a diferença entre escrever um código bom e performático e escrever um código que não funciona, ou é extremamente lento.

Existem duas formas principais para implementarmos código assíncrono em JavaScript, usando _**Callbacks**_ e _**Promises**_.

-   As _Callbacks_ fornecem uma interface com a qual você pode dizer: “e quando terminar de fazer isso, faça aquilo”. Podemos entender essa relação fazendo uma analogia ao cenário apresentado anteriormente. Nesse caso, o Atendente poderia pedir a Pessoa da Cozinha que prepara-se um pedido e ao final tocasse um sininho para avisar que o pedido estava pronto. 🔔 🧑‍🍳

Além de evitar uma espera desnecessária, essa operação permite que outras operações bloqueantes também sejam executadas ao mesmo tempo. Ainda sobre o exemplo, se o Atendente solicitasse um pedido para a cozinha e antes do pedido terminar voltasse para entregar um novo pedido, outra Pessoa da Cozinha poderia receber o pedido e iniciar o preparo. Sendo assim, poderíamos ter tantos pedidos realizados ao mesmo tempo quanto o número de Pessoas da Cozinha e recursos disponíveis.

Isso vai permitir um melhor aproveitamento dos recursos da sua máquina! 💪

Apesar das _Callbacks_ tornarem nosso código muito mais eficiente, elas também trazem alguns desafios para legibilidade do nosso código.

> O uso aninhado dessas funções pode dificultar a legibilidade do seu código. Conheça um pouco mais sobre esse problema lendo o material sobre [Callback Hell](http://callbackhell.com/).

Para resolver o problema da chamada Callback Hell, podemos utilizar as [[Promise]]. Elas foram introduzidas ao JavaScript como estratégia para melhorar a legibilidade do código, basicamente uma forma de resolver a “bagunça” que as [[Callback]] causavam. Quando usamos _Promises_, ainda estamos utilizando um tipo de callback, mas que possui uma interface mais legível e intuitiva.

Para entendermos o conceito e/ou objeto de uma Promise, vamos comparar com situações que poderiam ocorrer no exemplo do restaurante, visto anteriormente:

> A Pessoa da Cozinha se compromete a fazer um pedido para o Atendente, ou seja, faz uma promessa. Essa promessa pode ser cumprida e, portanto, **resolvida**, ou algo pode acontecer (acabou o gás 💨) impedindo que a promessa seja cumprida, neste caso ela será **rejeitada**.

Em JavaScript, as Promises funcionam do mesmo jeito: uma promessa/função é criada e, dentro dela, existe um código/ação a ser executado. Se o código é executado sem nenhum problema, a Promise é resolvida por meio da função `resolve`; se algo de errado acontecer durante a execução, a Promise é rejeitada por meio da função `reject`.

Uma promise pode se tornar resolvida com um valor ou rejeitada por algum motivo. Caso um estado de erro ocorra, o método `catch` do Promise é chamado. Esse método, por sua vez, chama o método de tratamento associado ao estado rejected. Caso o `then` ocorra, ele chama o método resolved.

> Exemplo 1: Tratando erros de forma síncrona.

```js
function dividirNumeros(num1, num2) {
  if (num2 == 0) throw new Error("Não pode ser feito uma divisão por zero");

  return num1 / num2;
}

try {
  const resultado = dividirNumeros(2, 1);
  console.log(`resultado: ${resultado}`);
} catch (e) {
  console.log(e.message);
}

```

> Exemplo 2: Tratando erros de forma assíncrona.

```js
function dividirNumeros(num1, num2) {
  const promise = new Promise((resolve, reject) => {
    if (num2 == 0) 
      reject(new Error("Não pode ser feito uma divisão por zero"));

    const resultado = num1 / num2;
    resolve(resultado)
  });

  return promise;
}

dividirNumeros(2, 1)
  .then(result => console.log(`sucesso: ${result}`))
  .catch(err => console.log(`erro: ${err.message}`));

```

> No exemplo 2, note que a função `dividirNumeros` retorna uma Promise, ou seja, ela _promete_ que vai dividir os números. Caso não consiga realizar a divisão, ela **rejeita** essa promessa, utilizando a função `reject`. Caso ocorra tudo certo, ela **resolve** a promessa, utilizando a função `resolve`.

-   As Promises foram introduzidas para resolver o famoso problema do _**Callback Hell**_, mas elas introduziram uma certa complexidade de execução e sintaxe do código. Por esse motivo, em 2017 o JavaScript trouxe uma nova forma para trabalhar com operações assíncronas de forma mais simples: as funções _**async/await**_ .

## Funções [[Async e Await]]

As funções _**async**_ são, basicamente, uma abstração de Promises que facilitam ainda mais a nossa programação com operações assíncronas. Essas funções reduzem cláusulas repetitivas (_**boilerplates**_) em torno de Promises e, consequentemente, evitam a propagação de erros em [promises encadeadas](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Using_promises#encadeamento).

Em outras palavras, elas fazem o código parecer síncrono, mas é assíncrono e não bloqueante nos bastidores. 💚

Uma função `async` retorna uma promise, tal como o exemplo abaixo:

```js
function dividirNumeros(num1, num2) {
  const promise = new Promise((resolve, reject) => {
    if (num2 == 0) 
      reject(new Error("Não pode ser feito uma divisão por zero"));

    const resultado = num1 / num2;
    resolve(resultado)
  });

  return promise;
}
```

Contudo, quando você chama a função `dividirNumeros` com o prefixo `await`, a execução irá esperar até que a Promise seja `resolvida` ou `rejeitada`.

> Precisamos ter bastante atenção aqui 😳! A função que fizer a chamada da Promise `dividirNumeros` (ou qualquer outra função que retorne uma Promise) deve ser definida como `async`, conforme o exemplo a seguir:

```js
const doSomething = async () => {
  console.log(await dividirNumeros(2,2));
};
```

Anota aí 🖊: Toda função na qual utilizamos async, passa automaticamente a retornar uma Promise, que será rejeitada em caso de erro, e resolvida em caso de sucesso.

Como você pode ver no exemplo anterior, nosso código fica muito mais simples e legível. Além disso, os maiores benefícios surgirão quando o código for muito maior e mais complexo.

As funções `async` podem ser encadeadas facilmente e, além disso, seu código será muito mais legível, se comparado ao uso de Promises. Veja o exemplo a seguir:

```js
const promiseParaFazerAlgumaCoisa = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('Eu fiz alguma coisa'), 2000)
  })
}

const assistirAlguemFazendoAlgumaCoisa = async () => {
  const something = await promiseParaFazerAlgumaCoisa()
  return something + '\n e Eu vi você fazendo'
}

const AssistirAlguemAssistindoAlguemFazendoAlgumaCoisa = async () => {
  const something = await assistirAlguemFazendoAlgumaCoisa()
  return something + '\n e Eu também vi você vendo ele fazendo'
}

AssistirAlguemAssistindoAlguemFazendoAlgumaCoisa().then(res => {
  console.log(res)
})
```

> A função `setTimeout()` está sendo utilizada apenas para simular uma operação que irá demorar, neste caso, dois segundos para ser concluída. Se quiser conhecer um pouco mais sobre essa função, veja a [documentação](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout).


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/2b8f0936-7281-49e0-b51e-3bb024b6c5f1)
