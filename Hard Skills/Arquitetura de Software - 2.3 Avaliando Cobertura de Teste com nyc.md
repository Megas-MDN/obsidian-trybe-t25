[[Arquitetura de Software]]
[[Arquitetura de Software - 2 Camada Model]]


Na lição anterior vimos como implementar algumas funções do nosso componente model e alguns testes para essas funções.🤔 _**Porém, você pode estar se perguntando:**_ como saber se os cenários de testes criados são suficientes para minha aplicação?!

**Resposta:** O primeiro parâmetro a ser observado são as regras de negócios. Idealmente, todos os fluxos possíveis de uma função devem ser verificados por ao menos um teste. Contudo existem outros fatores que podem nos guiar para definir a quantidade de testes desejáveis para a nossa aplicação. Dentre eles, a cobertura de código (% de código executado durante o teste) serve para nos guiar durante a concepção dos testes.

Para nos ajudar com essa avaliação da porcentagem de código executado, podemos usar o módulo `nyc` que fornece um relatório de cobertura de teste do seu código após a execução dos testes. Para isso, já temos instalado o módulo `nyc`. Para instalar em outros projetos usando o **npm** você pode usar o seguinte comando:

Copiar

```bash
npm install -D -E nyc@15.1.0
```

Além disso, é necessário adicionar um script para facilitar a chamada do comando `nyc` que faz a cobertura de teste. Esse ajuste já está presente no projeto Trybecar, mas caso queira replicar em outros projetos adicione o seguinte script no `package.json`.

Copiar

```json
"scripts": {
    "test:coverage": "nyc --all --include src/models --include src/services --include src/controllers mocha tests/unit/**/*.js --exit"
  },
```

No trecho acima, já deixamos pronto para o nyc avaliar a cobertura de testes dos diretórios da camada Model, Controller e Services (`--include src/models --include src/services --include src/controllers`) e para fazer a cobertura de testes baseado no teste do mocha (`mocha tests/unit/**/*.js --exit`).

Feito isso, você já pode executar os seus testes verificando a cobertura de código.

```bash
npm run test:coverage
```

Para entendermos melhor o resultado que aparece no nosso terminal, vamos explorar o seguinte resultado de executar o comando antes de implementar os testes da função `insert` da nossa `passenger.model`:

![Resultado antes de implementar os testes](https://content-assets.betrybe.com/prod/6225ee56-655b-4c69-8e05-e8ea0081df76-Resultado%20antes%20de%20implementar%20os%20testes.png)

Resultado antes de implementar os testes

A tabela traz as porcentagem de **código do programa que foi executado ao rodar os testes**. para cada coluna temos:

-   `File`: nome do arquivo do projeto.
-   `Stmts`: instruções do código.
-   `Branch`: estruturas de controle (por exemplo: ramificações de uma estrutura if/else).
-   `Funcs`: funções, métodos ou sub-rotinas.
-   `Lines`: linha do arquivo.

As informações mais importantes que conseguimos tirar dessa tabela são:

-   Na coluna `% Stmts` temos a informação da porcentagem de instruções, do respectivo arquivo, que foram cobertos pelo teste.

> De olho na dica 👀: este valor é utilizado pelo avaliador para definir se um requisito do projeto foi aprovado ou não.

-   Na coluna `% Lines` (porcentagem de linhas de código) da linha `All files`(todos os arquivos) temos a informação do total de número de linhas da nossa aplicação que nossos testes estão cobrindo, nesse caso `76,19%`
-   Na coluna `Uncovered Line #s` (número das linhas de códigos que não estão cobertas) da linha `passenger.model.js` temos a informação de exatamente quais são as linhas de código do arquivo `passenger.model.js` que ainda não estão cobertas, nesse caso o intervalo começando na linha `21` e indo até a linha `32` representado por `21-32`

![Resultado depois de implementar os testes](https://content-assets.betrybe.com/prod/6225ee56-655b-4c69-8e05-e8ea0081df76-Resultado%20depois%20de%20implementar%20os%20testes.png)

Resultado depois de implementar os testes

Perceba que após implementado o teste para a função `insert` os valores agora estão todos em `100` pois agora temos cobertura total do nosso código.

Agora é hora de começar o processo de refatoração das funcionalidades já existentes no projeto TrybeCar para utilizar a camada **Model**.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/e3b85ab5-cb8d-422b-873d-5ba7ec8a2d83)
