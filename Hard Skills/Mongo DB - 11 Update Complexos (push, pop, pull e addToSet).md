[[Mongo DB]]

## Operador $push

O operador `$push` adiciona um valor a um _array_. Se o campo não existir no documento, um novo _array_ com o valor em um elemento será adicionado.

Sintaxe:

```js
{ $push: { <campo1>: <valor1>, ... } }
```

Em conjunto com o `$push` você pode utilizar o que chamamos de **modificadores**. Cada um desses modificadores tem funções específicas que você verá melhor com exemplos. São eles:

-   `$each`: Adiciona múltiplos valores a um _array_;
-   `$slice`: Limita o número de elementos do _array_. Requer o uso do modificador `$each`;
-   `$sort`: Ordena os elementos do _array_. Requer o uso do modificador `$each`;
-   `$position`: Especifica a posição do elemento que está sendo inserido no _array_. Também requer o modificador `$each`. Sem o modificador `$position`, o operador `$push` adiciona o elemento no final do _array_.
    

Quando você utiliza um modificador, o processo de **push** ocorre na seguinte ordem, independentemente da ordem em que os modificadores aparecem:

1.  Altera o _array_ para adicionar os elementos na posição correta;
2.  Aplica a ordenação (`$sort`), se especificada;
3.  Limita o _array_ (`$slice`), se especificado;
4.  Armazena o _array_.
    

Veja alguns exemplos. Utilizaremos um banco de dados chamado `sales`.

### Adicionando um valor a um _array_

Considere a coleção `supplies`, uma coleção vazia. A operação abaixo adiciona um objeto que tem as informações da compra de um produto ao _array_ `items` do documento em que o `_id` seja igual a **1** na coleção `supplies`.

Para não precisarmos escrever uma _query_ só para fazer o _insert_ do documento, vamos usar a opção `upsert: true` para já adicionar o elemento ao mesmo tempo que usamos o operador `$push`. É importante ficar nítido que a condição `upsert` não influencia a forma como o `$push` funciona.

```js
use sales;
db.supplies.updateOne(
  { _id: 1 },
  {
    $push: {
      items: {
        "name": "notepad",
        "price":  35.29,
        "quantity": 2,
      },
    },
  },
  { upsert: true },
);
```

Veja, o método `updateOne()` é o mesmo que você já utilizou nos exemplos anteriores. A única diferença é a inclusão do operador `$push`. O resultado dessa operação é um documento com o seguinte formato:

Copiar

```js
{
	_id : 1,
	items : [
		{
			"name" : "notepad",
			"price" : 35.29,
			"quantity" : 2,
		},
	],
}
```

### Adicionando múltiplos valores a um array

Se você quiser, também é possível adicionar múltiplos valores a um _array_ utilizando o operador `$push`, mas dessa vez será necessário adicionar o **modificador** `$each`.

A operação abaixo adicionará mais dois produtos ao _array_ `items` do primeiro documento na coleção `supplies`:

Copiar

```js
db.supplies.updateOne(
  {},
  {
    $push: {
      items: {
        $each: [
          {
            "name": "pens",
            "price": 56.12,
            "quantity": 5,
          },
          {
            "name": "envelopes",
            "price": 19.95,
            "quantity": 8,
          },
        ],
      },
    },
  },
  { upsert: true },
);
```

O documento ficará assim:

Copiar

```js
{
	_id : 1,
	items : [
		{
			"name" : "notepad",
			"price" : 35.29,
			"quantity" : 2,
		},
		{
			"name" : "pens",
			"price" : 56.12,
			"quantity" : 5,
		},
		{
			"name" : "envelopes",
			"price" : 19.95,
			"quantity" : 8,
		},
	],
}
```

### Múltiplos modificadores

O `$push` pode ser utilizado com múltiplos modificadores, fazendo várias operações ao mesmo tempo em um _array_.

Desconsidere as últimas alterações com `$push` (se quiser acompanhar, você pode utilizar `db.dropDatabase()` para remover as alterações anteriores) e veja a realização dele abaixo, com ainda mais opções!

Copiar

```js
db.supplies.updateOne(
  { _id: 1 },
  {
    $push: {
      items: {
        $each: [
          {
            "name" : "notepad",
            "price" : 35.29,
            "quantity" : 2,
          },
          {
            "name": "envelopes",
            "price": 19.95,
            "quantity": 8,
          },
          {
            "name": "pens",
            "price": 56.12,
            "quantity": 5,
          },
        ],
        $sort: { "quantity": -1 },
        $slice: 2,
      },
    },
  },
  { upsert: true },
);
```

Essa operação utiliza os seguintes modificadores:

-   O modificador `$each` para adicionar múltiplos documentos ao _array_ `items`;
    
-   O modificador `$sort` para ordenar todos os elementos alterados no _array_ `items` pelo campo `quantity` em ordem decrescente;
    
