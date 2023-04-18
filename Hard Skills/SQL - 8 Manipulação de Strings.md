[[Banco de Dados]]
[[SQL]]
[[SQL - 5 Encontrando Dados em um Banco de Dados*****]]

Uma das responsabilidades das pessoas que lidam com o registro de informações em um banco de dados é se certificar de que esses dados estão coerentes, normalizados e cadastrados no formato correto. O **MySQL** possui algumas funções de manipulação de **texto** que facilitam essas tarefas.

As principais podem ser vistas a seguir:

```sql
-- Converte o texto da string para CAIXA ALTA
SELECT UCASE('Oi, eu sou uma string');

-- Converte o texto da string para caixa baixa
SELECT LCASE('Oi, eu sou uma string');

-- Substitui as ocorrências de uma substring em uma string
SELECT REPLACE('Oi, eu sou uma string', 'string', 'cadeia de caracteres');

-- Retorna a parte da esquerda de uma string de acordo com o
-- número de caracteres especificado
SELECT LEFT('Oi, eu sou uma string', 3);

-- Retorna a parte da direita de uma string de acordo com o
-- número de caracteres especificado
SELECT RIGHT('Oi, eu sou uma string', 6);

-- Exibe o tamanho, em caracteres, da string, a função LENGTH retorna o tamanho em bytes
SELECT CHAR_LENGTH('Oi, eu sou uma string');

-- Extrai parte de uma string de acordo com o índice de um caractere inicial
-- e a quantidade de caracteres a extrair
SELECT SUBSTRING('Oi, eu sou uma string', 5, 2);

-- Se a quantidade de caracteres a extrair não for definida,
-- então a string será extraída do índice inicial definido, até o seu final
SELECT SUBSTRING('Oi, eu sou uma string', 5);
```

Para fixar melhor, que tal explorar na prática o que cada comando faz? Execute cada um deles no **MySQL Workbench** e veja os resultados.

Algo importante a se notar sobre strings em SQL é que, diferente de várias linguagens de programação, no SQL, as _strings_ são **indexadas a partir do índice 1** e não do índice 0. Caso tenha resultados inesperados, essa pode ser uma das razões.

Observe que, apesar de ter usado strings temporárias nos exemplos acima, também é possível fazer essas operações diretamente nas colunas de uma tabela.

##### Outros Exemplos:

Faça uma _query_ que exiba a palavra `'trybe'` em CAIXA ALTA.
```sql
SELECT UCASE('trybe');
```


Faça uma _query_ que transforme a frase `'Você já ouviu falar do DuckDuckGo?'` em `'Você já ouviu falar do Google?'`.
```sql
SELECT REPLACE('Você já ouviu falar do DuckDuckGo?', 'DuckDuckGo', 'Google');
```


Utilizando uma _query_, encontre quantos caracteres temos em `'Uma frase qualquer'`.
```sql
SELECT LENGTH('Uma frase qualquer');
```


Extraia e retorne apenas a palavra “JavaScript” da frase `'A linguagem JavaScript está entre as mais usadas'`.
```sql
SELECT SUBSTRING('A linguagem JavaScript está entre as mais usadas', 13, 10);
-- OU
3SELECT SUBSTRING('A linguagem JavaScript está entre as mais usadas', -36, 10);
```


Padronize a string `'RUA NORTE 1500, SÃO PAULO, BRASIL'` para que suas informações estejam todas em caixa baixa.
```sql
SELECT LCASE('RUA NORTE 1500, SÃO PAULO, BRASIL');
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/6ead052e-46e3-4d96-a207-873325293189/lesson/4fae867f-d7ef-4a86-b8c1-cca96ed52b53)
