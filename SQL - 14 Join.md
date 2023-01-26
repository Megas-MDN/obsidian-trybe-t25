[[Banco de Dados]]
[[SQL]]

[INNER JOIN](#INNER%0dJOIN)
[LEFT e RIGHT JOIN](#LEFT%0de%0dRIGHT%0dJOIN)
[SELF JOIN](#SELF%0dJOIN)


# O que é um `JOIN`?

Até o momento, você já criou consultas para filtrar, ordenar, selecionar, alterar, agrupar, inserir e apagar dados armazenados nas tabelas dos seus bancos de dados. Cada consulta, no entanto, sempre acessava apenas uma tabela.

Em alguns casos, uma tabela pode não possuir toda a informação necessária. Em função disso, existe a opção de usar os diversos tipos de `JOIN` para combinar em um mesmo resultado registros de duas ou mais tabelas. Esses tipos são: `INNER JOIN`, `LEFT JOIN` e `RIGHT JOIN`, para combinar duas ou mais tabelas, e `SELF JOIN`, quando uma tabela precisa ser combinada consigo mesma. Você verá detalhes de cada um desses tipos de `JOIN` a seguir.

![O que o banco pensa quando você diz `JOIN`](https://content-assets.betrybe.com/prod/O%20que%20o%20banco%20pensa%20quando%20voc%C3%AA%20diz%20%60JOIN%60.gif)

O que o banco pensa quando você diz `JOIN`

# `INNER JOIN`

`INNER JOIN` permite retornar todos os resultados em que a condição da cláusula `ON` for satisfeita. A sintaxe de um `INNER JOIN` é a seguinte:


```sql
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
```

Veja uma representação visual do `INNER JOIN` abaixo:

![Innerjoin](https://content-assets.betrybe.com/prod/Innerjoin.png)

INNER JOIN

## Por que usamos o _alias_ (`AS`)?

O _alias_ `AS` é usado para apelidar qualquer parte da sua _query_. Isso ajuda o sistema de banco de dados a identificar a qual coluna estamos nos referindo, evitando erros de ambiguidade de nome de colunas, além de tornar suas _queries_ mais concisas e legíveis.

Por exemplo, observe as _queries_ a seguir:

**Código sem** `alias`

```sql
SELECT sakila.actor.first_name, actor_id, sakila.film_actor.actor_id
FROM sakila.actor
INNER JOIN sakila.film_actor
ON sakila.actor.actor_id = sakila.film_actor.actor_id;
```

O código acima, além de ser muito extenso, não permite que o banco de dados descubra de qual tabela deve trazer o `actor_id`, uma vez que ambas as tabelas, `actor` e `filme_actor`, possuem uma coluna `actor_id`. O seguinte erro será gerado ao tentar executar essa _query_:

![Erro de ambiguidade de coluna](https://content-assets.betrybe.com/prod/Erro%20de%20ambiguidade%20de%20coluna.png)

Erro de ambiguidade de coluna

**Código com** `alias`

Podemos tornar a _query_ mais legível com um _alias_, além de evitar o erro de ambiguidade de coluna:

```sql
SELECT a.first_name, a.actor_id, f.actor_id
FROM sakila.actor AS a
INNER JOIN sakila.film_actor AS f
ON a.actor_id = f.actor_id;
```

**OBS.:** A palavra-chave `AS` pode ser omitida. Nesse caso, o _alias_ é passado diretamente, após o nome da tabela:

```sql
SELECT a.first_name, a.actor_id, f.actor_id
FROM sakila.actor a
INNER JOIN sakila.film_actor f
ON a.actor_id = f.actor_id;
```

## Dicas sobre como escolher o tamanho do _alias_

Sua _query_ é composta de poucas linhas? Então use apenas letras ou a primeira sílaba para representar a coluna. Por exemplo, **“actor”** se tornaria **“A”** ou **“act”**.

Caso esteja montando `JOINS` com muitas linhas, é recomendado usar um _alias_ mais descritivo para tornar a leitura e interpretação da _query_ mais simples.

![Ok, Linus, it](https://content-assets.betrybe.com/prod/Ok,%20Linus,%20it.jpeg)
> Ok, Linus, it


# `LEFT` e `RIGHT JOIN`

Você precisa encontrar um conjunto de registros, mas não tem certeza se uma das colunas de referência envolvidas possui ou não essa informação. Para que você encontre registros nessa situação, podemos usar o `LEFT JOIN` ou `RIGHT JOIN`.

O conceito de `JOIN` pode levar um certo tempo para ser compreendido. Sendo assim, vá no seu ritmo, reveja o conteúdo deste dia quantas vezes forem necessárias para compreender bem esse conceito. Pense em perguntas que você gostaria de responder sobre algum de seus bancos de dados que utilizem dados de mais de uma tabela. Abra o **Workbench** e tente fazer uma _query_ que responda a elas.

## Três _queries_ e uma pergunta

Vamos visualizar a diferença entre os três joins já vistos até o momento. Rode e analise cada uma das três _queries_ a seguir. Busque notar a diferença entre as colunas da direita e da esquerda e a quantidade de dados retornados em cada _query_, como foi mostrado no vídeo. Gaste de dois a cinco minutos aqui e depois continue.

`LEFT JOIN`
```SQL
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
INNER JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
```

`RIGHT JOIN`
```SQL
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
RIGHT JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
```


`INNER JOIN`
```SQL
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
INNER JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
```


## Notando as diferenças

Depois de ter analisado as _queries_ acima, note que, de fato, a única diferença entre os três joins é a questão do foco. Vamos explorar essa ideia a seguir.

**LEFT JOIN**: quando utilizamos o `LEFT JOIN`, focamos a tabela da esquerda. São retornados todos os registros da tabela da esquerda e valores correspondentes da tabela da direita, **caso existam**. Valores que não possuem correspondentes são exibidos como nulos.

Veja uma representação visual do `LEFT JOIN` abaixo:


![leftjoin](https://content-assets.betrybe.com/prod/leftjoin.png)















> LEFT JOIN.


**RIGHT JOIN**: quando utilizamos o `RIGHT JOIN`, focamos a tabela da direita. São retornados todos os registros da tabela da direita e valores correspondentes da tabela da esquerda, **caso existam**. Valores que não possuem correspondentes são exibidos como nulos.

Veja uma representação visual do `RIGHT JOIN` abaixo:

![[Pasted image 20230125014041.png]]

> RIGHT JOIN.


**INNER JOIN**: finalmente, temos o `INNER JOIN`, que foca em trazer somente os registros que possuem valores correspondentes **em ambas as tabelas**.

Novamente, você pode ver uma representação visual do `INNER JOIN` abaixo:

![[Pasted image 20230125014151.png]]
> INNER JOIN.


Até o momento, temos usado mais de uma tabela para analisar dados e gerar informação. No entanto, a informação a ser analisada pode estar concentrada em apenas uma tabela. Nesse cenário, o `SELF JOIN` pode ser usado para criar resultados relevantes.

# `SELF JOIN`


Há certos cenários nos quais faz sentido pesquisar e tirar alguma conclusão analisando apenas uma única tabela. Os tipos de `JOIN` que você viu até agora precisam necessariamente que mais de uma tabela seja incluída em uma _query_ para que um resultado possa ser gerado. O `SELF JOIN` não possui esse requisito. Vamos ver a seguir algumas das aplicações do `SELF JOIN`.

É possível fazer pesquisas e comparações dentro da própria tabela através do `SELF JOIN`. Lembre-se dessa opção sempre que a informação que você precisa filtrar ou comparar para encontrar algo estiver em uma única tabela.

Note que um `SELF JOIN` não é um tipo diferente de `JOIN`. É apenas um caso em que uma tabela faz join consigo mesma. Você pode utilizar qualquer dos tipos de `JOIN` vistos ao realizar um `SELF JOIN`.

Utilizando o schema `hr` como exemplo, se quisermos buscar o nome das pessoas colaboradoras e das respectivas gerências (`manager`), podemos montar a seguinte _query_ usando `SELF JOIN`:

```sql
SELECT
    CONCAT(Employee.first_name, " ", Employee.last_name) AS "Nome da Pessoa Colaboradora",
    CONCAT(Manager.first_name, " ", Manager.last_name) AS "Nome Gerente"
FROM
    employees AS Employee
INNER JOIN
    employees AS Manager ON Employee.manager_id = Manager.employee_id;
```


#### Recursos adicionais (opcional)

-   [Como utilizar `INNER JOIN`, `LEFT LEFT` e `RIGHT JOIN`, por Dev Media](https://www.devmedia.com.br/clausulas-inner-join-left-join-e-right-join-no-sql-server/18930)
-   [Entenda mais sobre o `INNER JOIN` no MySQLTutorial](https://www.mysqltutorial.org/mysql-inner-join.aspx)
-   Aprenda SQL `JOINS` na prática com o [SQL Bolt](https://sqlbolt.com/lesson/select_queries_with_joins)
-   Maneiras diferentes de otimizar suas _queries_ neste [link](https://dev.mysql.com/doc/refman/8.0/en/optimization.html)
-   Para mais exercícios de fixação sobre SQL em geral, acesse esse [repositório](https://github.com/XD-DENG/SQL-exercise) e siga o READ ME.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/783f9e5d-06b1-485e-9268-7df42aa26324/lesson/19cc3526-3dab-42f4-8daa-5307275a2f23)