[[Banco de Dados]]
[[SQL]]
[[Funções]]

Conseguimos fazer algumas coisas legais, como, por exemplo, consultar data e hora atuais usando as seguintes funções:

```sql
SELECT CURRENT_DATE(); -- YYYY-MM-DD
SELECT NOW(); -- YYYY-MM-DD HH:MM:SS
```

Também podemos calcular a diferença em dias entre duas datas usando o `DATEDIFF` e a diferença de tempo entre dois horários usando o `TIMEDIFF`. Em ambos os casos, o segundo valor é subtraído do primeiro para calcular o resultado.

```sql
-- 30, ou seja, a primeira data é 30 dias depois da segunda
SELECT DATEDIFF('2020-01-31', '2020-01-01');

-- -30, ou seja, a primeira data é 30 dias antes da segunda
SELECT DATEDIFF('2020-01-01', '2020-01-31');

-- -01:00:00, ou seja, há 1 hora de diferença entre os horários
SELECT TIMEDIFF('08:30:10', '09:30:10');

-- -239:00:00, ou seja, há uma diferença de 239 horas entre as datas
SELECT TIMEDIFF('2021-08-11 08:30:10', '2021-08-01 09:30:10');
```

Outro ponto interessante é que também podemos usar `CURRENT_DATE()` e `NOW()` em conjunto com os comandos de manipulação de datas e tempo para encontrar resultados dinâmicos da seguinte maneira:

```sql
SELECT YEAR(CURRENT_DATE()); -- retorna o ano atual
SELECT HOUR(NOW()); -- retorna a hora atual
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/6ead052e-46e3-4d96-a207-873325293189/lesson/81f2c554-8d0d-462c-8b67-e7b1d47444a7)