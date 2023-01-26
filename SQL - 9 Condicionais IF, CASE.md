[[Banco de Dados]]
[[SQL]]
[[IF...Else]]
[[Switch...Case]]

Em linguagens de _alto nível_, tais como: _Python_ e _JavaScript_, as condicionais são a base para a criação de algoritmos dinâmicos que se adaptam de acordo com a necessidade do programa. Nesse quesito, o SQL não fica para trás, sendo também possível usar nele os principais comandos de controle de fluxo, como o `IF` e o `CASE`.

> Obs.: Caso queira saber mais sobre linguagens de alto nível, leia o artigo de _William Oliveira_ na seção de recursos adicionais.

```sql
-- Sintaxe:
SELECT IF(condicao, valor_se_verdadeiro, valor_se_falso);

SELECT IF(idade >= 18, 'Maior de idade', 'Menor de Idade')
FROM pessoas;

SELECT IF(aberto, 'Entrada permitida', 'Entrada não permitida')
FROM estabelecimentos;

-- Exemplo utilizando o banco sakila:
SELECT first_name, IF(active, 'Cliente Ativo', 'Cliente Inativo') AS status
FROM sakila.customer
LIMIT 20;
```


Em situações em que é preciso comparar mais de uma condição, é preferível utilizar o `CASE`.

```sql
-- Sintaxe:
SELECT CASE
  WHEN condicao THEN valor
  ELSE valor padrao
END;

SELECT
    nome,
    nivel_acesso,
    CASE
        WHEN nivel_acesso = 1 THEN 'Nível de acesso 1'
        WHEN nivel_acesso = 2 THEN 'Nível de acesso 2'
        WHEN nivel_acesso = 3 THEN 'Nível de acesso 3'
        ELSE 'Usuário sem acesso'
    END AS nivel_acesso
FROM permissoes_usuario;

-- Exemplo utilizando a tabela sakila.film:
SELECT
    first_name,
    email,
    CASE
        WHEN email = 'MARY.SMITH@sakilacustomer.org' THEN 'Cliente de baixo valor'
        WHEN email = 'PATRICIA.JOHNSON@sakilacustomer.org' THEN 'Cliente de médio valor'
        WHEN email = 'LINDA.WILLIAMS@sakilacustomer.org' THEN 'Cliente de alto valor'
        ELSE 'não classificado'
    END AS valor
FROM sakila.customer
LIMIT 10;
```


Exemplo usando o Bando de Dados Sakila

1.  Usando o `IF` na tabela `sakila.film`, exiba o **id do filme**, o **título** e uma coluna extra chamada **‘conheço o filme?’**, em que deve-se avaliar se o nome do filme é ‘**ACE GOLDFINGER**‘. Caso seja, exiba “Já assisti a esse filme”. Caso contrário, exiba “Não conheço o filme”. Não esqueça de usar um _alias_ para renomear a coluna da condicional.

```sql
SELECT
    film_id,
    title,
    IF(title = 'ACE GOLDFINGER', 'Já assisti a esse filme', 'Não conheço o filme') AS 'conheço o filme?'
FROM sakila.film;
```

2.  Usando o `CASE` na tabela `sakila.film`, exiba o **título**, a **classificação indicativa** (`rating`) e uma coluna extra que vamos chamar de **‘público-alvo’** em que colocaremos a classificação do filme de acordo com as seguintes siglas:
    -   **G:** “Livre para todos”;
    -   **PG:** “Não recomendado para menores de 10 anos”;
    -   **PG-13:** “Não recomendado para menores de 13 anos”;
    -   **R:** “Não recomendado para menores de 17 anos”;
    -   **Se não cair em nenhuma das classificações anteriores:** “Proibido para menores de idade”.


```
SELECT
    title, 
    rating, 
    CASE
        WHEN rating = 'G' THEN 'Livre para todos'
        WHEN rating = 'PG' THEN 'Não recomendado para menores de 10 anos' 
        WHEN rating = 'PG-13' THEN 'Não recomendado para menores de 13 anos'
        WHEN rating = 'R' THEN 'Não recomendado para menores de 17 anos'
        ELSE 'Proibido para menores de idade'
    END AS 'público Alvo'
FROM sakila.film;
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/6ead052e-46e3-4d96-a207-873325293189/lesson/fcd94539-2c2c-406b-9b96-6166a6f803b6)
