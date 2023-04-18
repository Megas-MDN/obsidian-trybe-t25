[[Banco de Dados]]
[[SQL]]

**Antes de iniciar essa seção:**

Os bancos de dados utilizados no vídeo podem ser acessados nos links a seguir.

Banco de dados `praticando`: [link](https://lms-assets.betrybe.com/lms/praticando.sql).

Banco de dados `hotel`: [link](https://lms-assets.betrybe.com/lms/hotel.sql).

Para usá-los em seu computador, copie o código disponibilizado em cada link e restaure cada um utilizando o MySQL Workbench, selecionando todo código e clicando no botão de raio para executar o script de restauração.

![Restaurando um banco de dados a partir de um script](https://content-assets.betrybe.com/prod/Restaurando%20um%20banco%20de%20dados%20a%20partir%20de%20um%20script.png)
> Restaurando um banco de dados a partir de um script

## Vamos Praticar um pouco mais sobre o exists

Use o [banco de dados hotel](https://lms-assets.betrybe.com/lms/hotel.sql) para realizar os desafios a seguir:

1.  Usando o `EXISTS` na tabela `books_lent` e `books`, exiba o **id** e **título** dos livros que ainda não foram emprestados.

**Solução**

```sql
SELECT
    id, title
FROM
    hotel.Books AS b
WHERE
    NOT EXISTS( SELECT
            *
        FROM
            hotel.Books_Lent
        WHERE
            b.Id = book_id);
```

2.  Usando o `EXISTS` na tabela `books_lent` e `books`, exiba o **id** e **título** dos livros estão atualmente emprestados e que contêm a palavra “lost” no título.

**Solução**

```sql
SELECT
    id, title
FROM
    hotel.Books b
WHERE
    EXISTS( SELECT
            *
        FROM
            hotel.Books_Lent
        WHERE
            b.Id = book_id AND b.title LIKE '%lost%');
```

3.  Usando a tabela `carsales` e `customers`, exiba apenas o nome dos clientes que ainda não compraram um carro.

**Solução**

```sql
SELECT
    name
FROM
    hotel.Customers c
WHERE
    NOT EXISTS( SELECT
            *
        FROM
            hotel.CarSales
        WHERE
            customerid = c.customerid);
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/b20149b3-a0e4-4069-bc83-8cc389e7e191/lesson/72740c4e-4c6c-4515-87a6-68b2c3758372/solution)
