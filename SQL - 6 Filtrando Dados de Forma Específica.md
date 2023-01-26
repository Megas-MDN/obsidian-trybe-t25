[[Banco de Dados]]
[[SQL]]

## `WHERE` - especificando resultados

![Ordem dos operadores](https://content-assets.betrybe.com/prod/Ordem%20dos%20operadores.png)

Ordem dos operadores

Sendo assim, quando se faz a seguinte _query_:

```sql
SELECT * FROM sakila.payment
WHERE amount = 0.99 OR amount = 2.99 AND staff_id = 2;
```

Como o operador `AND` tem preferência sobre o operador `OR`, ele é avaliado primeiro. Então os registros buscados são aqueles nos quais `amount = 2.99` e `staff_id = 2`. Na sequência, são buscados os registros nos quais `amount = 0.99`, independente do valor de `staff_id`. Os valores retornados serão os resultados dessas duas buscas. Ou seja, a _query_ é executada como se tivesse os seguintes parênteses: `amount = 0.99 OR (amount = 2.99 AND staff_id = 2)`.

Agora, quando executar a seguinte _query_:

```sql
SELECT * FROM sakila.payment
WHERE (amount = 0.99 OR amount = 2.99) AND staff_id = 2;
```

Primeiramente, a expressão dentro dos parênteses é avaliada, e todos os resultados que satisfazem a condição `amount = 0.99 OR amount = 2.99` são retornados. Na sequência, a expressão do lado direito do `AND` é avaliada, e todos os resultados que satisfazem a condição `staff = 2` são retornados. O `AND` então compara o resultado de ambos os lados e faz com que somente os resultados que satisfazem ambas as condições sejam retornados.

## Operadores booleanos e relacionais

Como foi exibido no vídeo anterior, de forma geral, temos os seguintes operadores:


```sql
-- OPERADOR - DESCRIÇÃO
=   IGUAL
>   MAIOR QUE
<   MENOR QUE
>=  MAIOR QUE OU IGUAL
<=  MENOR QUE OU IGUAL
<>  DIFERENTE DE
AND OPERADOR LÓGICO E
OR  OPERADOR LÓGICO OU
NOT NEGAÇÃO
IS  COMPARA COM VALORES BOOLEANOS (TRUE, FALSE, NULL)
```

**Dica final:** Sempre se atente a essa ordem de precedência para que consiga montar suas _queries_ de acordo com o que precisa. Na dúvida, use parênteses.


## `LIKE` - criando pesquisas mais dinâmicas

Você está tentando se lembrar do nome de um filme a que já assistiu, mas só se lembra de que ele terminava com `don` no nome. Como seria possível usar o `LIKE` para te ajudar a encontrá-lo?

```sql
SELECT * FROM sakila.film
WHERE title LIKE '%don';
```

![like1](https://content-assets.betrybe.com/prod/like1.png)

Resultado da pesquisa. Encontramos! O filme é

O `LIKE` é usado para buscar por meio de uma sequência específica de caracteres, como no exemplo acima. Além disso, dois “curingas”, ou modificadores, são normalmente usados com o `LIKE`:

-   **%** - O sinal de percentual, que pode representar zero, um ou múltiplos caracteres
    
-   **_** - O underscore (às vezes chamado de underline, no Brasil), que representa um único caractere
    

Vamos ver abaixo como usá-los (todos podem ser verificados no banco `sakila`)

```sql
SELECT * FROM sakila.film
WHERE title LIKE '%don';
```

![like_don](https://content-assets.betrybe.com/prod/like_don.png)

Resultado da pesquisa. Encontra qualquer resultado finalizando com

```sql
SELECT * FROM sakila.film
WHERE title LIKE 'plu%';
```

![like_plu](https://content-assets.betrybe.com/prod/like_plu.png)

Resultado da pesquisa. Encontra qualquer resultado iniciando com

```sql
SELECT * FROM sakila.film
WHERE title LIKE '%plu%';
```

![like_plu2](https://content-assets.betrybe.com/prod/like_plu2.png)

Resultado da pesquisa. Encontra qualquer resultado que contém

```sql
SELECT * FROM sakila.film
WHERE title LIKE 'p%r';
```

![like_pr](https://content-assets.betrybe.com/prod/like_pr.png)

Resultado da pesquisa. Encontra qualquer resultado que inicia com

```sql
SELECT * FROM sakila.film
WHERE title LIKE '_C%';
```

![like_c](https://content-assets.betrybe.com/prod/like_c.png)

Resultado da pesquisa. Encontra qualquer resultado em que o segundo caractere da frase é

```sql
SELECT * FROM sakila.film
WHERE title LIKE '________';
```

![like_eight](https://content-assets.betrybe.com/prod/like_eight.png)

Resultado da pesquisa. Encontra qualquer resultado em que o título possui exatamente 8 caracteres

```sql
SELECT * FROM sakila.film
WHERE title LIKE 'E__%';
```

![like_three](https://content-assets.betrybe.com/prod/like_three.png)
> Resultado da pesquisa. Encontra todas as palavras com no mínimo 3 caracteres e que iniciam com E.


## `IN` e `BETWEEN` - englobando uma faixa de resultados

## Operador `IN`

Como você viu no início do dia hoje, é possível juntar várias condições nas suas _queries_ usando os operadores `AND` e `OR`. No entanto, você ainda terá que digitar cada condição separadamente, como no exemplo a seguir:

```sql
SELECT * FROM sakila.actor
WHERE first_name = 'PENELOPE'
OR first_name = 'NICK'
OR first_name = 'ED'
OR first_name = 'JENNIFER';
```

Uma forma melhor de fazer essa mesma pesquisa seria usando o `IN`:

```sql
SELECT * FROM sakila.actor
WHERE first_name IN ('PENELOPE','NICK','ED','JENNIFER');
```

![Sqlin1](https://content-assets.betrybe.com/prod/Sqlin1.png)

Resultado da pesquisa usando o operador `IN`

Você poderia fazer esse mesmo processo para números também:

```sql
SELECT * FROM sakila.customer
WHERE customer_id IN (1, 2, 3, 4, 5);
```

![Sqlin2](https://content-assets.betrybe.com/prod/Resultado%20da%20pesquisa%20usando%20o%20operador%20%60IN%60.png)

Resultado da pesquisa usando o operador `IN`

Então, para que você faça pesquisas utilizando o `IN`, a sintaxe que deve ser usada é a seguinte:

```sql
SELECT * FROM banco_de_dados
WHERE coluna IN (valor1, valor2, valor3, valor4, ..., valorN);

-- ou também
SELECT * FROM banco_de_dados
WHERE coluna IN (expressão);
```

-   Como você faria, então, para encontrar, usando o `IN`, todos os detalhes sobre o aluguel dos clientes com os seguintes ids: 269, 239, 126, 399, 142? As informações podem ser encontradas na tabela `payment`.
-   Como encontraria todas as informações sobre os endereços que estão registrados nos distritos de QLD, Nagasaki, California, Attika, Mandalay, Nantou e Texas? As informações podem ser encontradas na tabela `address`.

## Operador `BETWEEN`

Uma outra opção quando queremos trabalhar com faixas de resultados é o `BETWEEN`, que torna possível fazer pesquisas dentro de uma faixa inicial e final.

```sql
expressão BETWEEN valor1 AND valor2;
-- a expressão é a sua query
-- e valor1 e valor2 delimitam o resultado
```

Então, quando você faz uma _query_ como essa, você terá o resultado da imagem a seguir:

```sql
-- Note que o MySQL inclui o valor inicial e o final nos resultados
 title, length FROM sakila.film
WHERE length BETWEEN 50 AND 120;
```

![Resultados abreviados usando `BETWEEN` com números](https://content-assets.betrybe.com/prod/Resultados%20abreviados%20usando%20%60BETWEEN%60%20com%20n%C3%BAmeros.png)

Resultados abreviados usando `BETWEEN` com números

## Usando o `BETWEEN` com strings

Para encontrar uma faixa de valores em que os valores são strings, podemos digitar a palavra por completo para encontrar os valores. Exemplo:


```sql
SELECT * FROM sakila.language
WHERE name BETWEEN 'Italian' AND 'Mandarin'
ORDER BY name;
```

## Usando o `BETWEEN` com datas

Para usar o `BETWEEN` com datas, basta que você digite o valor no formato padrão da data, que é `YYYY-MM-DD HH:MM:SS`, sendo os valores de horas, minutos e segundos opcionais. No exemplo abaixo, estamos filtrando os resultados para exibir o `rental_id` e `rental_date` apenas entre o mês 05 e o mês 07:

```sql
SELECT rental_id, rental_date FROM sakila.rental
WHERE rental_date
BETWEEN '2005-05-27' AND '2005-07-17';
```

![Resultados abreviados usando `BETWEEN` com datas](https://content-assets.betrybe.com/prod/Resultados%20abreviados%20usando%20%60BETWEEN%60%20com%20datas.png)

Resultados abreviados usando `BETWEEN` com datas

## Como decidir qual usar?

Lembre-se de que, no caso do `IN`, você precisa especificar os valores que devem ser incluídos no resultado e, no caso do `BETWEEN`, você não precisa incluir os valores que estão entre o valor inicial e final. Então, vale a pena analisar essa diferença e ver qual te atenderá melhor.

## Qual tem a melhor performance?

A melhor forma de responder a essa pergunta é: **depende**.

Não é o que você esperava? Então vai aqui uma resposta melhor: isso vai depender do tipo e quantidade de dados com os quais você está trabalhando. A melhor forma de você não chutar é clicar no botão _Execution Plan_ no **MySQL Workbench** e verificar o tempo de execução para tomar a decisão de qual tem o menor custo de execução - o que significa que a _query_ finalizará mais rápido.

Há outras ferramentas inteiras só para mensurar performance. Considere o _Execution Plan_ apenas uma introdução ao tema.

Fazendo um pequeno teste, temos os seguintes resultados (que podem sofrer alterações, dependendo da quantidade de dados com os quais se está trabalhando):

![Sqlin3](https://content-assets.betrybe.com/prod/Sqlin3.png)

Execution Plan usando `IN`. Custo total: 116.56

![sqlBetween2](https://content-assets.betrybe.com/prod/sqlBetween2.png)
> Execution Plan usando `BETWEEN`. Custo total: 125.36

No final das contas, depois de analisar questões como performance, você poderá tomar sua decisão sobre qual usar com mais segurança!


## Data e tempo - lidando com resultados temporais

No MySQL, o tipo `DATE` faz parte dos [tipos de dados](https://www.mysqltutorial.org/mysql-data-types.aspx) **temporais**, os quais vamos ver com mais detalhes no decorrer do curso. O **MySQL**, por padrão, usa o formato `YYYY-MM-DD` **(ano/mês/dia)** ao armazenar os valores de uma data. Você é obrigado, pelo banco de dados, a salvar nesse formato, e não é possível alterá-lo. Temos também o tipo `DATETIME`, que inclui informações de tempo. Vamos ver dois tipos comuns a seguir:

-   **_DATE_** - Possui apenas data, no formato `YYYY-MM-DD` na faixa de `1001-01-01` até `9999-12-31`
-   **_DATETIME_** - Possui data e tempo, no formato `YYYY-MM-DD HH:MM:SS` com a faixa de `1000-01-01 00:00:00` até `9999-12-31 23:59:59`.

Se você pesquisar agora no banco `sakila` usando a seguinte _query_:


```sql
SELECT * FROM sakila.payment;
```

![dateExplained](https://content-assets.betrybe.com/prod/dateExplained.jpeg)

Resultado da pesquisa

É possível confirmar que a coluna `payment_date` é exibida no formato `YYYY-MM-DD HH:MM:SS`. Assim, para fazer pesquisas e filtrar dados baseados em datas, temos que ter sempre isso em mente: quando você pensar no dia de 25 de dezembro de 2020, para o banco dados, esse dia será `2020-12-25`.

## Maneiras de encontrar dados por data

Vamos dizer que queremos encontrar pagamentos realizados na data `2005-07-31` na tabela `sakila.payment`. Há várias formas de fazer isso.

Usando a função `DATE(coluna_do_tipo_date)`:


```sql
SELECT * FROM sakila.payment
WHERE DATE(payment_date) = '2005-07-31';
```

![date_payment](https://content-assets.betrybe.com/prod/date_payment.png)
> Resultado da pesquisa. Encontra todos os pagamentos deste dia, ignorando horas, minutos e segundos

Usando `LIKE` para valores aproximados:


```sql
SELECT * FROM sakila.payment
WHERE payment_date LIKE '2005-07-31%';
```

![date_payment](https://content-assets.betrybe.com/prod/date_payment.png)

Resultado da pesquisa. Encontra todos os pagamentos deste dia, ignorando horas, minutos e segundos


```sql
SELECT * FROM sakila.payment
WHERE payment_date LIKE '2005-08-20 00:30:52';
```

![like_payment2](https://content-assets.betrybe.com/prod/like_payment2.png)

Resultado da pesquisa. Encontra um pagamento com dia e hora exatos

Usando `BETWEEN`:

```sql
SELECT *
FROM sakila.payment
WHERE payment_date BETWEEN '2005-05-26 00:00:00' AND '2005-05-27 23:59:59';
```

![between_payment3](https://content-assets.betrybe.com/prod/between_payment3.png)

Resultado da pesquisa. Encontra pagamentos especificando um valor mínimo e um valor máximo para a data

Qual é mais _performática_? Use o **_Execution Plan_** para determinar isso.

## Selecionando apenas partes de uma data

Às vezes você está interessado em apenas uma parte de uma data, como o ano ou as horas. **MySQL** possui funções que retornam partes específicas de uma data ou hora.

```sql
-- Teste cada um dos comandos a seguir:
SELECT DATE(payment_date) FROM sakila.payment; -- YYYY-MM-DD
SELECT YEAR(payment_date) FROM sakila.payment; -- Ano
SELECT MONTH(payment_date) FROM sakila.payment; -- Mês
SELECT DAY(payment_date) FROM sakila.payment; -- Dia
SELECT HOUR(payment_date) FROM sakila.payment; -- Hora
SELECT MINUTE(payment_date) FROM sakila.payment; -- Minuto
SELECT SECOND(payment_date) FROM sakila.payment; -- Segundo
```


#### Recursos adicionais:

-   [Quiz prêmio nobel com MySQL](https://sqlzoo.net/wiki/Nobel_Quiz)
-   [Desafios do HackerRank sobre conhecimentos básicos](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=select)
-   [Lidando com datas no MySQL](https://popsql.com/learn-sql/mysql/how-to-query-date-and-time-in-mysql/)
-   [Recursos para aprender e praticar SQL](https://www.w3resource.com/mysql/mysql-tutorials.php)
-   [Dates are more troublesome than they seem!](https://www.youtube.com/watch?v=-5wpm-gesOY)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/0798d603-86d8-4b98-849e-06094bfa936c/lesson/16e08471-e5b4-440d-b0ef-2b79104f4573)