-   E o modificador `$slice` para manter apenas os **dois primeiros** elementos ordenados no _array_ `items`.
    

Em resumo, essa operação mantém no _array_ `items` apenas os dois documentos com a _quantidade_ (campo `quantity`) mais alto. Veja o resultado logo abaixo:

Copiar

```js
{
  _id : 1,
  items : [
    {
      "name" : "envelopes",
      "price" : 19.95,
      "quantity" : 8,
    },
    {
      "name" : "pens",
      "price" : 56.12,
      "quantity" : 5,
    },
  ],
}
```


## Operador $pop

Uma maneira simples de remover o primeiro ou o último elemento de um _array_ é utilizar o operador `$pop`. Passando o valor **-1** ao operador `$pop` você removerá o primeiro elemento. Já ao passar o valor **1,** você removerá o último elemento do _array_. Simples, não é?!

Considere o seguinte documento na coleção `supplies`:

```js
{
  _id: 1,
  items: [
    {
      "name" : "notepad",
      "price" : 35.29,
      "quantity" : 2,
    },
    {
      "name": "envelopes",
      "price": 19.95,
      "quantity": 8,
    },
    {
      "name": "pens",
      "price": 56.12,
      "quantity": 5,
    },
  ],
}
```

### Removendo o primeiro item de um array

Para remover o primeiro elemento do _array_ `items`, utilize a seguinte operação:

```js
db.supplies.updateOne({ _id: 1 }, { $pop: { items: -1 } });
```

O documento será alterado e o primeiro elemento será removido do _array_ `items`:

```js
{
  _id: 1,
  items: [
    {
      "name": "envelopes",
      "price": 19.95,
      "quantity": 8,
    },
    {
      "name": "pens",
      "price": 56.12,
      "quantity": 5,
    },
  ],
}
```

### Removendo o último item de um array

Para remover o último elemento do _array_ `items`, utilize a seguinte operação:

```js
db.supplies.updateOne({ _id: 1 }, { $pop: { items: 1 } });
```

Executando essa operação, é removido o último elemento do _array_ `items` e o documento ficará assim:

```js
{
  _id: 1,
  items: [
    {
      "name" : "notepad",
      "price" : 35.29,
      "quantity" : 2,
    },
    {
      "name": "envelopes",
      "price": 19.95,
      "quantity": 8,
    },
  ],
}
```



## Operador $pull

O operador `$pull` remove de um _array_ existente todos os elementos com um ou mais valores que atendam à condição especificada.

### Removendo todos os itens iguais a um valor especificado

Vamos considerar os seguintes documentos na coleção `supplies`:

```js
{
  _id: 1,
  items: [
    {
      "name" : "notepad",
      "price" : 35.29,
      "quantity" : 2,
    },
    {
      "name": "envelopes",
      "price": 19.95,
      "quantity": 8,
    },
    {
      "name": "pens",
      "price": 56.12,
      "quantity": 5,
    },
  ],
},
{
  _id: 2,
  items: [
    {
      "name" : "pencil",
      "price" : 5.29,
      "quantity" : 2,
    },
    {
      "name": "envelopes",
      "price": 19.95,
      "quantity": 8,
    },
    {
      "name": "backpack",
      "price": 80.12,
      "quantity": 1,
    },
    {
      "name": "pens",
      "price": 56.12,
      "quantity": 5,
    },
  ],
}
```

Digamos que você queira remover do _array_ `items` os elementos `pens` e `envelopes`:


```js
db.supplies.updateMany(
  {},
  {
    $pull: {
      items: {
        name: { $in: ["pens", "envelopes"] },
      },
    },
  },
);
```

Na atualização acima, foi utilizado o operador `$pull` combinado com o operador `$in` para alterar o _array_ `items`. O resultado dessa atualização pode ser visto a seguir:


```js
{
  _id : 1,
  items : [
    {
      "name" : "notepad",
      "price" : 35.29,
      "quantity" : 2,
    },
  ],
},
{
  _id : 2,
  items : [
    {
      "name" : "pencil",
      "price" : 5.29,
      "quantity" : 2,
    },
    {
      "name" : "backpack",
      "price" : 80.12,
      "quantity" : 1,
    },
  ],
}
```

### Removendo todos os itens que atendem a uma condição diretamente no $pull

Você pode especificar uma condição de remoção diretamente no `$pull`. Essa condição pode ser, por exemplo, um operador de comparação.

Tendo o seguinte documento na coleção `profiles`:

```js
{ _id: 1, votes: [3, 5, 6, 7, 7, 8] }
```

Você pode remover todos os elementos do _array_ `votes` que sejam maiores ou iguais a **6** (operador `$gte`). Por exemplo:


```js
db.profiles.updateOne(
  { _id: 1 },
  {
    $pull: {
      votes: { $gte: 6 },
    },
  },
);
```

