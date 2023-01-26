[[Banco de Dados]]
[[SQL]]


O comando SQL UNION é um recurso importante da [linguagem SQL](https://blog.betrybe.com/sql/) que **auxilia na construção de queries capazes de retornar diferentes conjuntos de dados**. Por isso, ele se mostra extremamente útil quando precisamos consultar dados específicos em diferentes tabelas com um só comando.

No entanto, assim como os demais [comandos SQL](https://blog.betrybe.com/desenvolvimento-web/comandos-sql/), é preciso saber utilizar esse recurso corretamente para evitar cometer erros nas consultas ou acarretar problemas de desempenho no banco.

## O que é o comando SQL UNION e quais os operadores de conjunto?

O comando UNION é o operador responsável por **combinar os resultados de duas ou mais consultas SQL**, retornando como resultado todas as linhas das consultas realizadas. Mas para utilizá-lo é preciso ter atenção a algumas regras:

-   a quantidade e a ordem das colunas devem ser iguais em todas as queries;
-   os tipos de dados das colunas precisam ser compatíveis.

Além dele, também temos a variação UNION ALL e os operadores INTERSECT e EXCEPT, que explicaremos mais fundo nos tópicos a seguir.

### SQL UNION

Por padrão, o operador UNION **seleciona apenas valores distintos** entre as tabelas. Para isso, ele combina os resultados das queries e, em seguida, executa um SELECT DISTINCT para eliminar os valores duplicados.

![Figura 1. Retorno do SQL UNION](https://lh4.googleusercontent.com/lrxYURlZ90J85Y_u9XCfJbWScsjJyIT0lNXZnd6agpjCSwDV2SqJZp5TYDjKMzUXWlcfPUlo64mgrcwg_-jWUBlwVqAzXvCXZ19ikTTM7ZHfPHuTaCa4gjUlJAKAbYkL_qNva3k6)

Figura 1. Retorno do SQL UNION

Se usássemos o UNION nas tabelas 1 e 2, por exemplo, teríamos como resultado a tabela “3”:

Tabela 1:

A

B

C

D

Tabela 2:

C

D

E

F

1 UNION 2 = Tabela 3:

A

B

C

D

E

F

#### Sintaxe

A sintaxe básica do UNION é bastante simples, conforme você pode conferir aqui:

```sql
 SELECT nome_da_coluna FROM nome_da_tabela1
 UNION
 SELECT nome_da_coluna FROM nome_da_tabela2; 
```

### SQL UNION ALL 

O operador UNION ALL tem a mesma função do UNION, ou seja, ele combina os resultados de duas ou mais queries, a diferença é que ele **mantém os valores duplicados** de cada SELECT.

![](https://lh3.googleusercontent.com/EJrMmbcEya0Obn3jcEMC2JjsY_cA_MPJSSWGazo3mYX6VjiKLxakeei9uuQK6nESlCnRBbmBf6CNzbA2-YVPcYIHP2lpVFj_yOCqaKnCs3xO4nzXJ0fS5VwfMWO3octXj30eJTda)

Figura 2. Retorno do SQL UNION ALL

Nesse caso, se usássemos o UNION ALL nas tabelas 1 e 2, o resultado que teríamos na tabela 3 seria o seguinte:

Tabela 1:

A

B

C

D

Tabela 2:

C

D

E

F

1 UNION ALL 2 = Tabela 3:

A

B

C

D

C

D

E

F

#### Sintaxe

Para usar esse operador, basta lembrar da sintaxe abaixo:

```sql
 SELECT nome_da_coluna FROM nome_da_tabela1
 UNION ALL
 SELECT nome_da_coluna FROM nome_da_tabela2; 
```

### SQL EXCEPT

O operador de conjunto EXCEPT é responsável por combinar dois comandos SELECT, comparando seus retornos para **retornar apenas as linhas que aparecem somente na primeira tabela**. Ou seja, ele exclui do retorno todos os valores da segunda tabela, além dos registros duplicados entre elas.

![Figura 3. Retorno do SQL EXCEPT](https://u3r3f6s2.rocketcdn.me/wp-content/uploads/2021/08/image1-2-1024x313.png)

Figura 3. Retorno do SQL EXCEPT

Pensando novamente nas nossa tabelas de exemplo, caso fosse usado um EXCEPT nelas, o resultado obtido seria: 

Tabela 1:

A

B

C

D

Tabela 2:

C

D

E

F

1 EXCEPT 2 = Tabela 3:

A

B

#### Sintaxe

Assim como os anteriores, a sintaxe básica para aplicar um EXCEPT é muito simples. Veja:

```sql
 SELECT nome_da_coluna FROM nome_da_tabela1
 EXCEPT
 SELECT nome_da_coluna FROM nome_da_tabela2; 
```

### SQL INTERSECT

O operador INTERSECT é usado para combinar o resultado de duas ou mais consultas, mas ele **retorna apenas os valores que se repetem**. Basicamente, ele pega um dado da primeira tabela e avalia se há um valor igual na segunda tabela. Caso haja, o valor é retornado pelo SELECT. Se não houver, ele é descartado.

![Figura 4. Retorno do SQL INTERSECT](https://lh3.googleusercontent.com/2kno6LuBqYMFamYNoS1prk9wWkkjfvLHBiLYcWrWllJ9jKlkQ6C3Cj0aw3_M3ItHuPWdIQB94aBsrl9THLb_-LujTW_fyv_0OWnAok-VKOTxDnYs1nC21PB3WCQPz3i1crhScP3x)

Figura 4. Retorno do SQL INTERSECT

Para exemplificar, se essa instrução fosse usada nas tabelas 1 e 2, nossa tabela 3 ficaria assim:

Tabela 1:

A

B

C

D

Tabela 2:

C

D

E

F

1 INTERSECT 2 = Tabela 3:

C

D

#### Sintaxe

A sintaxe básica do INTERSECT é muito simples, como mostramos a seguir:

```sql
 SELECT nome_da_coluna FROM nome_da_tabela1
 INTERSECT
 SELECT nome_da_coluna FROM nome_da_tabela2; 
```

## Boas práticas ao usar o comando SQL UNION

Uma das recomendações ao utilizar esse comando é **optar pelo operador UNION ALL caso não haja a possibilidade das tabelas do seu banco conterem registros duplicados**. Isso porque, ao contrário do UNION, ele não executará um SQL DISTINCT para excluir os valores duplicados do resultado. Por consequência, serão usados menos recursos do banco e a [aplicação](https://blog.betrybe.com/desenvolvimento-web/aplicacoes-web/) terá melhor performance.

Da mesma forma, não se deve usar o UNION explicitamente com a função DISTINCT. Afinal, ela já é executada por padrão e, caso seja adicionada no código, o resultado será o mesmo. No entanto, a operação será realizada duas vezes pelo banco, o que aumentará o gasto de recursos do sistema.

## Exemplos de uso do comando SQL UNION e SQL UNION ALL

Agora que a função de cada um dos comandos já foram explicadas, vamos aos exemplos práticos! Para eles, usaremos como base as tabelas “clientes” e “fornecedores”, que mostramos a seguir:

**id** | **nome** | **endereco** | **cidade** | **pais**
-- | -- | -- | -- | -- 
1 | Gabriel Maia | Rua José Alencar, 27, Santa Luca | Guajará | Brasil
2 | Manuel Delgado | Carrera 09, 112, La Candelaria | Bogotá | Colômbia
3 | Joseph | Tenth Avenue, 203, Bronx | New York | USA

Tabela 1. Tabela clientes

**id** | **nome** | **endereco** | **cidade** | **pais**
-- | -- | -- | -- | --
1 | Marques Tubulações | Rua Maria das Graças, 401, Isabel | Piracicaba | Brasil
2 | Stone Papers | 208 Oxford Rd. | dores Houston | USA
3 | Mercado de San Juan | Calle de Ernesto Pugibet, 21 | Mexico City | México

Tabela 2. Tabela fornecedores

### Exemplo 1: SQL UNION

Neste primeiro exemplo, vamos demonstrar uma forma de uso simples do UNION. No caso, queremos consultar os países cadastrados nas tabelas “clientes” e “fornecedores”. Para isso, será usado o seguinte comando SQL:

```sql
 SELECT pais FROM clientes
 UNION
 SELECT pais FROM fornecedores; 
```

Após rodar o código, temos o resultado mostrado a seguir:

![Figura 5. Resultado do SQL UNION](https://lh6.googleusercontent.com/OVHjOS51fd7xMlm4VWRm4l-Kd6iVsuD6vF8KVsGRPL_8uPJ6b59lsVikCi9jvM4gixoiSAi9K_iDHN1YTEg4hcLEsGucCauLM4UIELJKtsChzHRaHf2mAkUNF0pX8FXlf5NQptel)

Figura 5. Resultado do SQL UNION

### Exemplo 2: SQL UNION ALL

Agora também vamos consultar os países cadastrados nas tabelas “clientes” e “fornecedores”. No entanto, dessa vez usaremos o operador UNION ALL para observar a diferença entre os resultados. 

```sql
 SELECT pais FROM clientes
 UNION ALL
 SELECT pais FROM fornecedores; 
```

Depois de [executar o código](https://blog.betrybe.com/python/python-while/), vemos o resultado abaixo:

![Figura 6. Resultado do SQL UNION ALL](https://lh3.googleusercontent.com/0KomDuv-YfsvT0N57-i50NLsmpFnpf2Zt1eCKNnTPKresVtx4GL5ana1HUDIkxbObAa5RMsFt_d3HswQZIhjWcsk0tXICqbRl_tk7dTa5NMkYF_bzN0C7rnI-uhYLaYGXQ6tkCQY)

Figura 6. Resultado do SQL UNION ALL

Perceba que, ao contrário do exemplo anterior, o comando listou todos os países sem excluir aqueles que se repetem nas tabelas.

### Exemplo 3: SQL UNION com cláusula WHERE

O uso da cláusula WHERE é opcional em comandos SELECT, mas ela pode ser usada para tornar a busca mais apurada no [banco de dados](https://blog.betrybe.com/tecnologia/bancos-de-dados/). Neste exemplo, vamos usá-la para filtrar os registros pelo país.

No caso, queremos consultar o nome e a cidade de clientes e fornecedores do país Brasil. Para obter esse resultado, usaremos a seguinte query:

```sql
 SELECT nome, cidade
 FROM clientes
 WHERE pais = 'Brasil'
 UNION
 SELECT nome, cidade
 FROM fornecedores
 WHERE pais = 'Brasil'; 
```

Abaixo, observe o retorno dado pelo comando:

![](https://lh4.googleusercontent.com/BFPBVYEWTMPsjFTmuS2Z2c22wO1_9vTQ75CAEFevd3q3SrljOFIef42H_LfN6auqSLuy9RJhV_Ny6yeJNgnrDOok6gmXNQfwHiTZaVjTzVIVXMTNKHeeO9HWDrVNjpith89-Xmg5)

Figura 7. Resultado do SQL UNION com cláusula WHERE

Como foi possível perceber, o **comando SQL UNION facilita a** [**manipulação de dados**](https://blog.betrybe.com/tecnologia/mineracao-de-dados/) **no banco e torna as consultas mais eficientes ao combinar os resultados de múltiplas queries em um só retorno**. Portanto, trata-se de um operador extremamente útil para quem lida com essa linguagem.+

###### Fonte: [Blog Trybe](https://blog.betrybe.com/sql/sql-union/)