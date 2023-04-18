[[Mongo DB]]


## limit()

Você pode limitar o número de documentos retornados por uma consulta utilizando o método `limit()`. Esse método é semelhante à declaração `LIMIT` em um banco de dados que utiliza **SQL**.

Uma utilização comum do `limit()` é para maximizar a performance e evitar que o **MongoDB** retorne mais resultados do que o necessário para o processamento.

O método `limit()` é utilizado da seguinte forma:

```js
db.collection.find(<query>).limit(<número>)
```

Note que você deve especificar um valor numérico no `limit()`.

Um exemplo utilizando a coleção **bios**:

```js
db.bios.find().limit(5)
```

A operação acima retornará os **cinco** primeiros documentos da coleção **bios**.


## pretty()

Com o método `pretty()` você pode deixar os resultados exibidos no **MongoDB Shell** um pouco mais legíveis. Esse método aplica uma indentação na exibição dos resultados no console, de forma que fica bem melhor de ler.

Exemplo de utilização do método `pretty()`, usando a coleção **bios**:

```js
db.bios.find().limit(5).pretty()
```

Utilize o método `pretty()` à vontade!


## skip(<número>)

Acione o método `skip()` para controlar a partir de que ponto o **MongoDB** começará a retornar os resultados. Essa abordagem pode ser bastante útil para realizar paginação dos resultados.

O método `skip()` precisa de um **parâmetro numérico** que determinará **quantos documentos** serão **“pulados”** antes de começar a retornar.

O exemplo abaixo na coleção **bios** pulará os dois primeiros documentos e retornará o cursor a partir daí:


```js
db.bios.find().skip(2)
```

Você pode combinar os métodos `limit()` e `skip()` criando, assim, uma paginação:

```js
db.bios.find().limit(10).skip(5)
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/da82d65f-2261-4bcb-87bb-71e6a7e565f5/lesson/12b92b15-faea-4dba-9c83-920dedd3b789)
