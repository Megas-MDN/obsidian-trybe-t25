[[Jest]]

Ao escrever testes, você precisa verificar que valores satisfazem a algumas condições. A função `expect` é utilizada para dar acesso a um conjunto de métodos chamados _matchers_. Esses métodos são estruturas de comparação utilizadas em diversas bibliotecas de testes, inclusive no **Jest**. Podemos pensar neles como uma ponte que dita qual é a relação entre o resultado que temos e o que queremos. O `expect` recebe o valor a ser testado e retorna um objeto representando uma _expectation_. Sobre esse objeto pode-se chamar os _matchers_ que **Jest** fornece.

Vamos passar pelos _matchers_ mais comuns. É importante ressaltar que existem muitos outros _matchers_ que podem ser encontrados na [**documentação oficial**](https://jestjs.io/docs/en/expect) do **Jest**. Aliás, **ler documentação** é uma prática constante no cotidiano de pessoas desenvolvedoras, pois na maior parte das vezes é na documentação que constam as informações atualizadas. Conforme as ferramentas que conhecemos passam a ter mais opções de uso e funcionalidades, com mais frequência recorreremos à documentação aprendendo assim a utilizá-las melhor.

### **toBe**

`toBe` é o matcher mais simples. Esse _matcher_ testa [igualdade estrita](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Equality_comparisons_and_sameness) entre o valor passado para `expect` e seu argumento. Isso significa, por exemplo, que um teste com o _expectation_ abaixo falharia porque a string “5” não é igual ao número 5.
```js
expect(5).toBe("5")
```

### **toEqual**

Para compreendermos a diferença entre `toEqual` e `toBe`, precisamos entender que no **JavaScript** existem duas formas de atribuir valores. A primeira é para a variável, e a segunda é para propriedade do objeto, bem como ao passar argumentos para uma função. Essas formas de atribuição são conhecidas por **valor** e **referência**.

Para nos aprofundarmos nessas duas formas, é importante entender os tipos de dados, que separamos em _tipos primitivos_ (Ex. number, string, boolean, etc) e _objetos_ (Ex. Objetos, Funções, Arrays, etc).

Nos _tipos primitivos_ a atribuição ocorre por **valor**, ou seja, uma cópia do valor original, pois eles são imutáveis. Eles são como gêmeos, uma vez que o primeiro gêmeo corta seu cabelo, o segundo não terá seu cabelo alterado. Por exemplo:
```js
let gemeoUm = "Cabelo comprido";
let gemeoDois = gemeoUm;

gemeoUm = "Careca";

console.log(gemeoUm); // Careca
console.log(gemeoDois); // Cabelo comprido
```

Por outro lado, os _objetos_ tem atribuição por **referência**, ou seja, a cada vez que você cria um novo objeto, cria-se um novo espaço na memória para ele. Eles são mutáveis, portanto podemos considerar que é uma forma de criar um apelido (_alias_) para o original, ou seja, você pode ser chamado pelo seu nome ou por seu apelido, mas você é uma pessoa única, não é possível criar um clone seu. Veja este exemplo:
```js
let myName = { firstName: "Pedro" };
let identity = myName;

myName.firstName = "Carol";

console.log(myName.firstName); // Carol
console.log(identity.firstName); // Carol
```

Isso significa que objetos e arrays com conteúdo iguais são considerados diferentes no **JavaScript**. Para testar a igualdade de objetos e arrays, é preciso usar o _matcher_ `toEqual`, que acessa cada elemento do objeto ou array, fazendo um trabalho de comparação específico e que retorna uma resposta mais voltada para a necessidade dos testes:
```js
test('Igualdade de array e object', () => {
  const arr = [1, 2 ,3];
  const obj = { a: 1, b: 2, c: 3};

  expect(arr).toBe([1, 2, 3]); // fails
  expect(obj).toBe({ a: 1, b: 2, c: 3}); // fails
  expect(arr).toEqual([1, 2, 3]); // OK
  expect(obj).toEqual({ a: 1, b: 2, c: 3}); // OK
});
```

### **Valores booleanos**

Os valores `null`, `undefined` e `false` são do tipo `falsy`. Isso significa que são tratados como `false` sempre que se espera um valor booleano, como em condicionais. Às vezes, porém, é preciso distinguir entre eles. O **Jest** fornece _matchers_ específicos para cada um. Leia mais sobre eles na [documentação do Jest](https://jestjs.io/docs/en/using-matchers#truthiness).

### **Números**

Há também _matchers_ para as principais formas de comparar números. Leia [aqui](https://jestjs.io/docs/pt-BR/using-matchers#n%C3%BAmeros) sobre esses _matchers_

### **Strings**

Para comparar string com expressões regulares, utilize o _matcher_ [_toMatch_](https://jestjs.io/docs/pt-BR/expect#tomatchregexporstring).

### **Arrays**

Você pode verificar se um array contém um item em particular utilizando [_toContain_](https://jestjs.io/docs/pt-BR/expect#tocontainitem). Para verificar que um item possui uma estrutura mais complexa, utilize[_toContainEqual_](https://jestjs.io/docs/pt-BR/expect#tocontainequalitem). O [_toHaveLength_](https://jestjs.io/docs/pt-BR/expect#tohavelengthnumber) permite facilmente verificar o tamanho de um array ou de uma string.

### **Objetos**

É bastante comum testar se um objeto possui uma propriedade específica. O _matcher_ [_toHaveProperty_](https://jestjs.io/docs/pt-BR/expect#tohavepropertykeypath-value) é ideal para esses casos.

### **Exceções**

O _matcher_ [_toThrow_](https://jestjs.io/docs/pt-BR/expect#tothrowerror) será usado para testar se uma função é capaz de lançar um erro quando executada. Por exemplo, se quisermos testar uma função `verificaNumeros('string')` passando uma `string` como parâmetro, o _matcher_ `toThrow` irá testar o erro retornado pela função para verificar se o log de error está correto, por exemplo. Para testar se uma função está retornando um erro, é importante estar atento à sintaxe do `.toThrow`:
```js
const multiplyByTwo = (number) => {
  if (!number) {
    throw new Error('number é indefinido')
  }
  return number * 2;
};
multiplyByTwo(4);

test('testa se multiplyByTwo retorna o resultado da multiplicação', () => {
  expect(multiplyByTwo(4)).toBe(8);
});
test('testa se é lançado um erro quando number é indefinido', () => {
  expect(() => { multiplyByTwo() }).toThrow();
});
test('testa se a mensagem de erro é "number é indefinido"', () => {
  expect(() => { multiplyByTwo() }).toThrowError(new Error('number é indefinido'));
});
```

Note que, para testar se um erro é lançado, passamos uma função para o `expect`. Chamamos `multiplyByTwo` dentro da `arrow function`. Chamar a função diretamente dentro de `expect` fará com que o erro não seja capturado. Assim, a asserção falhará, porque o erro acontecerá antes mesmo de `expect` ser executado e ter a chance de capturar o erro. Para testar a mensagem de erro, como fizemos no terceiro teste do exemplo acima, usamos o _matcher_ `toThrowError` e passamos dentro dos parênteses a mensagem que será mostrada em caso de erro: `new Error("number é indefinido")`. Observe que, nos dois casos, a função que queremos testar é chamada indiretamente por uma `arrow function`. Seguir essa sintaxe é importante para que o seu teste funcione corretamente.

### **not**

`not` permite testar o oposto de algo. Por exemplo, este código testa que domingo é um dia da semana, mas não um dia útil:
```js
const workDays = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'];
const weekDays = ['Sunday', ...workDays, 'Saturday'];

test('Sunday is a week day', () => {
  expect(weekDays).toContain('Sunday');
});

test('Sunday is not a workday', () => {
  expect(workDays).not.toContain('Sunday');
});
```

Existem muitos _matchers_, e você pode até mesmo criar os seus. A [documentação](https://jestjs.io/docs/pt-BR/expect) do **Jest** explica com detalhes todos os _matchers_ disponíveis. Consulte-a sempre!