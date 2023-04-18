[[JavaScript]]

# Introdução (O que é TypeScript?)

**TypeScript** é uma linguagem de programação de código aberto desenvolvida pela **_Microsoft_**. Ela é um **_superconjunto (superset) do JavaScript_**, isso significa que você poderá continuar utilizando todo o conhecimento adquirido até agora em **_JavaScript_** para desenvolver em **TypeScript**. Isso é sensacional, não é? 🤓

Especificamente, o **TypeScript** é um superconjunto do **_ECMAScript 2015_**, mais comumente denominado **_ECMAScript 6 ou ES6_**. Sendo assim, todo o código **_JavaScript_** também é código **TypeScript**, e um programa desenvolvido em **TypeScript** pode consumir o **_JavaScript_** de forma direta. É de explodir a mente! 🤯

## Por que a linguagem TypeScript foi criada?

**_JavaScript_** é, hoje, a linguagem oficial da Web, sendo utilizada para criar aplicações multiplataforma que rodam tanto no navegador quanto em servidores, e até mesmo em dispositivos mobile e IoT (_Internet of Things_ - internet das coisas). No entanto, ela tem uma limitação: não foi concebida para a criação de aplicativos envolvendo milhares ou até mesmo milhões de linhas de código, pois ela não possui alguns dos recursos presentes em outras linguagens.

A linguagem **TypeScript** foi desenvolvida justamente para resolver as limitações do **_JavaScript_**, sem prejudicar sua capacidade de executar código em todas as plataformas.


# Tipagem (dicas de tipo)

O grande recurso do **TypeScript** é o sistema de tipos. Em **TypeScript** podemos identificar o tipo de dado em variáveis, parâmetros ou retornos de funções utilizando a **_tipagem_**.

**_Tipagem_**, também conhecida como **_dicas de tipos_**, é a forma que utilizamos para descrever de qual tipo será o valor de um componente do nosso código - por exemplo: variáveis, expressões, funções ou módulos. Isso proporciona uma melhor documentação do código e permite que o **TypeScript** valide se ele está funcionando da maneira correta.

Antes de avançarmos para **como** o **TypeScript** faz isso, vamos falar um pouco mais sobre tipagem em linguagens de programação.

Podemos categorizar a tipagem em uma linguagem de programação como:

## Tipagem Estática:

Não permite que a pessoa desenvolvedora altere o tipo após ele ser declarado e, geralmente, a verificação de tipo é feita em tempo de compilação.

✅ A tipagem utilizada na linguagem **TypeScript** tem essa característica e vamos aprender sobre o seu **_compilador_** mais à frente.

## Tipagem Dinâmica:

Está ligada à habilidade da linguagem de programação em “escolher o tipo de dado” de acordo com o valor atribuído à variável em tempo de execução - ou seja, de forma dinâmica.

❌ Não há essa característica na tipagem do **TypeScript**.

## Tipagem Forte:

Linguagens fortemente tipadas não realizam conversões automaticamente. Melhor dizendo, não é possível realizar operações entre valores de diferentes tipos, sendo necessário que a pessoa desenvolvedora faça a conversão para um dos tipos, caso seja possível.

✅ A tipagem utilizada na linguagem **TypeScript** também possui essa característica.

## Tipagem Fraca:

A tipagem fraca tem a característica da linguagem de realizar conversões automáticas entre tipos diferentes de dados - ou melhor, operações entre valores de tipos diferentes podem ocorrer sem a necessidade de uma conversão explícita de tipo. Porém, o resultado pode não ser o esperado e erros podem ocorrer durante a execução.

❌ Não há essa característica na tipagem do **TypeScript**.

![Imagem que demonstra a tipagem do TypeScript](https://content-assets.betrybe.com/prod/Imagem%20que%20demonstra%20a%20tipagem%20do%20TypeScript.png)

Imagem que demonstra a tipagem do TypeScript

| Tipagem  | Significado                                                                                                      |
| -------- | ---------------------------------------------------------------------------------------------------------------- |
| Estática | Não permite que a pessoa desenvolvedora altere o tipo após ele ser declarado.                                    |
| Dinâmica | A linguagem de programação “escolhe” o tipo de dado a partir do valor atribuído à variável em tempo de execução. |
| Fraca    | Tipagem fraca tem a característica da linguagem realizar conversões automáticas entre tipos diferentes de dados. |
|     Forte     |           Linguagens fortemente tipadas não realizam conversões automaticamente.                                                                                                       |



## Inferência de tipo:

Algumas linguagens com tipagem estática podem fazer a inferência de tipo na declaração de variáveis, mas sem permitir que o tipo seja alterado após a declaração.

O **TypeScript** é uma dessas linguagens. Podemos usar a inferência de tipo, mas o compilador apresenta um erro quando tentamos atribuir um valor de tipo diferente à variável. Isso porque ele apenas realiza a inferência do tipo inicial da variável. Depois disso, como a linguagem possui tipagem estática, não é possível alterar o tipo.

Então, **TypeScript** é uma linguagem **_fortemente tipada_** e **_estaticamente tipada_** que possui **_inferência de tipo_**. Veremos exemplos disso quando começarmos a escrever nossas primeiras linhas de código nas seções a seguir.

Antes disso, vamos falar sobre **Transpiladores** e **Compiladores**, e sobre o **TSC**, que é o compilador do **TypeScript**.


# Recursos adicionais (opcional)

-   [Unicamp - Compiladores](https://www.dca.fee.unicamp.br/cursos/EA876/apostila/HTML/node37.html#:~:text=Um%20compilador%20%C3%A9%20um%20programa,de%20m%C3%A1quina%20para%20um%20processador.&text=O%20programa%20em%20linguagem%20simb%C3%B3lica,de%20m%C3%A1quina%20atrav%C3%A9s%20de%20montadores.)
-   [Código Fonte TV - Compiladores](https://www.youtube.com/watch?v=afUiVvDUIRA)
-   [Wikiqube - Compilador fonte a fonte (Transpilador)](https://pt.wikiqube.net/wiki/source-to-source_compiler)
-   [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
-   [Microsoft Docs - Introdução ao TypeScript](https://docs.microsoft.com/pt-br/learn/modules/typescript-get-started/)
-   [Introdução às referências do TSConfig](https://www.typescriptlang.org/pt/tsconfig)

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/4e3b7d3a-94a1-4fce-9545-0f2b04f8ccd9/day/f2bc13d9-91a6-488b-aa3f-257b0f5bb449/lesson/401bf387-b3f5-4278-b8b2-6d4f59708fa4)
