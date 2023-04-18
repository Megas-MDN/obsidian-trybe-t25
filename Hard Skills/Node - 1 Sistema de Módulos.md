[[Node]]
[[Object Destructuring]]

- [Exportando módulos](#Exportando%0dmódulos)
- [Importando módulos](#Importando%0dmódulos)


Dados do site [ModuleCounts.com](http://www.modulecounts.com/) mostram que atualmente o NPM, onde os pacotes Node.js são disponibilizados, está entre os repositórios com maior número de pacotes.

> Ter muitos pacotes publicados no repositório atual, nos dá uma ideia de duas grandes vantagens do Node.js: uma comunidade extremamente ativa e uma grande quantidade de ferramentas para resolver os mais diversos tipos de problema.

Mas, o que é um pacote Node e como podemos utilizá-los no nosso código?🤔

Iremos chegar a essa resposta em breve, mas antes disso você precisa saber o que é um **módulo em Node.js**. 🤓

> 🎬 Caso você prefira consumir este conteúdo em vídeo, ele está disponível mais adiante nesta seção.

Anota aí 🖊: um módulo em Node.js é um “pedaço de código”, o qual pode ser organizado em um ou mais arquivos, que possui escopo próprio. Ou seja, suas variáveis, funções, classes e afins só estão disponíveis nos arquivos que fazem parte daquele módulo.

Em outras palavras, um módulo é uma funcionalidade, ou um conjunto de funcionalidades, que se encontram isoladas do restante do código. **O Node.js possui três tipos de módulos:** internos, locais e de terceiros.

## Módulos internos

Os módulos internos (ou _core modules_) são inclusos no Node.js e instalados junto com ele quando baixamos o _runtime_. Alguns exemplos de _core modules_ são:

-   [`fs`](https://nodejs.org/api/fs.html): fornece uma API para interagir com o sistema de arquivos de forma geral;
-   [`url`](https://nodejs.org/api/url.html): provê utilitários para ler e manipular URLs;
-   [`util`](https://nodejs.org/api/util.html): oferece ferramentas e funcionalidades comumente úteis a pessoas programadoras.
-   [`os`](https://nodejs.org/api/os.html): oferece ferramentas e funcionalidades relacionadas ao sistema operacional.

⚠️ **Aviso**: clique no nome de cada módulo para abrir a documentação oficial (em inglês).

## Módulos locais

Os módulos locais são aqueles definidos juntamente à nossa aplicação. Eles representam as funcionalidades ou partes do nosso programa que foram separados em arquivos diferentes. Podem ser publicados no NPM, para que outras pessoas possam baixá-los e utilizá-los, o que nos leva ao nosso próximo e último tipo de módulo.

## Módulos de terceiros

Os módulos de terceiros são aqueles criados por outras pessoas desenvolvedoras e disponibilizados para uso por meio do `npm`. Nós também podemos criar e publicar nossos próprios módulos, seja para utilizarmos em diversas aplicações diferentes, seja para permitir que outras pessoas os utilizem. Veremos como fazer isso adiante, para isso continue a leitura.


## Maneiras de importar e exportar módulos

Quando queremos utilizar o conteúdo de um módulo ou pacote de outro arquivo no Node.js, precisamos **importar** esse módulo/pacote para o contexto atual no qual estamos.

Para isso, existem dois sistemas de módulos difundidos na comunidade JavaScript:

-   Módulos **ES6**;
    
-   Módulos **CommonJS**.
    

## ES6

O nome ES6 vem de ECMAScript 6 (especificação seguida pelo JavaScript).

> Nessa especificação, os módulos são importados utilizando a palavra-chave `import`, tendo como contrapartida a palavra-chave `export` para exportá-los.

O Node.js só começou a oferecer um suporte estável para o sistema de módulos ES6 a partir da versão 14. A expectativa é que em um futuro próximo esse padrão, que agora é oferecido de forma nativa, se torne o recomendado. Porém, por ser um recurso recente, ainda não conquistou o espaço que até então é ocupado pelo CommonJS.

Se você tentar utilizar os módulos ES6 em um projeto Node.js de forma padrão, você poderá se deparar com o seguinte erro no seu terminal `SyntaxError: Cannot use import statement outside a module`.

> Por ainda não ser o padrão recomendado, é necessária a adição de uma chave no arquivo `package.json` (este arquivo será abordado na lição `NPM`) antes que seja possível utilizar as importações do ES6.

Felizmente, o próprio erro sugere 2 soluções de como resolver esse problema:

1️⃣ Trocar a extensão dos arquivos de `.js` para `.mjs`. No qual o erro aparecera da seguinte forma:

> `(node:4871) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.`. ;

2️⃣ Adicionar no arquivo `package.json` a chave `type` com o valor `module`, exemplo:

```json
// package.json
{
  ...
  "type": "module",
  ...
}
```

Vale destacar que antes de se tornar um recurso nativo, só era possível utilizar o padrão ES6 no Node.js por meio de transpiladores como o [Babel](https://babeljs.io/), ou supersets da linguagem, como o [TypeScript](https://www.typescriptlang.org/).

> **Transpiladores** são ferramentas que leem o código-fonte escrito em uma linguagem como o Node.js e produzem o código equivalente em outra linguagem.
> 
> **Supersets** são linguagens que utilizam um transpilador para adicionar novas funcionalidades ao JavaScript.

Para saber mais sobre módulos ES6 e transpiladores, acesse a seção de Recursos adicionais (opcional).

## CommonJS

No CommonJS as palavras-chaves utilizadas para importação e exportação de módulos são, respectivamente, `require()` e `module.exports`.

O CommonJS é o sistema de módulos padrão do Node.js e, portanto, o sistema que utilizaremos daqui para frente.

## Exportando módulos

Para exportar algo no sistema CommonJS, utilizamos a variável global `module.exports`, atribuindo a ela o valor que desejamos exportar:

```js
// brlValue.js
const brl = 5.37;

module.exports = brl;
```

-   Note como utilizamos as palavras-chave `module.exports`.

> Como vimos anteriormente, um módulo possui um escopo isolado, ou seja, suas funções, variáveis, classes e demais definições existem somente dentro do módulo.

O `module.exports` nos permite definir quais desses “objetos” internos ao módulo serão **exportados**, ou seja, estarão acessíveis para os arquivos que importarem aquele módulo. Ele pode receber **qualquer valor válido em JavaScript, incluindo objetos, classes, funções e afins.**

No arquivo acima, estamos exportando do nosso módulo o valor da constante `brl`(que é `5.37`), ao importarmos esse módulo, receberíamos o valor `5.37` como resposta. Apesar disso funcionar, exportar um único valor constante assim não é comum. Vamos observar um caso que acontece com mais frequência:

```js
// brlValue.js
const brl = 5.37;

const usdToBrl = (valueInUsd) => valueInUsd * brl;

module.exports = usdToBrl;
```

💪**Agora,vamos trazer isso para a prática!**

Imagine que estamos exportando uma função, de modo que podemos utilizá-la para converter um valor em dólares para outro valor,neste caso em reais.

O uso desse nosso módulo se daria da seguinte forma:

```js
// index.js
const convert = require('./brlValue');

const usd = 10;
const brl = convert(usd);

console.log(brl) // 53.7
```

Perceba que podemos dar o nome que quisermos para a função depois que a importamos, independente de qual é o seu nome dentro do módulo.

Suponha que agora desejamos exportar tanto a função de conversão quanto o valor do dólar (a variável `brl`). Para isso, podemos exportar um objeto contendo as duas constantes da seguinte forma:

```js
// brlValue.js
const brl = 5.37;

const usdToBrl = (valueInUsd) => valueInUsd * brl;

module.exports = {
  brl,
  usdToBrl,
};
```

Desse modo, ao importarmos o módulo receberemos o seguinte objeto como resposta:

```js
// index.js
const brlValue = require('./brlValue');

console.log(brlValue); // { brl: 5.37, usdToBrl: [Function: usdToBrl] }

console.log(`Valor do dólar: ${brlValue.brl}`); // Valor do dólar: 5.37
console.log(`10 dólares em reais: ${brlValue.usdToBrl(10)}`); // 10 dólares em reais: 53.7
```

Como estamos lidando com um objeto, podemos utilizar _object destructuring_ para transformar as propriedades do objeto importado em constantes no escopo global:

```js
const { brl, usdToBrl } = require('./brlValue');

console.log(`Valor do dólar: ${brl}`); // Valor do dólar: 5.37
console.log(`10 dólares em reais: ${usdToBrl(10)}`); // 10 dólares em reais: 53.7
```


## Importando módulos

A seguir, você verá como utilizar o `require` para importar cada tipo de módulo.

### Módulos locais

Quando queremos importar um módulo local, precisamos passar para o `require` o caminho do módulo, seguindo a mesma assinatura.

-   Por exemplo: `require('./meuModulo')`. Note que a extensão (`.js`) não é necessária. Por padrão, o Node já procura por arquivos terminados em `.js` ou `.json` e os considera como módulos.

Além de importarmos um arquivo como módulo, podemos importar uma pasta. Isso é útil, pois muitas vezes um módulo está dividido em vários arquivos, porém, desejamos importar todas as suas funcionalidades de uma única vez. Nesse caso, a pasta precisa conter um arquivo chamado `index.js`, o qual importa cada um dos arquivos do módulo e os exporta da forma mais conveniente.

Por exemplo:

```js
// meuModulo/funcionalidade-1.js

module.exports = function () {
  console.log('funcionalidade1');
}
```

```js
// meuModulo/funcionalidade-2.js

module.exports = function () {
  console.log('funcionalidade2');
}
```

```js
// meuModulo/index.js
const funcionalidade1 = require('./funcionalidade-1');
const funcionalidade2 = require('./funcionalidade-2');

module.exports = { funcionalidade1, funcionalidade2 };
```

No exemplo acima, quando importarmos o módulo `meuModulo`, teremos um objeto contendo duas propriedades, as quais são as funcionalidades que exportamos dentro de `meuModulo/index.js`.

Para importarmos e utilizarmos o módulo `meuModulo`, basta passar o caminho da pasta como argumento para a função `require`, desse modo:

```js
// minha-aplicacao/index.js
const meuModulo = require('./meuModulo');

console.log(meuModulo); // { funcionalidade1: [Function: funcionalidade1], funcionalidade2: [Function: funcionalidade2] }

meuModulo.funcionalidade1();
```

## Módulos internos

Para utilizarmos um módulo interno, devemos passar o nome do pacote como parâmetro para a função `require`. Por exemplo, `require('fs')` importa o pacote `fs`, responsável pelo sistema de arquivos.

Uma vez que importamos um pacote, podemos utilizá-lo no nosso código como uma variável da seguinte forma:


```js
const fs = require('fs');

fs.readFileSync('./meuArquivo.txt');
```

Repare que o nome da variável pode ser qualquer um que escolhermos. O importante é o nome do pacote que passamos como parâmetro para o `require`.

## Módulos de terceiros

Módulos de terceiros são importados da mesma forma que os módulos internos: passando seu nome como parâmetro para a função `require`. A diferença é que, como esses módulos não são nativos do Node.js, precisamos primeiro instalá-los na pasta do projeto em que queremos utilizá-los.

Anota aí 🖊: O registro oficial do Node.js, em que milhares de pacotes estão disponíveis para serem instalados, é o `npm`. Além disso, `npm` também é o nome da ferramenta de linha de comando (CLI - _command line interface_), responsável por baixar e instalar esses pacotes. O CLI `npm` é instalado juntamente com o Node.js.

Quando importamos um módulo que não é nativo do Node.js e que não aponta para um arquivo local, o Node inicia uma busca por esse módulo. Essa busca acontece na pasta `node_modules`. Caso um módulo não seja encontrado na `node_modules` mais próxima do arquivo que o chamou, o Node procurará por uma pasta `node_modules` na pasta que contém a pasta atual. Caso encontrado, o módulo é carregado. Caso contrário, o processo é repetido em um nível de pasta acima. Isso acontece até que o módulo seja encontrado ou até que uma pasta `node_modules` não exista no local em que o Node está procurando.

![Fluxograma de importação de arquivos node](https://content-assets.betrybe.com/prod/3aea70b5-b9a6-48d7-b701-a63bb8f75d5e-Fluxo.png)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/3ec54ace-ebb1-416d-b899-d3050dd8d8b7)
