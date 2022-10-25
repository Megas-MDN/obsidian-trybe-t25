[[Jest]]
[[Testes com Jest]]

## afterAll(fn, timeout)

Executa uma função depois que todos os testes neste arquivo forem concluídos. Se a função retorna uma promise ou é um generator, Jest aguarda essa promise resolver antes de continuar.

Opcionalmente, você pode fornecer um `timeout` (em milissegundos) para especificar quanto tempo esperar antes de abortar. The default timeout is 5 seconds.

Por exemplo:

Por exemplo:

```js
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterAll(() => {
  cleanUpDatabase(globalDatabase);
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

Se `afterAll` está dentro de um bloco `describe`, ele é executado ao final do bloco "describe".

Se você deseja executar uma limpeza após cada teste em vez de após todos os testes, use ao invés `afterEach`.

Se você deseja executar uma limpeza após cada teste em vez de após todos os testes, use ao invés `afterEach`.

## afterEach(fn, timeout)

Executa uma função após cada um dos testes deste arquivo completar. Se a função retorna uma promise ou é um generator, Jest aguarda essa promise resolver antes de continuar.

Opcionalmente, você pode fornecer um `timeout` (em milissegundos) para especificar quanto tempo esperar antes de abortar. The default timeout is 5 seconds.

Por exemplo:
```js
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterEach(() => {
  cleanUpDatabase(globalDatabase);
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

Se `afterEach` está dentro de um bloco `describe`, ele é executado somente após os testes que estão dentro deste bloco "describe".

Se você deseja executar uma limpeza apenas uma vez, depois que todos os testes são executados, use `afterAll`.

Se você deseja executar uma limpeza apenas uma vez, depois que todos os testes são executados, use `afterAll`.

## beforeAll(fn, timeout)

Executa uma função antes de qualquer um dos testes neste arquivo ser executado. Se a função retornar uma promise ou for um generator, o Jest vai esperar até que ela esteja resolvida para executar os testes.

Opcionalmente, você pode fornecer um `timeout` (em milissegundos) para especificar quanto tempo esperar antes de abortar. The default timeout is 5 seconds.

Por exemplo:
```js
const globalDatabase = makeGlobalDatabase();

beforeAll(() => {
  // Limpa o banco de dados e adiciona alguns dados de teste.
  // O Jest aguardará que essa promessa seja resolvida antes de executar os testes.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

  // Jest irá esperar que essa promessa seja resolvida antes de executar testes.
  // Como configuramos o banco de dados apenas uma vez neste exemplo, é importante
//que nossos testes não o modifiquem.
test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});
```

Aqui `beforeAll` garante que o banco de dados está configurado antes dos testes serem executados. Se a configuração for síncrona, você pode fazer tudo sem precisar usar o `beforeAll`. A chave é que Jest esperará por uma promessa resolver, para que você possa ter configuração assíncrona também.

Se você deseja executar algo antes de cada teste, em vez de antes que qualquer teste seja executado, use `beforeEach`.

Se você deseja executar algo antes de cada teste, em vez de antes que qualquer teste seja executado, use `beforeEach`.

## beforeEach(fn, timeout)

Executa uma função antes que cada um dos testes neste arquivo seja executado. Se a função retornar uma promise ou for um generator, o Jest vai esperar até que ela esteja resolvida para executar os testes.

Opcionalmente, você pode fornecer um `timeout` (em milissegundos) para especificar quanto tempo esperar antes de abortar. The default timeout is 5 seconds.

Por exemplo:
```js
const globalDatabase = makeGlobalDatabase();

beforeEach(() => {
  // Clears the database and adds some testing data.
  // Jest irá esperar que essa promessa seja resolvida antes de executar testes.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

// Since we only set up the database once in this example, it's important
// that our tests don't modify it. test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});
```

Se `beforeEach` está dentro de um bloco `describe`, ele é executado para cada teste no bloco "describe".

Se você só precisa executar algum código de configuração uma vez, antes que qualquer teste execute, use ao invés `beforeAll`.

Se você só precisa executar algum código de configuração uma vez, antes que qualquer teste execute, use ao invés `beforeAll`.

###### Fonte: https://jestjs.io/pt-BR/docs/api#describename-fn 