Depois dessa operação, o documento ficará apenas com valores menores do que 6 no _array_ `votes`, veja só:


```js
{ _id: 1, votes: [3,  5] }
```

### Removendo itens em um array de Documentos

Veja a coleção `survey` com os seguintes documentos:


```js
{
  _id: 1,
  results: [
    { item: "A", score: 5 },
    { item: "B", score: 8, comment: "Strongly agree" },
  ],
},
{
  _id: 2,
  results: [
    { item: "C", score: 8, comment: "Strongly agree" },
    { item: "B", score: 4 },
  ],
}
```

Os documentos têm um _array_ chamado `results` que armazena documentos.

Com a operação abaixo, você consegue remover do _array_ `results` todos os elementos que contenham o campo `score` igual a **8** e o campo `item` igual a **“B”**. Ou seja, o documento deve atender a ambas as condições.

```js
db.survey.updateMany(
  {},
  {
    $pull: {
      results: { score: 8 , item: "B" },
    },
  },
);
```

A expressão do operador `$pull` aplica as condições a cada elemento do _array_ `results` como se estivesse no primeiro nível, isso porque os documentos dentro do _array_ `results` não contêm outros campos com mais _arrays_. Se isso acontecer, você deve utilizar uma outra abordagem, que será detalhada mais à frente.

Após essa operação, os documentos ficarão assim:

```js
{
  _id: 1,
  results: [ { "item": "A", "score": 5 } ],
},
{
  _id: 2,
  results: [
    { "item": "C", "score": 8, "comment": "Strongly agree" },
    { "item": "B", "score": 4 },
  ],
}
```


## Operador $addToSet

O operador `$addToSet` é utilizado quando você precisa garantir que os valores de um _array_ não sejam duplicados. Ou seja, ele garante que apenas valores únicos estejam presentes no _array_, tratando o _array_ como se fosse um conjunto (uma vez que conjuntos, na matemática, não podem conter elementos duplicados).

Você precisa ter em mente três aspectos sobre o `$addToSet`:

-   Se você utilizá-lo em um campo que não existe no documento alterado, ele criará um campo do tipo _array_ com o valor especificado na operação;
-   Se você utilizá-lo em um campo já existente no documento, mas esse campo não for um _array_, a operação não funcionará;
-   Se o valor passado for um documento, o MongoDB o considerará como duplicado se um documento existente no _array_ for exatamente igual ao documento a ser adicionado, ou seja, possui os mesmos campos com os mesmos valores e esses campos estão na mesma ordem.
    

Veja alguns exemplos considerando o documento abaixo na coleção `inventory`:


```js
{
  _id: 1,
  item: "polarizing_filter",
  tags: ["electronics", "camera"],
}
```

### Adicionando ao array

A operação abaixo adiciona o elemento **“accessories”** ao _array_ `tags` desde que **“accessories”** não exista no _array_:

```js
db.inventory.updateOne(
  { _id: 1 },
  { $addToSet: { tags: "accessories" } },
);
```

O _array_ `tags` agora tem mais um elemento:

```js
{
  _id: 1,
  item: "polarizing_filter",
  tags: [
    "electronics",
    "camera",
    "accessories",
  ],
}
```

### Se o valor existir

A operação abaixo tenta adicionar o elemento **“camera”** ao _array_ `tags`. Porém, esse elemento já existe e a operação não surtirá efeito:

```js
db.inventory.updateOne(
  { _id: 1 },
  { $addToSet: { tags: "camera"  } },
);
```

Como resultado dessa operação, é retornada uma mensagem dizendo que o MongoDB encontrou um documento com o `_id` igual a **1,** mas não fez nenhuma alteração:

```js
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 0 }
```

### Com o modificador $each

Você pode utilizar o operador `$addToSet` combinado com o modificador `$each`. Esse modificador permite que você adicione múltiplos valores a um _array_.

Veja o seguinte documento da coleção `inventory`:

```js
{ _id: 2, item: "cable", tags: ["electronics", "supplies"] }
```

A operação abaixo utiliza o operador `$addToSet` e o modificador `$each` para adicionar alguns elementos a mais no _array_ `tags`:


```js
db.inventory.updateOne(
  { _id: 2 },
  {
    $addToSet: {
      tags: {
        $each: ["camera", "electronics", "accessories"],
      },
    },
  },
);
```

Como resultado, a operação adicionará ao _array_ `tags` somente os elementos **“camera”** e **“accessories”,** uma vez que o elemento **“electronics”** já existia no _array_. Veja abaixo:

```js
{
  _id: 2,
  item: "cable",
  tags: ["electronics", "supplies", "camera", "accessories"],
}
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/9aa9cc0e-6e53-4986-a5fe-7b93df92375f/lesson/df071bd5-6d59-499f-a8e2-3859d1529710)