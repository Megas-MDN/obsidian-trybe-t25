[[Banco de Dados]]

  
Atualmente, a análise de dados é indispensável para empresas e pessoas em processos de tomada de decisão. Essa é uma das maneiras mais eficientes de gerar conhecimento, tanto utilizando dados passados quanto fazendo projeções futuras.

Feita uma análise inicial dos dados, seus resultados serão transformados em _informações_ que, depois de estudadas, podem vir a gerar _conhecimentos_ que, por sua vez, se tornam uma vantagem competitiva para as empresas, além de um norte para decisões individuais.

Uma das formas de como nós, profissionais da tecnologia da informação, podemos contribuir para isso, é gerando e disponibilizando os dados necessários para análise. Isso pode ser feito através de tabelas e consultas criadas dentro de um **banco de dados**, utilizando a linguagem **SQL**.

![Diagrama front-end x back-end](https://content-assets.betrybe.com/prod/Diagrama%20front-end%20x%20back-end.png)

Para entendermos mais sobre como podemos gerenciar essas informações a nosso favor, precisamos entender um pouco sobre o fluxo de trabalho de uma pessoa desenvolvedora back-end que lida com banco de dados. Ele funciona assim:

O front-end faz a requisição para o back-end, o back-end faz a conexão e consulta o banco de dados. Então o banco retorna alguma informação para o back-end, e é aqui que a API (Application Programming Interface) trabalha. O back-end será responsável por processar essas informações, recebendo requisições, enviando respostas e, por sua vez, alimentando o front-end.

## O que é SQL?

**SQL** (_Structured Query Language_) é a linguagem mais usada para criar, pesquisar, extrair e também manipular dados dentro de um _banco de dados relacional_. Para que isso seja possível, existem comandos como o `SELECT`, `UPDATE`, `DELETE`, `INSERT` e `WHERE`, entre outros.

## Como essas informações (tabelas) são armazenadas?

Todas as pesquisas realizadas dentro de um banco de dados são feitas em tabelas. Tabelas possuem linhas e colunas. Linhas representam um exemplo, ou instância, daquilo que se deseja representar, ao passo que colunas descrevem algum aspecto da entidade representada.

Por exemplo, a imagem a seguir apresenta uma tabela com dados sobre pessoas. Cada linha na tabela representa uma pessoa específica. As colunas descrevem uma característica que queremos armazenar sobre as pessoas; nesse caso, são nome, sobrenome e email.

![Ilustração de linhas e colunas em uma tabela](https://content-assets.betrybe.com/prod/Ilustra%C3%A7%C3%A3o%20de%20linhas%20e%20colunas%20em%20uma%20tabela.png)


#### Recursos adicionais (opcional)

-   [Diferença entre dados, informação e conhecimento](https://www.estrategiaconcursos.com.br/blog/dados-informacao-conhecimento-uma-apresentacao)
-   [Importância dos bancos de dados na sociedade](https://tecnoblog.net/245120/banco-de-dados-importancia)
-   [O que é um banco de dados?](https://www.homehost.com.br/blog/tutoriais/mysql/o-que-e-um-banco-de-dados)
-   [Explicação e exercícios sobre tipos de chaves](https://www.blogson.com.br/chave-primaria-estrangeira-e-composta-no-mysql)
-   [SQL vs NoSQL, como são diferentes?](https://www.treinaweb.com.br/blog/sql-vs-nosql-qual-usar)
-   [Guia de Estilo SQL · SQL Style Guide](https://www.sqlstyle.guide/pt-br/)
-   [Instalação do MySQL de forma nativa (sem o uso do docker)](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/a924acf1-0d61-4d28-a8c3-54b73e673d27/lesson/43613abe-be7b-4ab4-aec3-40c036b4fcd0)
-   [Introdução ao básico do SQL com prática](https://sqlzoo.net/wiki/SELECT_basics)
-   [W3Schools - Curso SQL online](https://www.w3schools.com/sql/)
-   [Documentação Oficial MySQL](https://dev.mysql.com/doc/refman/8.0/en/)
-   [Tutorial sobre tipos de comando SQL do W3Schools](https://www.w3schools.in/mysql/ddl-dml-dcl/)
-   [Tutorial sobre tipos de comando SQL do Java T Point](https://www.javatpoint.com/dbms-sql-command)
-   [Quiz prêmio nobel com MySQL](https://sqlzoo.net/wiki/Nobel_Quiz)
-   [Desafios do HackerRank sobre conhecimentos básicos](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=select)
-   [Lidando com datas no MySQL](https://popsql.com/learn-sql/mysql/how-to-query-date-and-time-in-mysql/)
-   [Recursos para aprender e praticar SQL](https://www.w3resource.com/mysql/mysql-tutorials.php)
-   [Dates are more troublesome than they seem!](https://www.youtube.com/watch?v=-5wpm-gesOY)
-   [Tutorial sobre `INSERT` do Guru99](https://www.guru99.com/insert-into.html)
-   [Tutorial sobre `INSERT` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-insert-statement.aspx)
-   [Tutorial sobre `UPDATE` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-update-data.aspx)
-   [Tutorial sobre `DELETE` e `UPDATE` do Guru99](https://www.guru99.com/delete-and-update.html)
-   [Tutorial sobre `DELETE` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-delete-statement.aspx)
-   [Tutorial sobre `DELETE` do Tech On The Net](https://www.techonthenet.com/mysql/delete.php)
-   [Documentação sobre restrições de chaves estrangeiras no MySQL](https://dev.mysql.com/doc/refman/5.7/en/create-table-foreign-keys.html)
-   [Como utilizar `INNER JOIN`, `LEFT LEFT` e `RIGHT JOIN`, por Dev Media](https://www.devmedia.com.br/clausulas-inner-join-left-join-e-right-join-no-sql-server/18930)
-   [Entenda mais sobre o `INNER JOIN` no MySQLTutorial](https://www.mysqltutorial.org/mysql-inner-join.aspx)
-   Aprenda SQL `JOINS` na prática com o [SQL Bolt](https://sqlbolt.com/lesson/select_queries_with_joins)
-   Maneiras diferentes de otimizar suas _queries_ neste [link](https://dev.mysql.com/doc/refman/8.0/en/optimization.html)
-   Para mais exercícios de fixação sobre SQL em geral, acesse esse [repositório](https://github.com/XD-DENG/SQL-exercise) e siga o READ ME.
-   [Algumas ferramentas gratuitas para modelagem de tabelas](https://www.holistics.io/blog/top-5-free-database-diagram-design-tools/)
-   [Data Science](https://www.linkedin.com/jobs/data-scientist-vagas/?originalSubdomain=br)
-   [Boas práticas na criação de tabelas.](https://www.devmedia.com.br/padronizacao-de-nomenclatura-revista-sql-magazine-100/24710)
-   [Modelo ER e Diagrama ER](https://www.devmedia.com.br/modelo-entidade-relacionamento-mer-e-diagrama-entidade-relacionamento-der/14332)
-   [Como modelar um banco de dados gratuitamente através do **draw.io**](https://drawio-app.com/entity-relationship-diagram-erd/)
-   [SQL Data Types](https://www.w3schools.com/sql/sql_datatypes.asp)
-   [MySQL Data Types](https://www.mysqltutorial.org/mysql-data-types.aspx)
-   [Quando é recomendado uso de chave primária composta](https://pt.stackoverflow.com/questions/15883/quando-%C3%A9-recomendado-o-uso-de-chave-prim%C3%A1ria-composta)
-   [Normalização em Bancos de Dados - Diego Machado](https://medium.com/@diegobmachado/normaliza%C3%A7%C3%A3o-em-banco-de-dados-5647cdf84a12)
-   [Conceitos Gerais sobre normalização](https://www.luis.blog.br/normalizacao-de-dados-e-as-formas-normais.html)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/695be3a1-74b5-4c1d-9381-b3655397a00f)

