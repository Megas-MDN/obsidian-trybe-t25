[[Mongo DB]]

## Operador $all

O operador `$all` seleciona todos os documentos em que o valor do campo é um _array_ que contenha todos os elementos especificados. Se compararmos aos operadores que já conhecemos, esse operador é equivalente ao operador `$and`, pois fará a comparação de todos os valores especificados, porém, para _arrays_.

Utiliza-se `$all` sempre que é preciso passar mais de um valor de comparação, e é irrelevante para a verificação tanto a existência de mais elementos no _array_ quanto a ordem em que esses elementos estão.

Entenda essa diferença com estas duas _queries_:

```js
db.inventory.find({ tags: ["red", "blank"] });

db.inventory.find({ tags: { $all: ["red", "blank"] } });
```

A primeira _query_ retornará somente os documentos em que o _array_ `tags` seja **exatamente** igual ao passado como parâmetro no filtro, ou seja, contenha apenas esses dois elementos, na mesma ordem.

Já a segunda analisará o mesmo _array_, **independentemente** da existência de outros valores ou a ordem em que os elementos estejam.

Utilizar o `$all` poupa um pouco de código. Veja um exemplo utilizando o `$all`:

```js
db.inventory.find(
  { tags: { $all: [ "ssl", "security" ] } }
);
```

E seu equivalente, utilizando o `$and`:

```js
db.inventory.find(
  {
    $and: [
      { tags: "ssl" },
      { tags: "security" }
    ]
  }
);
```


## Operador $elemMatch

O operador `$elemMatch` seleciona os documentos que contêm um campo do tipo _array_ com pelo menos **um** elemento que satisfaça **todos** os critérios de seleção especificados. Ou seja, com esse operador você pode especificar várias _queries_ para um mesmo _array_.

Veja um exemplo considerando a coleção `scores` com os seguintes documentos:

```js
{ _id: 1, results: [82, 85, 88] },
{ _id: 2, results: [75, 88, 89] }
```

A _query_ abaixo seleciona somente os documentos em que o _array_ `results` contém **ao menos um elemento** que seja **maior ou igual a 80** e **menor que 85**:

```js
db.scores.find(
  { results: { $elemMatch: { $gte: 80, $lt: 85 } } }
);
```

Como resultado, apenas o documento com o `_id` igual a `1` será retornado, já que o 82 satisfaz as duas verificações.

Você pode utilizar o operador `$elemMatch` em _arrays_ que contenham subdocumentos e especificar vários campos desses subdocumentos como filtro. Veja os seguintes documentos na coleção `survey`:

```js
{
  _id: 1,
  results: [
    { product: "abc", score: 10 },
    { product: "xyz", score: 5 }
  ]
},
{
  _id: 2,
  results: [
    { product: "abc", score: 8 },
    { product: "xyz", score: 7 }
  ]
},
{
  _id: 3,
  results: [
    { product: "abc", score: 7 },
    { product: "xyz", score: 8 }
  ]
}
```

A _query_ abaixo selecionará apenas os documentos em que o _array_ `results` contenha ao menos um elemento subdocumento com o campo `product` igual a `xyz` **e** o campo `score` maior ou igual a `8`:

```js
db.survey.find(
  { results: { $elemMatch: { product: "xyz", score: { $gte: 8 } } } }
);
```

Será retornado apenas o documento com o `_id` igual a `3`.

Você não precisa utilizar o operador `$elemMatch` se estiver utilizando uma condição para apenas “um” campo do documento _embedado_. Veja:

```js
db.survey.find(
  { results: { $elemMatch: { product: "xyz" } } }
);
```

Como a operação acima só tem uma condição, o operador `$elemMatch` não se faz necessário e você pode utilizar a _query_ abaixo:

```js
db.survey.find(
  { "results.product": "xyz" }
);
```


## Operador $size

O operador `$size` seleciona documentos em que um _array_ contenha um **número de elementos** especificado.

Considere a coleção `products` a seguir, contendo documentos em que o campo `tags` pode ser um _array_:

```js
{ _id: 1, tags: ["red", "green"] },
{ _id: 2, tags: ["apple", "lime"] },
{ _id: 3, tags: "fruit" },
{ _id: 4, tags: ["orange", "lemon", "grapefruit"] }
```

Ao executar a _query_ abaixo, apenas os documentos com o `_id` igual `1` e `2` serão retornados, pois seus campos `tags` são _arrays_ e contêm exatamente **2 elementos**:

```js
db.products.find(
  { tags: { $size: 2 } }
);
```

**IMPORTANTE:** o operador `$size` aceita apenas valores numéricos, ou seja, ele verifica se um _array_ possui exatamente um certo número de elementos. Por isso, não é possível utilizá-lo, por exemplo, para trazer _arrays_ com comprimento maior do que 2 ($gt: 2). Se você precisar selecionar documentos com base em valores diferentes, a solução é criar um campo que se incremente quando elementos forem adicionados ao _array_.


