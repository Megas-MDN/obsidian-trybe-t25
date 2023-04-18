[[TypeScript]]

Agora, escreveremos nosso primeiro programa utilizando o **TypeScript.** Criaremos um módulo para calcular as áreas e perímetros de figuras geométricas.

**Obs:** No final da página, há um vídeo resumindo o que vimos até agora e demonstrando, na prática, algumas funcionalidades.

## Configuração

Crie um diretório chamado `exercises`. Nele, vamos inicializar nosso projeto **TypeScript**.

```bash
mkdir exercises && cd exercises
```

A seguir, vamos inicializar nosso projeto **Node**, instalar o TypeScript, o módulo `npm` com a configuração base do **TSConfig** para o **Node 16** (ou superior) e criar nosso `tsconfig.json`.

```bash
npm init -y
```

```bash
npm install -D typescript@4.4 @tsconfig/node16@1.0
```

```bash
touch tsconfig.json
```


```json
// ./tsconfig.json
{
  "extends": "@tsconfig/node16/tsconfig.json",
  "compilerOptions": {
    "target": "es2016",                                 
    "module": "commonjs",
    "rootDir": "./",
    "outDir": "./dist",
    "preserveConstEnums": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  }
}
```

Por fim, vamos instalar o pacote `npm` com as definições de tipos para o Node.js.

```bash
npm install -D @types/node@16.11
```

Em seguida, vamos criar dois arquivos: um chamado `index.ts`, que usaremos para testar o nosso módulo, e um chamado `exercises.ts`, onde faremos a implementação do nosso módulo com algumas funções.

```bash
touch index.ts && touch exercises.ts
```

## Implementação

Agora que já está tudo configurado, iniciaremos a implementação das funções. Primeiro, desenvolveremos uma função para calcular a área de um **quadrado**. A fórmula para o cálculo é elevar a medida de qualquer um dos lados ao quadrado. `A = s²`

