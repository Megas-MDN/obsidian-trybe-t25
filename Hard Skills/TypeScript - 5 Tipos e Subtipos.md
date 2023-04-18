[[TypeScript]]

Vamos falar um pouco mais sobre o grande recurso do **TypeScript** em relação ao **JavaScript**: os tipos.

Em **TypeScript,** todos os tipos são subtipos de um tipo principal chamado `any`, e este é um tipo que pode representar qualquer valor em **JavaScript**. Os demais tipos são os **_tipos primitivos_**, **_tipos de objeto_** ou **_parâmetros de tipo_**.

![Imagem que demonstra a divisão de tipos na linguagem TypeScript](https://content-assets.betrybe.com/prod/Imagem%20que%20demonstra%20a%20divis%C3%A3o%20de%20tipos%20na%20linguagem%20TypeScript.png)

Imagem que demonstra a divisão de tipos na linguagem TypeScript

## Tipos primitivos:

Hoje nós vamos focar em alguns dos tipos primitivos, que são os tipos `boolean`, `number`, `string`, `void`, `null` e `undefined`.

**boolean**: recebe verdadeiro (`true`) ou falso (`false`)

```typescript
let yes: boolean = true; // cria uma variável de nome "yes" e diz que o tipo é booleano e o valor é true
let no: boolean = false; // cria uma variável de nome "no" e diz que o tipo é booleano e o valor é false
```

**number**: recebe valores numéricos e, assim como no **_JavaScript_**, todos são valores de ponto flutuante.

```typescript
// cria uma variável de nome "x" e diz que o tipo é number mas não seta o valor
// isso não funciona com const
let x: number;

let y: number = 0;
let z: number = 123.456;
```

**string**: recebe uma sequência de caracteres armazenados como unidades de código UTF-16 Unicode.

```typescript
let s: string;
let empty: string = "";
let abc: string = 'abc';
```

**void**: existe apenas para indicar a ausência de um valor, como em uma função sem valor retornado.

```typescript
function sayHelloWorld(): void {
  console.log("Hello World!");
}
```

**null** e **undefined**: são subtipos de todos os outros tipos.

```typescript
let nullValue = null;
let undefinedValue = undefined;
```

## Exemplo de declaração de variáveis utilizando inferência de tipo

Como visto anteriormente, podemos utilizar a inferência de tipo no **TypeScript**. É possível declarar uma variável sem especificarmos explicitamente o tipo e o compilador fará a inferência do tipo por meio do valor definido para a variável. Vamos verificar isso no site do [Playground TypeScript](https://www.typescriptlang.org/pt/play?#code/DYUwLgBAZsCGDmEC8EwCcCuIDcED0eEA9hAMZEC2ADgJZwAmRaENaAhywHZQhqvGoaVEgCMiRULE4BYAFDlOAZwkgAdMCLwAFAHIA8oOER6ICACIYCMxACXALh0AaVAE8qIIlGhx4ASmxycgqKkJwYFCK8AAoAksgQAMyqAIwALMkAbLgEAuTUdLCMzKwcNNy8-CRgQiRhEbxBREoq6pq6BtVGJuZ1kWix1vZOru6eEL3RMf6BsqCQFCCKigimKGYAEiDAGhAA6kzA9ACEZtmEJHm0DEws7Fw8fMxVNRAhfJzwjc2grdr6hiRumYFksVoMHM4wG4PF4Qct4CBprIgA). Após digitar o código abaixo, clique no botão `Run` e, ao término da execução, será exibido o resultado na guia `Logs`.

```typescript
let flag = true; // o compilador irá inferir o tipo boolean
console.log('O tipo de "flag" é:', typeof flag);

const numberPI = 3.1416; // o compilador irá inferir o tipo number
console.log('O tipo de "numberPI" é:', typeof numberPI);

let message = "Hello World!"; // o compilador irá inferir o tipo string
console.log('O tipo de "message" é:', typeof message);
```

A imagem abaixo apresenta o resultado esperado.

![Verificação de tipos no site TypeScript Playground](https://content-assets.betrybe.com/prod/c7ac3605-f5ee-4669-a00b-6d1051e9d607-Verifica%C3%A7%C3%A3o%20de%20tipos%20no%20site%20TypeScript%20Playground.png)
Verificação de tipos no site TypeScript Playground.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/4e3b7d3a-94a1-4fce-9545-0f2b04f8ccd9/day/f2bc13d9-91a6-488b-aa3f-257b0f5bb449/lesson/c2860a94-e8c2-43ea-8d8d-5e9f7cacfd95)
