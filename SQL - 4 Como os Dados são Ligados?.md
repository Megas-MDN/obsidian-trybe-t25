[[Banco de Dados]]
[[SQL]]


Em um banco de dados é comum termos diferentes tabelas, cada uma armazenando seus respectivos dados, mas que em conjunto tem um significado maior. No exemplo da sorveteria, poderíamos ter outras 2 tabelas que se relacionariam com a tabela de sabores: empresas fornecedoras e pedidos.

Para não precisarmos duplicar dados em tabelas diferentes, podemos estabelecer **relacionamentos** entre as tabelas. Em um banco de dados existem quatro tipos de relacionamento.

## Um para Um

Uma linha da Tabela **A** só deve possuir uma linha correspondente na tabela **B** ou vice-versa.

![Exemplo de relacionamento um para um](https://content-assets.betrybe.com/prod/540f5ea1-c92d-4c67-9374-3fc972823bf4-Exemplo%20de%20relacionamento%20um%20para%20um.png)

Na imagem acima, um empregado só pode estar relacionado a um pagamento, e um pagamento deve estar relacionado a apenas um empregado.

Apesar de ser possível inserir essas informações em apenas uma tabela, esse tipo de relacionamento é usado normalmente quando se quer dividir as informações de uma tabela maior em tabelas menores por questões de organização e normalização (veremos isso logo mais. Isso evita ter tabelas com dezenas de colunas, ou por várias outras questões específicas de um negócio. Pode ser encontrado em alguns conteúdos com a abreviação: **1:1** _(um para um)_.

## Um para Muitos ou Muitos para Um

Esse é um dos tipos mais comuns de relacionamento. Em cenários assim, uma linha na tabela **A** pode ter várias linhas correspondentes na tabela **B**, mas uma linha da tabela **B** só pode possuir uma linha correspondente na tabela **A**.

![Exemplo de relacionamento um para muitos ou muitos para um](https://content-assets.betrybe.com/prod/540f5ea1-c92d-4c67-9374-3fc972823bf4-Exemplo%20de%20relacionamento%20um%20para%20muitos%20ou%20muitos%20para%20um.png)

Na imagem acima, uma categoria pode estar ligada a vários livros; porém um livro deve possuir apenas uma categoria. Pode ser encontrado em alguns conteúdos com a abreviação: **N:1** _(muitos para um)_ ou **1:N** _(um para muitos)_ dependendo da regra de negócio.

## Muitos para Muitos

O tipo de relacionamento muitos para muitos acontece quando uma linha na tabela **A** pode possuir muitas linhas correspondentes na tabela **B** e vice-versa.

![Exemplo de relacionamento muitos para muitos](https://content-assets.betrybe.com/prod/540f5ea1-c92d-4c67-9374-3fc972823bf4-Exemplo%20de%20relacionamento%20muitos%20para%20muitos.png)

O relacionamento muitos para muitos pode ser visto também como dois relacionamentos um para muitos ligados por uma tabela intermediária, como é o caso da tabela `film_actor` do banco `sakila` demonstrada acima. Note que nesse caso a tabela `film_actor` possui `actor_id` e `film_id`, dessa forma, ela serve como uma tabela auxiliar, também chamada de **tabela de junção** que relaciona as tabelas `actor` e `film`. Esse tipo de relacionamento também pode ser chamado de _um para muitos ligados por um tabela intermediária_.

Dessa maneira, quando queremos demostrar que um filme pode contar com vários atores, e também que os atores podem atuar em vários filmes, surge a necessidade de um relacionamento muitos para muitos. Pode ser encontrado em alguns conteúdos com a abreviação: **N:N** _(muitos para muitos)_.

#### Recusos adicionais:

-   [Diferença entre dados, informação e conhecimento](https://www.estrategiaconcursos.com.br/blog/dados-informacao-conhecimento-uma-apresentacao)
-   [Importância dos bancos de dados na sociedade](https://tecnoblog.net/245120/banco-de-dados-importancia)
-   [O que é um banco de dados?](https://www.homehost.com.br/blog/tutoriais/mysql/o-que-e-um-banco-de-dados)
-   [Explicação e exercícios sobre tipos de chaves](https://www.blogson.com.br/chave-primaria-estrangeira-e-composta-no-mysql)
-   [SQL vs NoSQL, como são diferentes?](https://www.treinaweb.com.br/blog/sql-vs-nosql-qual-usar)
-   [Guia de Estilo SQL · SQL Style Guide](https://www.sqlstyle.guide/pt-br/)
-   [Instalação do MySQL de forma nativa (sem o uso do docker)](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/a924acf1-0d61-4d28-a8c3-54b73e673d27/lesson/43613abe-be7b-4ab4-aec3-40c036b4fcd0)

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/96f162a4-b0dc-4135-9933-07dd1bcffa03)
