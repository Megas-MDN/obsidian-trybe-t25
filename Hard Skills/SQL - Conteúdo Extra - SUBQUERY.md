[[Banco de Dados]]
[[SQL]]
[[SQL - 14 Join]]


Uma `SUBQUERY` é uma query aninhada que é avaliada dentro de um par de parênteses. Ela pode conter expressões simples, como adições e subtrações, mas não se limita a isso, uma vez que podemos utilizar praticamente todos os comandos já vistos até o momento dentro de uma `SUBQUERY`.

Algo a se lembrar é que a subquery não é a única maneira de encontrar resultados de tabelas relacionadas. Quando se trata de SQL, os `JOINs` podem ser usados para encontrar os mesmos resultados.

É recomendado tomar a decisão sobre qual opção utilizar (subquery ou `JOIN`) baseando-se na performance da sua query.

## Diferentes maneiras de utilizar uma SUBQUERY

1.  Usando uma `SUBQUERY` como fonte de dados para o `FROM`.

```sql
SELECT f.title, f.rating
FROM (
    SELECT *
    FROM sakila.film
    WHERE rating = 'R'
) AS f;
```

![Resultado da subquery usada no FROM](https://content-assets.betrybe.com/prod/Resultado%20da%20subquery%20usada%20no%20FROM.png)

Resultado da subquery usada no `FROM`

2.  Preenchendo uma coluna de um `SELECT` por meio de uma `SUBQUERY`.

```sql
SELECT
    address,
    district,
    (
        SELECT city
        FROM sakila.city
        WHERE city.city_id = sakila.address.city_id
    ) AS city
FROM sakila.address;
```

![Resultado da subquery como uma coluna do SELECT](https://content-assets.betrybe.com/prod/Resultado%20da%20subquery%20como%20uma%20coluna%20do%20SELECT.png)

Resultado da subquery como uma coluna do `SELECT`

3.  Filtrando resultados com `WHERE` usando como base os dados retornados de uma `SUBQUERY`.

```sql
SELECT address, district
FROM sakila.address
WHERE city_id IN (
    SELECT city_id
    FROM sakila.city
    WHERE city IN ('Sasebo', 'San Bernardino', 'Athenai', 'Myingyan')
);
```

![Resultado da subquery com o WHERE](https://content-assets.betrybe.com/prod/Resultado%20da%20subquery%20com%20o%20WHERE.png)

Resultado da subquery com o `WHERE`

4.  Usando uma tabela externa, de fora da `SUBQUERY`, dentro dela.

```sql
SELECT
    first_name,
    (
        SELECT address
        FROM sakila.address
        WHERE address.address_id = tabela_externa.address_id
    ) AS address
FROM sakila.customer AS tabela_externa;
```

![Resultado da subquery usando tabela externa](https://content-assets.betrybe.com/prod/Resultado%20da%20subquery%20usando%20tabela%20externa.png)

Resultado da subquery usando tabela externa

## SUBQUERY ou JOIN

Talvez você esteja se perguntando se seria possível resolver as queries anteriores através de um `JOIN`. De fato, podemos, como é exemplificado a seguir.

Usando `SUBQUERY`

```sql
SELECT
    first_name,
    (
        SELECT address
        FROM sakila.address
        WHERE address.address_id = tabela_externa.address_id
    ) AS address
FROM sakila.customer AS tabela_externa;
```

Usando `INNER JOIN`

```sql
SELECT c.first_name, ad.address
FROM sakila.customer c
INNER JOIN sakila.address ad ON c.address_id = ad.address_id;
```

Sabendo disso, como decidir entre as duas abordagens? Decida qual usar através de testes de performance e, em seguida, por afinidade.

## Uma maneira simples de mensurar a performance e decidir sobre qual abordagem utilizar (Execution Plan)

Diferente da maioria dos problemas que as pessoas desenvolvedoras resolvem, é possível decidir por queries melhores que outras por meio da medição do seu custo de execução. Existem diversas maneiras para mensurar a performance e otimizar queries no MySQL Server.

A otimização envolve configurar, ajustar e medir o desempenho em vários níveis:

-   Escalar o banco de dados de forma vertical, ou seja, instanciar mais CPU e memória para o processo do Banco de dados.
-   Escalar o banco de dados de forma horizontal, ou seja, instanciar mais máquinas e balancear a carga entre as diferentes instâncias.
-   Escrever o código SQL de forma que aproveite melhor os recursos do SGBD;

Nesta aula, iremos abordar apenas uma delas: o **execution plan**, um recurso que nos permite metrificar e comparar quais queries tem performance melhor para gerar um determinado resultado.

Ele mensura o custo de uma query e exibe o tipo de **scan** (motor de busca) efetuado em cada tabela incluída na query e seu custo total. O mysql possui algumas opções de scan, mas aqui só falaremos de 2 delas: **table scan** e **index seek**.

O **table scan** é utilizado quando você realiza uma query inespecífica e precisa buscar todos os dados da tabela. Como, por exemplo, a query abaixo.

```sql
SELECT * FROM table;
```

-   O **table scan** não utiliza um mecanismo de busca por índice, e precisa percorrer todos os registros da tabela para recuperar os resultados desejados, como seria pequisar dados em um livro sem índice, que você precisa ler todo o livro para encontrar a informação desejada.
    
-   O **index seek** é utilizado quando você realiza uma query específca com `WHERE`, em que a coluna utilizada tenha um _índice clusterizado_. Isso significa que, quando você adiciona uma coluna que possui uma chave primária na criação da tabela, o SQL automaticamente cria um _index clusterizado_ nesta coluna, como um índice que contém os capítulos de um livro, que pode ser utilizado para otimizar uma busca. Assim o **index seek** realiza uma busca mais rápida que o **table scan** e possui uma performance melhor em tabelas com muitas linhas.
    

```sql
SELECT * FROM table
WHERE alguma_condicao;
```

Se achar que sua consulta está lenta, você deve verificar o **execution plan** para confirmar se está usando **index seek** ou **table scan**. Em seguida, você pode otimizar sua consulta ajustando sua query.

Seu uso na prática pode ser visto da seguinte forma:

Tomando como exemplo as duas últimas queries desta página, crie dois novos arquivos SQL no seu MySQl Workbench. Em um deles, cole a query em que utilizamos a solução usada como `SUBQUERY` e, no outro, a que se utilizou como `INNER JOIN`.

Em seguida, execute uma das queries e depois clique em **Execution Plan**, como na imagem abaixo, e observe o valor de “Query Cost”. Quanto menor o valor, em comparação com outra versão da query, melhor a performance. Assim você pode simplesmente escolher a query que tem o menor custo.

![Como acessar o execution plan](https://content-assets.betrybe.com/prod/Como%20acessar%20o%20execution%20plan.png)

Como acessar o execution plan

Execute os comandos acima e verifique o custo de cada query. Ficou claro que, nesse caso específico, a `SUBQUERY` tem uma performance melhor que o `JOIN`, em razão de ter o custo de query mais baixo.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/b20149b3-a0e4-4069-bc83-8cc389e7e191/lesson/64459d62-5a06-4bd2-b515-16355a39822d)