![Área do quadrado](https://content-assets.betrybe.com/prod/846a1764-9dbe-4b7e-b79c-a6961c6a839c-%C3%81rea%20do%20quadrado.png)

Fórmula da Área de um Quadrado

```typescript
// ./exercises.ts

export function getSquareArea(side: number): number {
  return side ** 2;
}
```

A segunda função calculará a área de um **retângulo**. A fórmula para o cálculo é multiplicar a medida da base pela medida da altura. `A = b * h`

![Área do retângulo](https://content-assets.betrybe.com/prod/846a1764-9dbe-4b7e-b79c-a6961c6a839c-%C3%81rea%20do%20ret%C3%A2ngulo.png)

Fórmula da Área de um Retângulo

```typescript
// ./exercises.ts

// export function getSquareArea(side: number): number {
//   return side ** 2;
// }

export function getRectangleArea(base: number, height: number): number {
  return base * height;
}
```

A terceira calculará a área de um **triângulo**. A fórmula consiste em multiplicar a medida da base pela medida da altura e dividir o resultado pela metade. `A = (b * h) / 2`

![Área do triângulo](https://content-assets.betrybe.com/prod/846a1764-9dbe-4b7e-b79c-a6961c6a839c-%C3%81rea%20do%20tri%C3%A2ngulo.png)

Fórmula da Área de um Triângulo

```typescript
// ./exercises.ts

// export function getSquareArea(side: number): number {
//   return side ** 2;
// }

// export function getRectangleArea(base: number, height: number): number {
//   return base * height;
// }

export function getTriangleArea(base: number, height: number): number {
  return (base * height) / 2;
}
```

Já a quarta função, será responsável por calcular o **perímetro** de um **polígono**. Um polígono é uma forma geométrica fechada que possui lados retos. Por exemplo: triângulos, retângulos, quadrados, trapézios, hexágonos, entre outros. A fórmula para o cálculo consiste em somar a medida de todos os lados. `P = a + b + c + d + e + f ...`

![Perímetro de um polígono](https://content-assets.betrybe.com/prod/846a1764-9dbe-4b7e-b79c-a6961c6a839c-Per%C3%ADmetro%20de%20um%20pol%C3%ADgono.png)

Fórmula do Perímetro de um Polígono

```typescript
// ./exercises.ts

// export function getSquareArea(side: number): number {
//   return side ** 2;
// }

// export function getRectangleArea(base: number, height: number): number {
//   return base * height;
// }

// export function getTriangleArea(base: number, height: number): number {
//   return (base * height) / 2;
// }

export function getPolygonPerimeter(sides: number[]): number {
  return sides.reduce((acc, side) => acc + side, 0);
}
```

Para termos um exemplo com retorno de tipos diferentes. Nossa última função será responsável por verificar se um **triângulo é válido** com base na medida de seus lados e deve retornar um valor booleano (`true` ou `false`). Para que um triângulo exista, um de seus lados deve ser maior que a **diferença absoluta** entre os outros dois e **menor que a soma** deles. Caso queira entender melhor, consulte [este artigo](https://mundoeducacao.uol.com.br/matematica/condicao-existencia-um-triangulo.htm) do Mundo Educação.

Copiar

```typescript
// ./exercises.ts

// export function getSquareArea(side: number): number {
//   return side ** 2;
// }

// export function getRectangleArea(base: number, height: number): number {
//   return base * height;
// }

// export function getTriangleArea(base: number, height: number): number {
//   return (base * height) / 2;
// }

// export function getPolygonPerimeter(sides: number[]): number {
//   return sides.reduce((acc, side) => acc + side, 0);
// }

export function triangleCheck(
  sideA: number,
  sideB: number,
  sideC: number
): boolean {
  const checkSideA = (sideB - sideC) < sideA && sideA < (sideB + sideC);
  const checkSideB = (sideA - sideC) < sideB && sideB < (sideA + sideC);
  const checkSideC = (sideA - sideB) < sideC && sideC < (sideA + sideB);
  return checkSideA && checkSideB && checkSideC;
}
```

## Utilizando as funções

Pronto. Agora, vamos fazer algumas chamadas a este módulo no arquivo index.ts.

```typescript
// ./index.ts

import * as Ex from './exercises';

console.log("A ÁREA DE UM:");

console.log(`- Quadrado de lado 10cm: ${Ex.getSquareArea(10)}cm²`);
console.log(`- Quadrado de lado 5cm: ${Ex.getSquareArea(5)}cm²`);
console.log(`- Quadrado de lado 100cm: ${Ex.getSquareArea(100)}cm²`);

console.log(`- Retângulo de base 10cm e altura 25cm: ${Ex.getRectangleArea(10, 25)}cm²`);
console.log(`- Retângulo de base 5cm e altura 30cm: ${Ex.getRectangleArea(5, 30)}cm²`);
console.log(`- Retângulo de base 200cm e altura 100cm: ${Ex.getRectangleArea(200, 100)}cm²`);

console.log(`- Triângulo de base 10cm e altura 25cm: ${Ex.getTriangleArea(10, 25)}cm²`);
console.log(`- Triângulo de base 5cm e altura 30cm: ${Ex.getTriangleArea(5, 30)}cm²`);
console.log(`- Triângulo de base 100cm e altura 200cm: ${Ex.getTriangleArea(100, 200)}cm²`);

console.log("\nO PERÍMETRO DE UM:");

console.log(`- Quadrado de lado 10cm: ${Ex.getPolygonPerimeter([10, 10, 10, 10])}cm`);
console.log(`- Retângulo de base 10cm e altura 25cm: ${Ex.getPolygonPerimeter([10, 25, 10, 25])}cm`);
console.log(`- Triângulo cujos lados tem 10cm cada: ${Ex.getPolygonPerimeter([10, 10, 10])}cm`);

console.log("\nVERIFICA A EXISTÊNCIA DE TRIÂNGULOS CUJOS LADOS TÊM:");

console.log(`- 10cm, 5cm e 3cm: ${Ex.triangleCheck(10, 5, 3)}`);
console.log(`- 10cm, 5cm e 3cm: ${Ex.triangleCheck(10, 5, 8)}`);
console.log(`- 10cm, 5cm e 3cm: ${Ex.triangleCheck(30, 30, 30)}`);
```

Em seguida, vamos compilar o nosso programa:

```bash
npx tsc
```

Nossos arquivos **JavaScript** foram gerados dentro do diretório `dist`. Agora, basta rodar o nosso programa compilado utilizando o **Node**.

```bash
node ./dist/index.js
```

A saída esperada é:


```bash
A ÁREA DE UM:
- Quadrado de lado 10cm: 100cm²
- Quadrado de lado 5cm: 25cm²
- Quadrado de lado 100cm: 10000cm²
- Retângulo de base 10cm e altura 25cm: 250cm² 
- Retângulo de base 5cm e altura 30cm: 150cm²
- Retângulo de base 200cm e altura 100cm: 20000cm² 
- Triângulo de base 10cm e altura 25cm: 125cm²
- Triângulo de base 5cm e altura 30cm: 75cm²
- Triângulo de base 100cm e altura 200cm: 10000cm²

O PERÍMETRO DE UM:
- Quadrado de lado 10cm: 40cm
- Retângulo de base 10cm e altura 25cm: 70cm
- Triângulo cujos lados tem 10cm cada: 30cm 

VERIFICA A EXISTÊNCIA DE TRIÂNGULOS CUJOS LADOS TÊM:
- 10cm, 5cm e 3cm: false
- 10cm, 5cm e 3cm: true 
- 10cm, 5cm e 3cm: true 
```


## Para fixar

1.  Crie uma nova função para calcular a área de um losango. A área do losango é dada pelo resultado da multiplicação da diagonal maior (D) pela diagonal menor (d) dividido por dois. `A = (D * d) / 2`

![Área do Losango](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20Losango.png)

Fórmula da Área de um Losango

-   Calcule a área de um losango que tem D = 32cm e d = 18cm;
-   Calcule a área de um losango que tem D = 200cm e d = 50cm;
-   Calcule a área de um losango que tem D = 75cm e d = 25cm.

2.  Crie uma nova função para calcular a área de um trapézio. A área do trapézio é dada pelo produto da altura (h) com a soma da base maior (B) e a base menor (b) dividido por dois. `A = [(B + b) * h] / 2`

![Área do Trapézio](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20Trap%C3%A9zio.png)

Fórmula da Área de um Trapézio

-   Calcule a área de um trapézio que tem B = 100cm, b = 70cm e altura = 50cm;
-   Calcule a área de um trapézio que tem B = 75cm, b = 50cm e altura = 35cm;
-   Calcule a área de um trapézio que tem B = 150cm, b = 120cm e altura = 80cm.

3.  Crie uma nova função para calcular a área de um círculo. A área do círculo de raio `r` é calculada multiplicando o raio ao quadrado pelo número irracional ℼ (em geral utilizamos ℼ = 3,14). `A = ℼ * r²`. _Dica: você pode acessar o valor de ℼ utilizando o módulo nativo `Math.PI`_.

![Área do Círculo](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20C%C3%ADrculo.png)

Fórmula da Área de um Círculo

-   Calcule a área de um círculo de raio igual 25cm;
-   Calcule a área de um círculo de raio igual 100cm;
-   Calcule a área de um círculo de raio igual 12,5cm.

## Solução

1.  Crie uma nova função para calcular a área de um losango. A área do losango é dada pelo resultado da multiplicação da diagonal maior (D) pela diagonal menor (d) dividido por dois. `A = (D * d) / 2`

![Área do Losango](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20Losango.png)

Fórmula da Área de um Losango

-   Calcule a área de um losango que tem D = 32cm e d = 18cm;
-   Calcule a área de um losango que tem D = 200cm e d = 50cm;
-   Calcule a área de um losango que tem D = 75cm e d = 25cm.

```typescript
// ./exercises.ts

// export function getSquareArea(side: number): number {
//   return side ** 2;
// }

// export function getRectangleArea(base: number, height: number): number {
//   return base * height;
// }

// export function getTriangleArea(base: number, height: number): number {
//   return (base * height) / 2;
// }

// export function getPolygonPerimeter(sides: number[]): number {
//   return sides.reduce((acc, side) => acc + side, 0);
// }

// export function triangleCheck(
//   sideA: number,
//   sideB: number,
//   sideC: number
// ): boolean {
//   const checkSideA = (sideB - sideC) < sideA && sideA < (sideB + sideC);
//   const checkSideB = (sideA - sideC) < sideB && sideB < (sideA + sideC);
//   const checkSideC = (sideA - sideB) < sideC && sideC < (sideA + sideB);
//   return checkSideA && checkSideB && checkSideC;
// }

export function getRhombusArea(D: number, d: number): number {
  return (d * D) / 2
}
```

```typescript
// ./index.ts

import * as Ex from './exercises';

console.log("A ÁREA DE UM:");
// ...

console.log(`- Losango com diagonais iguais a 32cm e 18cm: ${Ex.getRhombusArea(32, 18)}cm²`);
console.log(`- Losango com diagonais iguais a 200cm e 50cm: ${Ex.getRhombusArea(200, 50)}cm²`);
console.log(`- Losango com diagonais iguais a 75cm e 25cm: ${Ex.getRhombusArea(75, 25)}cm²`);
```

2.  Crie uma nova função para calcular a área de um trapézio. A área do trapézio é dada pelo produto da altura (h) com a soma da base maior (B) e a base menor (b) dividido por dois. `A = [(B + b) * h] / 2`

![Área do Trapézio](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20Trap%C3%A9zio.png)

Fórmula da Área de um Trapézio

-   Calcule a área de um trapézio que tem B = 100cm, b = 70cm e altura = 50cm;
-   Calcule a área de um trapézio que tem B = 75cm, b = 50cm e altura = 35cm;
-   Calcule a área de um trapézio que tem B = 150cm, b = 120cm e altura = 80cm.

```typescript
// ./exercise.ts
// ...

export function getTrapezoidArea(B: number, b: number, h: number): number {
  return ((B + b) * h) / 2
}
```


```typescript
// ./index.ts

import * as Ex from './exercises';

console.log("A ÁREA DE UM:");
// ...

console.log(`- Trapézio com base maior igual a 100cm, base menor igual a 70cm e altura igual a 50cm: ${Ex.getTrapezoidArea(100, 70, 50)}cm²`);
console.log(`- Trapézio com base maior igual a 75cm, base menor igual a 50cm e altura igual a 35cm: ${Ex.getTrapezoidArea(75, 50, 35)}cm²`);
console.log(`- Trapézio com base maior igual a 150cm, base menor igual a 120cm e altura igual a 80cm: ${Ex.getTrapezoidArea(150, 120, 80)}cm²`);
```

1.  Crie uma nova função para calcular a área de um círculo. A área do círculo de raio `r` é encontrada multiplicando o raio ao quadrado pelo número irracional ℼ (em geral utilizamos ℼ = 3,14). `A = ℼ * r²`. _Dica: você pode acessar o valor de ℼ utilizando o módulo nativo `Math.PI`_.

![Área do Círculo](https://content-assets.betrybe.com/prod/8d8210c9-f4e8-4697-95b7-19b673037fa6-%C3%81rea%20do%20C%C3%ADrculo.png)

Fórmula da Área de um Círculo

-   Calcule a área de um círculo de raio igual 25cm;
-   Calcule a área de um círculo de raio igual 100cm;
-   Calcule a área de um círculo de raio igual 12,5cm.

```typescript
// ./exercise.ts
// ...

export function getCircleArea(radius: number): number {
  return Math.PI * radius ** 2;
}
```

```typescript
// ./index.ts

import * as Ex from './exercises';

console.log("A ÁREA DE UM:");
// ...

console.log(`- Círculo de raio 10cm: ${Ex.getCircleArea(10)}cm²`);
console.log(`- Círculo de raio 5cm: ${Ex.getCircleArea(5)}cm²`);
console.log(`- Círculo de raio 100cm: ${Ex.getCircleArea(100)}cm²`);
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/4e3b7d3a-94a1-4fce-9545-0f2b04f8ccd9/day/f2bc13d9-91a6-488b-aa3f-257b0f5bb449/lesson/b3678856-c860-494c-8c6c-86de69071cca)