## Operador $expr

O operador `$expr` permite que você utilize [expressões de agregação](https://docs.mongodb.com/manual/meta/aggregation-quick-reference/#aggregation-expressions) e construa _queries_ que comparem campos no mesmo documento.

Considere os documentos abaixo na coleção `monthlyBudget`:

```js
{ _id: 1, category: "food", budget: 400, spent: 450 },
{ _id: 2, category: "drinks", budget: 100, spent: 150 },
{ _id: 3, category: "clothes", budget: 100, spent: 50 },
{ _id: 4, category: "misc", budget: 500, spent: 300 },
{ _id: 5, category: "travel", budget: 200, spent: 650 }
```

A _query_ abaixo utiliza o operador `$expr` para buscar os documentos em que o valor de `spent` exceda o valor de `budget`:

```js
db.monthlyBudget.find(
  {
    $expr: { $gt: [ "$spent", "$budget" ] }
  }
);
```

Apenas os seguintes documentos serão retornados:

```js
{ "_id" : 1, "category" : "food", "budget" : 400, "spent" : 450 }
{ "_id" : 2, "category" : "drinks", "budget" : 100, "spent" : 150 }
{ "_id" : 5, "category" : "travel", "budget" : 200, "spent" : 650 }
```

Note que, na _query_, nenhum valor foi especificado explicitamente. O que acontece é que o operador `$expr` entende que deve comparar os valores dos dois campos. Por isso o `$` é utilizado, indicando que a _string_ entre aspas referencia um campo.


## Operador $regex

O operador `$regex` fornece os “poderes” das **expressões regulares** (_regular expressions_) para seleção de _strings_. **MongoDB** utiliza expressões regulares compatíveis com [Perl](https://www.perl.org/) ([PCRE](https://www.pcre.org/)), versão 8.42, e com suporte a `UTF-8`.

Um uso muito comum para o operador `$regex` é fazer consultas como o `LIKE` do `SQL`. Considere os seguintes documentos na coleção `products`:

```js
{ _id: 100, sku: "abc123", description: "Single line description." },
{ _id: 101, sku: "abc789", description: "First line\nSecond line" },
{ _id: 102, sku: "xyz456", description: "Many spaces before     line" },
{ _id: 103, sku: "xyz789", description: "Multiple\nline description" }
```

A _query_ abaixo seleciona todos os documentos em que o campo `sku` “termine” com `"789"`:

```js
db.products.find({ sku: { $regex: /789$/ } });
```

O exemplo acima equivale ao comando `LIKE` do `SQL`:

```sql
SELECT * FROM products WHERE sku LIKE "%789";
```

Você pode especificar opções na regex. Por exemplo, você pode especificar a opção _case-insensitive_, fazendo com que o **MongoDB** ignore letras maiúsculas ou minúsculas. Veja o exemplo abaixo, que retorna palavras “começando” com ABC:

```js
db.products.find({ sku: { $regex: /^ABC/i } });
```

O caractere `i` ao lado da expressão indica a opção _case-insensitive_. Dessa forma, apenas os documentos que contenham `ABC` no campo `sku` serão retornados, sem se importar se está em maiúsculo ou minúsculo:

```js
{ "_id" : 100, "sku" : "abc123", "description" : "Single line description." }
{ "_id" : 101, "sku" : "abc789", "description" : "First line\nSecond line" }
```

Basicamente, tudo o que você pode construir com expressões regulares em outras linguagens de programação funcionará também em suas _queries_ no **MongoDB**. Saiba mais sobre o operador `$regex` clicando [aqui](https://docs.mongodb.com/manual/reference/operator/query/regex/index.html).


# Operador $mod

Saindo um pouco dos operadores textuais, existe o operador `$mod`, que seleciona todos os documentos em que o valor do campo dividido por um divisor seja igual ao valor especificado (ou seja, executa a operação matemática módulo).

> Operação módulo: encontra o resto da divisão de um número por outro.

Considere os seguintes documentos na coleção `inventory`:

```js
{ _id: 1, item: "abc123", qty: 0 },
{ _id: 2, item: "xyz123", qty: 5 },
{ _id: 3, item: "ijk123", qty: 12 }
```

A _query_ a seguir seleciona todos os documentos da coleção em que o valor do campo `qty` módulo `4` seja `0`:

```js
db.inventory.find({ qty: { $mod: [4, 0] } });
```

Então, apenas os seguintes documentos serão retornados:

```js
{ "_id" : 1, "item" : "abc123", "qty" : 0 }
{ "_id" : 3, "item" : "ijk123", "qty" : 12 }
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/c436d6e0-7e4f-4d32-8e47-15c4f17e5e0f/lesson/85e10495-3ca2-42bf-a9ce-2019659fa2fe)
