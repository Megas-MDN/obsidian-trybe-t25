[[Banco de Dados]]
[[SQL]]

Os resultados de uma _query_ podem ser agrupados por uma ou mais colunas usando o `GROUP BY`, o que faz com que todos os registros que têm o mesmo valor para tais colunas sejam exibidos juntos. O `GROUP BY` também pode ser usado em conjunto com as funções de agregação que vimos anteriormente.

O `GROUP BY` pode ser construído da seguinte forma:

```sql
SELECT coluna(s) FROM tabela
GROUP BY coluna(s);
```

Podemos utilizar o `GROUP BY` para agrupar os registros pelo valor de uma coluna, exibindo apenas um registro de cada valor, como é feito com a coluna `first_name` a seguir.

```sql
SELECT first_name FROM sakila.actor
GROUP BY first_name;
```

![groupby2 sakila actor](https://content-assets.betrybe.com/prod/groupby2%20sakila%20actor.png)

Tabela sakila.actor

Se você executar a _query_ anterior no seu banco de dados `sakila`, verá que são retornados 128 resultados. Porém, se retirar o `GROUP BY`, como na _query_ abaixo, notará que existem 200 registros na tabela `actor`. Isso acontece pelo fato de ele agrupar todos os registros que possuem o mesmo `first_name`, evitando duplicações na hora de retornar os dados.

```sql
SELECT first_name FROM sakila.actor;
```

Como dito, o `GROUP BY` removerá duplicações, retornando apenas um valor da coluna usada no agrupamento.

Porém, é mais comum utilizar o `GROUP BY` em conjunto com o `AVG`, `MIN`, `MAX`, `SUM` ou `COUNT`. Por exemplo, caso queiramos saber quantos registros existem na tabela de cada nome registrado, podemos usar o `COUNT()`. Assim, teremos uma informação mais fácil de ser compreendida.

```sql
SELECT first_name, COUNT(*) FROM sakila.actor
GROUP BY first_name;
```

![Tabela sakila actor groupby1](https://content-assets.betrybe.com/prod/Tabela%20sakila%20actor%20groupby1.png)

Tabela sakila.actor

Também podemos utilizar o `GROUP BY` para agrupar os registros pelos valores de mais de uma coluna.

```sql
SELECT rating, rental_rate, COUNT(1) as total FROM sakila.film
GROUP BY rating, rental_rate 
ORDER BY rating, rental_rate;
```

No exemplo acima, estamos usando a tabela `film` do banco `sakila`. A coluna `rating` nos mostra a classificação por idade do filme. A coluna `rental_rating` informa o valor do aluguel do filme separado/agrupado pela classificação. Além disso, inserimos uma função `ORDER BY` para facilitar a visualização dos resultados.

![Tabela sakila actor groupby1](https://content-assets.betrybe.com/prod/949fcc25-cc9c-4593-a753-e11e81640f11-Tabela%20sakila%20actor%20groupby1.png)

Tabela sakila.film

Agora vamos explorar como utilizar o `GROUP BY` em conjunto com as diversas funções de agregação que foram estudadas até aqui, por meio de alguns exemplos feitos com o nosso banco de dados `sakila`.

```sql
-- Média de duração de filmes agrupados por classificação indicativa
SELECT rating, AVG(length)
FROM sakila.film
GROUP BY rating;

-- Valor mínimo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MIN(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Valor máximo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MAX(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Custo total de substituição de filmes agrupados por classificação indicativa
SELECT rating, SUM(replacement_cost)
FROM sakila.film
GROUP by rating;
```

![Média de duração dos filmes por classificação indicativa](https://content-assets.betrybe.com/prod/M%C3%A9dia%20de%20dura%C3%A7%C3%A3o%20dos%20filmes%20por%20classifica%C3%A7%C3%A3o%20indicativa.png)

Média de duração dos filmes por classificação indicativa

![Valores mínimos de substituição dos filmes por classificação indicativa](https://content-assets.betrybe.com/prod/Valores%20m%C3%ADnimos%20de%20substitui%C3%A7%C3%A3o%20dos%20filmes%20por%20classifica%C3%A7%C3%A3o%20indicativa.png)

Valores mínimos de substituição dos filmes por classificação indicativa

![Valores máximos de substituição dos filmes por classificação indicativa](https://content-assets.betrybe.com/prod/Valores%20m%C3%A1ximos%20de%20substitui%C3%A7%C3%A3o%20dos%20filmes%20por%20classifica%C3%A7%C3%A3o%20indicativa.png)

Valores máximos de substituição dos filmes por classificação indicativa

![Soma total do custo de substituição dos filmes por classificação indicativa](https://content-assets.betrybe.com/prod/Soma%20total%20do%20custo%20de%20substitui%C3%A7%C3%A3o%20dos%20filmes%20por%20classifica%C3%A7%C3%A3o%20indicativa.png)

Soma total do custo de substituição dos filmes por classificação indicativa



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/6ead052e-46e3-4d96-a207-873325293189/lesson/51e575b4-9bb8-4b86-ad61-918d2c109ddd)

