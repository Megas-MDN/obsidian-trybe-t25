[[Banco de Dados]]
[[SQL]]

## Adição, subtração, multiplicação e divisão

Para as operações matemáticas mais comuns, podemos empregar os operadores matemáticos usuais. Vamos testar cada um deles?

Execute os seguintes comandos dentro do Workbench:

```sql
SELECT 5 + 5;
SELECT 5 - 5;
SELECT 5 * 5;
SELECT 5 / 5;
```

Podemos, também, usar as colunas diretamente como base para os cálculos, caso necessário.

```sql
SELECT rental_duration + rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration - rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration / rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration * rental_rate FROM sakila.film LIMIT 10;
```

## Divisão de inteiros com `DIV` e como encontrar seus restos com o `MOD`

O `DIV` retorna o resultado inteiro de uma divisão, ignorando as casas decimais de um número. Veja os exemplos abaixo:

```sql
SELECT 10 DIV 3; -- 3
SELECT 10 DIV 2; -- 5
SELECT 14 DIV 3; -- 4
SELECT 13 DIV 2; -- 6
```

Já o operador `MOD` retorna o resto de uma divisão como resultado. Por exemplo:

```sql
SELECT 10 MOD 3; -- 1
SELECT 10 MOD 2; -- 0
SELECT 14 MOD 3; -- 2
SELECT 13 MOD 2; -- 1
SELECT 10.5 MOD 2; -- 0.5, ou seja, 2 + 2 + 2 + 2 + 2 = 10, restando 0.5
```


### Desafios com DIV e MOD

**Dica:** Números pares são aqueles que podem ser divididos em duas partes iguais. Ou seja, são aqueles cuja divisão por 2 retorna resto 0.

1.  Monte uma _query_ usando o `MOD` juntamente com o `IF` para descobrir se o valor 15 é par ou ímpar. Chame essa coluna de **‘Par ou Ímpar’**, onde ela pode dizer ‘Par’ ou ‘Ímpar’.

2.  Temos uma sala de cinema que comporta 220 pessoas. Quantos grupos completos de 12 pessoas podemos levar ao cinema sem que ninguém fique de fora?

3.  Utilizando o resultado anterior, responda à seguinte pergunta: temos lugares sobrando? Se sim, quantos?

## Arredondando valores

Ter a capacidade de encontrar aproximações de valores é algo extremamente valioso na criação de relatórios e gráficos, que são utilizados por softwares de todos os tipos. O MySQL tem algumas funções que te ajudam a resolver isso. Vamos conhecê-las agora.

O `ROUND` arredonda os números de acordo com sua parte decimal. Se for maior ou igual a 0.5, o resultado é um arredondamento para cima. Caso contrário, ocorre um arredondamento para baixo. Veja os exemplos abaixo:


```sql
-- Podemos omitir ou especificar quantas casas decimais queremos
SELECT ROUND(10.4925); -- 10
SELECT ROUND(10.5136); -- 11
SELECT ROUND(-10.5136); -- -11
SELECT ROUND(10.4925, 2); -- 10.49
SELECT ROUND(10.4925, 3); -- 10.493
```

O arredondamento **sempre** para cima pode ser feito com o `CEIL`:

```sql
SELECT CEIL(10.51); -- 11
SELECT CEIL(10.49); -- 11
SELECT CEIL(10.2); -- 11
```

O arredondamento **sempre** para baixo pode ser feito com o `FLOOR`:

```sql
SELECT FLOOR(10.51); -- 10
SELECT FLOOR(10.49); -- 10
SELECT FLOOR(10.2); -- 10
```

## Exponenciação e raiz quadrada

Para cálculos de exponenciação e raiz quadradas, podemos utilizar as funções `POW` e `SQRT`, respectivamente.

Elevando um número X à potência Y usando a função `POW`:

```sql
SELECT POW(2, 2); -- 4
SELECT POW(2, 4); -- 16
```

Encontrando a raiz quadrada de um valor usando `SQRT`:


```sql
SELECT SQRT(9); -- 3
SELECT SQRT(16); -- 4
```

## Gerando valores aleatórios

Para situações em que se faz necessário gerar valores aleatórios, podemos usar a função `RAND`, em conjunto com as funções anteriores.

```sql
-- Para gerar um valor aleatório entre 0 e 1:
SELECT RAND();

-- Para gerar um valor entre 7 e 13:
SELECT ROUND(7 + (RAND() * 6));

-- O cálculo que é feito é o seguinte: (7 + (0.0 a 1.0 * 6))
```



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/6ead052e-46e3-4d96-a207-873325293189/lesson/b16c8fb7-ade8-4ebc-8711-579a7b9da4fb)

