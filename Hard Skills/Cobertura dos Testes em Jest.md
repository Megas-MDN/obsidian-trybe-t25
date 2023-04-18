[[Jest]]
[[Testes com Jest]]

Após escrever uma quantidade de testes, você pode rodar a cobertura de testes através do comando:

```bash
npm test -- --coverage
```

Esse comando faz um levantamento de quanto do código está sendo coberto pelos testes escritos. Após executar o comando, você deve receber como retorno uma tabela similar à tabela abaixo:
![[Pasted image 20221024015437.png]]

A partir da tabela, você tem informações sobre a quantidade de testes que está coberta por testes e como completar a cobertura desenvolvendo testes para a parte que ainda não está coberta. As colunas da tabela trazem as seguintes informações:

-   **Files**: Lista os arquivos testados pelo _jest_.
-   **% Stmts**: Exibe a porcentagem de declarações (_statements_) cobertas pelos testes.
-   **% Branch**: Exibe a porcentagem coberta dos diferentes caminhos por onde o código pode seguir. Por exemplo, no caso de estruturas condicionais, como _if_, calcula se há teste para o caso _verdadeiro_ e para o caso _falso_ da condição.
-   **% Funcs**: Exibe a porcentagem das funções cobertas pelos testes.
-   **% Lines**: Exibe a porcentagem de linhas cobertas pelos testes.
-   **Uncovered Line #s**: Exibe os números das linhas ainda não cobertas pelos testes.

A partir da informação de quais linhas não estão cobertas pelos testes, é possível escrever os testes que faltam para cobrir todo o código.

Caso queira uma visualização mais amigável, após executar o comando para calcular a cobertura de testes, uma pasta _“coverage”_ é criada com as informações de cobertura de testes. Dentro dessa pasta, há uma pasta _“lcov_report”_, que contém um arquivo _index.html_ com uma visualização dos dados da tabela e ainda exibe o código testado, marcando as linhas ainda não cobertas pelos testes.

![[Pasted image 20221024015508.png]]

**Importante:** Uma cobertura de testes sobre 100% do código-fonte não quer dizer, necessariamente, que os seus testes são suficientes para atestar o correto funcionamento do código. Significa, apenas, que existem testes escritos para todas as linhas. Para fazer testes de forma completa, você precisa assegurar que seus testes cobrem as diferentes situações que podem ocorrer com seu código.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/131a8311-a3d9-4404-ae50-2ea6c971f5d8/day/38734d31-b185-4754-bb62-df9746262898/lesson/a15b0fe5-63c4-49bb-839f-bf743bdebf8b)
