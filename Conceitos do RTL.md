[[React Testing Library - RTL]]
[[Teste Assincrono]]
[[React]]


Antes de começar os estudos com testes automatizados, é importante entender que, para desenvolver um bom teste, você precisa pensar em _quais casos de uso_ deverão ser testados, e não _quais funções testar_.Você pode estar se perguntando: “ O que são **casos de uso**?” Citando o dicionário de Oxford (tradução livre) temos a resposta:

> Uma situação específica em que um produto ou serviço pode, potencialmente, ser usado. Pense nos projetos anteriores do curso. Por exemplo:

-   Em um e-commerce, uma pessoa pode filtrar por uma categoria, adicionar um produto ao carrinho e finalizar a compra. Isso é um caso de uso.
-   A pessoa pode, por outro lado, não filtrar por categoria alguma, adicionar vários produtos ao carrinho de uma vez, e não finalizar a compra. Isso é outro caso de uso.
-   Em um _to do list_, adicionar uma tarefa nova é um caso de uso.
-   Deletar uma tarefa é um caso de uso.
-   Marcar uma tarefa é um caso de uso.
-   Desmarcar uma tarefa é um caso de uso.

Agora está ficando mais evidente? Vamos entender se há ferramentas que podem nos auxiliar.

## Cobertura de Código e Cobertura com Testes Automatizados

O principal objetivo da **Cobertura de Código** (_code coverage_), ou **Cobertura de Testes** é evidenciar quais linhas do código foram testadas e quais não estão sendo exploradas nos testes. É importante salientar que um projeto com cobertura de código alta não significa necessariamente que os testes não podem melhorar: cobertura alta é somente o primeiro passo!

Existem diversos softwares que checam para nós a cobertura de código. Em linhas gerais, os resultados podem evidenciar:

-   a proporção de linhas do seu código que é executada;
-   se há linhas que “nunca” serão executadas - problemas com `if else`, por exemplo;
-   a quantidade de funções externas que é chamada;
-   blocos de código repetitivos e/ou códigos inalcançáveis.

Se o resultado nos mostra que há uma cobertura alta, podemos dizer que o código foi bastante testado e tem uma chance menor de conter erros, mas não diz nada sobre a qualidade do código, o que só pode ser medido pela **Cobertura dos Casos de Uso**.

### Casos de uso x Cobertura de código

Casos de uso são possibilidades de usos do sistema. Exemplo: quais passos a pessoa usuária precisa seguir para fazer um login no sistema e o que é esperado ao fim do login tanto no sucesso quanto na falha? E se a pessoa não digitar o user? Ou a senha? E se a senha estiver incorreta? Cada uma dessas situações é um **caso de uso diferente**. Mais importante do que garantir a cobertura do código, algo que já é crucial, é garantir que seus testes abordam todos os **casos de uso** da sua aplicação. Para isto, é preciso criar testes automatizados que simulam uma pessoa acessando a página, fazendo uma sequência de ações que resulta naquele caso de uso.

