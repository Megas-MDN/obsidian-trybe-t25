[[Callback]]
[[Promise]]
[[Async e Await]]


É comum em JavaScript executar código de forma assíncrona. Quando você tiver o código que é executado de forma assíncrona, Jest precisa saber quando o código que está testando for concluído, antes que possa passar para outro teste. Jest tem várias maneiras de lidar com isso.

O padrão assíncrono mais comum são as "callbacks".

  
Por exemplo, digamos que você tem uma função `fetchData(callback)` que busca alguns dados e chama `callback(data)` quando está completa. Você deseja testar que este dado retornado seja apenas a string `'peanut butter'`.

Por padrão, testes de Jest completam uma vez que eles chegam ao fim da sua execução. Isso significa que este teste _não_ irá funcionar como o esperado:

```js
// Don't do this!
test('the data is peanut butter', () => {
  function callback(data) {
    expect(data).toBe('peanut butter');
  }

  fetchData(callback);
});
```

O problema é que o teste será concluído logo que `fetchData` completa, antes de sequer chamar a "callback".

Há uma forma alternativa de `test` que corrige isto. Em vez de colocar o teste em uma função com um argumento vazio, use um único argumento chamado `done`. Jest aguardará até que a "callback" `done` é chamada antes de terminar o teste.

```js
test('the data is peanut butter', done => {
  function callback(data) {
    expect(data).toBe('peanut butter');
    done();
  }

  fetchData(callback);
});
```

Se `done()` nunca é chamada, o teste falhará, que é o que você quer que aconteça.

### Promises

Se seu código usa "promises", ou promessas, há uma maneira mais simples para lidar com testes assíncronos. Jest retorna uma promessa de seu teste, e Jest irá aguardar a promessa ser resolvida. Se a promessa for rejeitada, o teste automaticamente irá falhar.

Por exemplo, digamos que `fetchData`, ao invés de usar uma "callback", retorna uma promessa que é esperada ser resolvida na string `'peanut butter'`. Podemos fazer um teste com:

```js
test('the data is peanut butter', () => {
  expect.assertions(1);
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});
```

Certifique-se de retornar a promessa - se você omitir esta instrução `return`, seu teste será concluído antes de completar `fetchData`.

Se você espera que uma promessa seja rejeitada, use o método `catch`. Se certifique de adicionar `expect.assertions` para verificar que um certo número de afirmações são chamadas. Caso contrário, uma promessa cumprida não iria falhar no teste.

```js
test('the fetch fails with an error', () => {
  expect.assertions(1);
  return fetchData().catch(e =>
    expect(e).toMatch('error')
  );
});
```

### `.resolves` / `.rejects` 

Você também pode usar o "matcher" `.resolves` em sua declaração esperada, e Jest irá aguardar a promessa resolver. Se a promessa for rejeitada, o teste automaticamente irá falhar.

```js
test('the data is peanut butter', () => {
  expect.assertions(1);
  return expect(fetchData()).resolves.toBe('peanut butter');
});
```

Não se esqueça de retornar a afirmação — se você omitir esta instrução `return`, seu teste será concluído antes de completar `fetchData`.

Se você espera que uma promessa seja rejeitada, use o "matcher" `.rejects`. Ele funciona analogicamente para o "matcher" `.resolves`. Se a promessa é cumprida, o teste automaticamente irá falhar.

```js
test('the fetch fails with an error', () => {
  expect.assertions(1);
  return expect(fetchData()).rejects.toMatch('error');
});
```

### Async/Await 

Como alternativa, você pode usar `async` e `await` em seus testes. Para escrever um teste async, basta usar a palavra-chave `async` na frente da função passada para `test`. Por exemplo, o mesmo cenário de `fetchData` pode ser testado com:

```js
test('the data is peanut butter', async () => {
  expect.assertions(1);
  const data = await fetchData();
  expect(data).toBe('peanut butter');
});

test('the fetch fails with an error', async () => {
  expect.assertions(1);
  try {
    await fetchData();
  } catch (e) {
    expect(e).toMatch('error');
  }
});
```

É claro que você pode combinar `async` e `await` com `.resolves` ou `.rejects` 

```js
test('the data is peanut butter', async () => {
  expect.assertions(1);
  await expect(fetchData()).resolves.toBe('peanut butter');
});

test('the fetch fails with an error', async () => {
  expect.assertions(1);
  await expect(fetchData()).rejects.toMatch('error');
});
```

Nestes casos, `async` e `await` são efetivamente apenas uma sintaxe mais simples da mesma lógica dos exemplos de uso de promessas.

Nenhuma dessas formas é particularmente superior às outras, e você pode misturar e combiná-las através de uma base de código, ou até mesmo em um único arquivo. Apenas vai depender de qual estilo torna os testes mais simples.

###### Fonte: https://deltice.github.io/jest/docs/pt-BR/asynchronous.html#content
