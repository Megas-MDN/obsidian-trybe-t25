[[React]]
[[JavaScript]]
[[Atualizar Estado em React]] 
[[Objeto]]


Desestruturação Dinâmica é um facilitador para acessar propriedades de forma dinâmica dentro de uma desestruturação.

Primeiramente, vale ressaltar o que é desestruturação de objetos em JavaScript. Para isso, considere o exemplo abaixo:

```javascript
const myObject = {
  name: 'John Doe',
  age: 50
};

// Estamos desestruturando a propriedade `name` do objeto `myObject`.
const { name, age } = myObject;

// Anteriormente, a forma mais simples de se alcançar o mesmo efeito:
const name = myObject.name;
const age = myObject.age;
```

Note então que a desestruturação é uma forma simples de se extrair alguns valores de dentro de um objeto, criando variáveis no escopo atual de acordo com os nomes das respectivas propriedades.

E se você quiser desestruturar uma propriedade de um objeto, atribuindo um outro nome à variável que será criada, você pode utilizar esta sintaxe:

```javascript
const myObject = {
  name: 'John Doe'
};

// No exemplo abaixo, `name` é a propriedade que queremos
// desestruturar do objeto. E `prop` é o nome da variável
// que será criada a partir da desestruturação.
// Se omitíssemos `: prop` da construção abaixo, uma variável
// `name` criar-se-ia no escopo atual. Então...

// Nome da propriedade que estaremos "acessando" (desestruturando) do objeto.
//      ↓↓↓↓
const { name: prop } = myObject;
//            ↑↑↑↑
// Nome da variável que será criada.

console.log(prop); // John Doe
```

### Desestruturação "dinâmica"

A desestruturação via propriedades computadas permite fazer a desestruturação mesmo se você não "souber estaticamente" a chave que você deseja acessar. Em outras palavras, ao invés de ser "desestruturação estática", ocorre uma "desestruturação dinâmica".

A forma mais simples de se acessar uma propriedade a partir de uma expressão ("dinâmica") é utilizar a notação de colchetes para acessar à propriedade do objeto. Veja:

```javascript
const myDynamicKey = 'name';

const myObject = {
  name: 'John Doe'
};

// O que faremos abaixo é a mesma coisa que:
//
//   ```
//   myObject.name;
//   ```
//
// Só que estamos utilizando uma outra variável,
// que está representando a chave que queremos acessar.
//
// Isso é útil para acessar propriedades de forma dinâmica.
// A propriedade a ser lida virá da avaliação de `myDynamicKey`:
//                   ↓↓↓↓↓↓↓↓↓↓↓↓↓↓
const prop = myObject[myDynamicKey];

console.log(prop); // John Doe
```

Agora, se quisermos fazer isso utilizando a desestruturação:

```javascript
const myDynamicKey = 'name';

const myObject = {
  name: 'John Doe'
};

// Estamos declarando uma variável `prop` que virá
// da desestruturação de uma propriedade computada.
//
// A propriedade que iremos desestruturar do objeto
// virá do valor de `myDynamicKey`. No caso, como
// `myDynamicKey` é "name", então iremos acessar, de
// forma dinâmica, a propriedade `name` de `myObject`.
const { [myDynamicKey]: prop } = myObject;

console.log(prop); // John Doe
```

Então, destrinchando a nossa desestruturação acima:

```javascript
// Computação dinâmica que estamos fazendo. A propriedade
// correspondente ao valor de `myDynamicKey` será desestruturada
// de forma dinâmica.
//      ↓↓↓↓↓↓↓↓↓↓↓↓↓↓
const { [myDynamicKey]: prop } = myObject;
//                      ↑↑↑↑
// Variável que criamos para o resultado dessa computação dinâmica.
// Como estamos utilizando uma computação dinâmica nessa desestruturação,
// somos forçados a criar uma variável explicitamente na nossa desestruturação.
```

[Click aqui para acessar o link do arquivo](https://pt.stackoverflow.com/questions/430322/o-que-s%C3%A3o-nomes-computados-desestrutura%C3%A7%C3%A3o-din%C3%A2mica-em-javascript)
