[[JavaScript]]
[[Operações Assíncronas]]
[[Promise]]
[[Then() e Catch()]]




A declaração **`async function`** define uma _função assíncrona_, que retorna um objeto AsyncFunction.

## Sintaxe##

```js
async function nome([param[, param[, ... param]]]) {
   instruções
}
```

### Nome

O nome da função.

### Param

O nome de um parâmetro a ser passado para a função.

### Instruções

As instruções que compõem o corpo da função.


## Descrição

Quando uma função assíncrona é chamada, ela retorna uma `Promise`. Quando a função assíncrona retorna um valor, a `Promise` será resolvida com o valor retornado. Quando a função assíncrona lança uma exceção ou algum valor, a `Promise` será rejeitada com o valor lançado.

Uma função assíncrona pode conter uma expressão `await`, que pausa a execução da função assíncrona e espera pela resolução da `Promise` passada, e depois retoma a execução da função assíncrona e retorna o valor resolvido.


### Exemplo:

```js
function resolverDepoisDe2Segundos(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function adicionar1(x) {
  var a = resolverDepoisDe2Segundos(20);
  var b = resolverDepoisDe2Segundos(30);
  return x + await a + await b;
}

adicionar1(10).then(v => {
  console.log(v);  // exibe 60 depois de 2 segundos.
});

async function adicionar2(x) {
  var a = await resolverDepoisDe2Segundos(20);
  var b = await resolverDepoisDe2Segundos(30);
  return x + a + b;
}

adicionar2(10).then(v => {
  console.log(v);  // exibe 60 depois de 4 segundos.
});
```


### Reescrevendo uma cadeia de Promise com uma função async

Uma API que retorna uma `Promise` vai resultar em uma cadeia de `Promises` e separa a função em várias partes. Considere o seguinte código:

```js
function pegarDadosProcessados(url) {
  return baixarDados(url) // retorna uma Promise
    .catch(e => {
      return baixarDadosReservas(url) // retorna uma Promise
    })
    .then(v => {
      return processarDadosNoWorker(v); // retorna uma Promise
    });
}
```

pode ser escrita em uma única função `async` desta forma:

```js
async function pegarDadosProcessados(url) {
  let v;
  try {
    v = await baixarDados(url);
  } catch(e) {
    v = await baixarDadosReservas(url);
  }
  return processarDadosNoWorker(v);
}
```

Note que no exemplo acima não tem a instrução `await` na instrução do `return`, porque o valor retornado de uma função `async` é implícitamente passado por um `Promise.resolve.`

###### Fonte: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/async_function#sintaxe
