# O que são _queries_

[[Banco de Dados]]
[[SQL]]

Inquirir, ou **_query_**, em inglês, é o nome dado aos comandos que você digita dentro de uma janela ou linha de comando com a intenção de interagir de alguma maneira com uma base de dados. No mundo de banco de dados, você pode tanto trazer dados quanto alterá-los, atribuir permissões de acesso e manipulação e muito mais. Vamos dar um olhada nos principais tipos de _queries_ a seguir:

-   **_DDL_**: Data Definition Language - Todos os comandos que lidam com o esquema, a descrição e o modo como os dados devem existir em um banco de dados:
    
    -   `CREATE`: Para criar bancos de dados, tabelas, índices, views, procedures, functions e triggers;
    -   `ALTER`: Para alterar a estrutura de qualquer objeto;
    -   `DROP`: Permite deletar objetos;
    -   `TRUNCATE`: Apenas esvazia os dados dentro de uma tabela, mas a mantém no banco de dados.
-   **_DML_**: Data Manipulation Language - Comandos que são usados para manipular dados. São utilizados para armazenar, modificar, buscar e excluir dados em um banco de dados. Os comandos e usos mais comuns nesta categoria são:
    
    -   `SELECT`: Usado para buscar dados em um banco de dados;
    -   `INSERT`: Insere dados em uma tabela;
    -   `UPDATE`: Altera dados dentro de uma tabela;
    -   `DELETE`: Exclui dados de uma tabela.
-   **_DCL_**: Data Control Language - Mais focado nos comandos que concedem direitos, permissões e outros tipos de controle ao sistema de banco de dados.
    
    -   `GRANT`: Concede acesso a um usuário;
    -   `REVOKE`: Remove acessos concedidos através do comando `GRANT`.
-   **_TCL_**: Transactional Control Language - Lida com as transações dentro de suas pesquisas.
    
    -   `COMMIT`: Muda suas alterações de temporárias para permanentes no seu banco de dados;
    -   `ROLLBACK`: Desfaz todo o impacto realizado por um comando;
    -   `SAVEPOINT`: Define pontos para os quais uma transação pode voltar. É uma maneira de voltar para pontos específicos de sua _query_;
    -   `TRANSACTION`: Comandos que definem onde, como e em que escopo suas transações são executadas.


## `SELECT`, o primeiro passo

Antes da aula a seguir, temos dois conceitos importantes que podem ser utilizados já no início do seu aprendizado de **SQL**. Esses conceitos são usar o `SELECT` para gerar valores e usar o `AS` para dar nomes às suas colunas, como nos exemplos a seguir. Rode cada um deles em uma janela de _query_ para verificar os resultados:


```sql
SELECT 'Olá, bem-vindo ao SQL!';
SELECT 10;
SELECT now();
SELECT 20 * 2;
SELECT 50 / 2;
SELECT 18 AS idade;
SELECT 2019 AS ano;
SELECT 'Rafael', 'Martins', 25, 'Desenvolvedor Web';
SELECT 'Rafael' AS nome, 'Martins' AS sobrenome, 25 AS idade, 'Desenvolvedor Web' AS 'Área de atuação';
```

Depois de rodar cada um desses comandos, vemos que é possível fazer algumas coisas apenas usando o `SELECT`, ainda sem alterar o banco de dados.

-   É possível gerar e calcular valores usando apenas `SELECT valor_a_ser_calculado_ou_exibido`;
-   Perceba que a palavra-chave `AS` permite que você dê nome às suas colunas para que elas façam mais sentido quando estiver lendo os resultados. Lembre-se de que, caso o nome tenha mais de uma palavra, devemos usar aspas simples para nomear as colunas;
-   Note que sempre finalizamos uma _query_ usando o ponto e vírgula (`;`);
-   Observe também que as palavras-chave (reservadas) estão em maiúsculo. Isso é uma convenção para facilitar a leitura da _query_. É recomendado que faça o mesmo!

## `CONCAT` - juntando duas ou mais colunas

Dê uma pesquisada agora na tabela `sakila.actor` usando o comando `SELECT * FROM sakila.actor` e veja que temos uma coluna chamada `first_name` e outra chamada `last_name`. Vamos imaginar que é necessário criar um relatório com o nome completo de um ator. Como podemos fazer isso? É fácil, basta usar a função `CONCAT`.

Para compreender seu uso, execute os exemplos a seguir no **MySQL Workbench**:


```sql
SELECT CONCAT(first_name, last_name) FROM sakila.actor;

-- Seu resultado ficou estranho? Eu também achei! Tente agora a query a seguir.

SELECT CONCAT(first_name, " ", last_name) FROM sakila.actor;

-- Muito melhor, certo? Mas dá para melhorar? Dá!

SELECT CONCAT(first_name, " ", last_name) AS "Nome Completo" FROM sakila.actor;
```

Então, como podemos ver no exemplo acima, é possível concatenar mais de uma coluna em apenas uma. Para isso, usamos a função `CONCAT`, que cria novos dados e informações a partir dos dados já existentes em uma tabela.


## `DISTINCT` - evitando dados repetidos

Dê uma olhada nesta tabela:

![Tabela fictícia](https://content-assets.betrybe.com/prod/49e3ba9e-f111-4bec-b7a9-3be8c3e0b283-Tabela%20fict%C3%ADcia.png)
> Tabela fictícia

Para criá-la no seu banco de dados, abra uma nova janela de _query_ no **MySQL Workbench** e execute o seguinte código:


```sql
CREATE DATABASE `Escola`;
CREATE TABLE IF NOT EXISTS Escola.Estudantes (
    `Nome` VARCHAR(7) CHARACTER SET utf8,
    `Idade` INT
);
INSERT INTO Escola.Estudantes VALUES
    ('Rafael', 25),
    ('Amanda', 30),
    ('Roberto', 45),
    ('Carol', 19),
    ('Amanda', 25);
```

Feito isso, você terá acesso à tabela `Estudantes` do banco de dados `Escola`. Levando em conta a explicação que você acabou de ver, como você montaria uma _query_ para encontrar os seguintes dados?

1.  Monte uma _query_ para encontrar pares únicos de **nomes** e **idades**.

**Solução:**
```sql
SELECT DISTINCT Nome, Idade FROM Escola.Estudantes;
```


2.  Quantas linhas você encontraria na _query_ anterior?

**Solução:** 5


3.  Monte uma _query_ para encontrar somente os **nomes** únicos.

**Solução:** 
```sql
SELECT DISTINCT Nome FROM Escola.Estudantes;
```

4.  Quantas linhas você encontraria na _query_ anterior?

**Solução:** 4

5.  Monte uma _query_ para encontrar somente as **idades** únicas.

**Solução:** 
```sql
SELECT DISTINCT Idade FROM Escola.Estudantes;
```

6.  Quantas linhas você encontraria na _query_ anterior?

**Solução:**  4


## `COUNT` - contando resultados

Um dos principais objetivos de se usar um banco de dados é responder a perguntas como: “Que quantidade de um certo tipo de dados existe na tabela?”. Ou, em um caso mais próximo ao nosso: “Quantas pessoas temos cadastradas no sistema?”. Ou ainda: “Em quantos estados temos clientes?”.

O `COUNT` retorna o número de resultados da sua _query_.

⚠️ **Atenção:** O comando `COUNT` não retorna dados nulos (**NULL** em **SQL**), entretanto valores _vazios_ (como uma string vazia, por exemplo: `""`) são considerados caracteres e por isso serão contados.

Nosso kit de ferramentas só está crescendo! Imagine que cada comando que você for aprendendo é como se fosse um novo acessório para o seu dia a dia.

![Os comandos SQL](https://content-assets.betrybe.com/prod/bd3fca39-d84d-440a-a946-9b2f0ca25773-Os%20comandos%20SQL.png)
> Os comandos (SQL) são como os acessórios: quando perceber, já vai ter juntado um monte.

Percebeu que você pode usar o `COUNT` de maneiras bem criativas, certo? Legal, então vamos pensar no seguinte cenário:

![tabela staff](https://content-assets.betrybe.com/prod/71a3f74d-f95e-48c9-ad85-7db7493b8d05-tabela%20staff.png)

tabela staff

Essa é a tabela `staff` do banco de dados `sakila`. Como você poderia responder às seguintes questões?

-   **Quantas senhas** temos cadastradas nessa tabela?

**Solução**
```sql
SELECT COUNT(password) FROM sakila.staff;
```

**Resposta:** 1

-   **Quantas pessoas** temos no total trabalhando para nossa empresa?

**Solução**
```sql
SELECT COUNT(*) FROM sakila.staff;
```

**Resposta:** 2

Até agora, trabalhamos principalmente com tabelas que têm poucas linhas de resultados (média de 200), e até aí tudo bem. Porém, em muitos cenários reais, você pode se deparar com milhares ou até centenas de milhares de resultados, e é aqui que vamos `LIMIT`_ar_ os resultados!


## `LIMIT` - especificando a quantidade de resultados

Se você abrir agora o nosso banco de dados `sakila` e executar a _query_ a seguir, verá que o resultado é 16044, ou seja, existem 16044 linhas na tabela `rental`.


```sql
SELECT COUNT(*) FROM sakila.rental;
```

Isso não é sempre necessário e pode até ser um problema em bancos de dados gigantes, em que as tabelas podem conter milhares ou milhões de linhas. Resolver isso é bem simples: tudo que você precisa fazer é limitar o resultado usando o `LIMIT`:


```sql
# Query + LIMIT quantidade_de_resultados
SELECT * FROM sakila.rental LIMIT 10;
```

![Tabela rental limitada a 10 linhas](https://content-assets.betrybe.com/prod/b7beb44f-52f4-4072-9c6b-429ecbf3641c-Tabela%20rental%20limitada%20a%2010%20linhas.png)

Tabela rental limitada a 10 linhas

> 👀 Observação: O Workbench pode limitar nossa visualização devido a paginação (Ou filtro).


## `LIMIT OFFSET` - Pulando linhas desnecessárias

Para pular uma certa quantidade de linhas do seu resultado, você pode usar o comando `OFFSET`.

```sql
# Query + LIMIT quantidade_de_linhas OFFSET quantidade_de_linhas
SELECT * FROM sakila.rental LIMIT 10 OFFSET 3;
```

![Tabela staff](https://content-assets.betrybe.com/prod/f3d90215-1ae9-4541-bd03-e41486b68d79-Tabela%20staff.jpg)
Tabela staff

Você poderia também limitar os resultados de forma gráfica, usando as opções do **Workbench**, que, por padrão, não impõe limites aos resultados de suas pesquisas.

![limit3](https://content-assets.betrybe.com/prod/f3d90215-1ae9-4541-bd03-e41486b68d79-limit3.png)

Tranquilo, não é? Agora, olhando o resultado a seguir, qual _query_ eu teria que montar para trazer os 10 primeiros resultados, a partir de `JOHNNY`?

![Tabela actor](https://content-assets.betrybe.com/prod/5c1296dc-e8f1-4faa-b41a-21f7b37add3d-Tabela%20actor.png)

Tabela actor

Ótimo, tomara que tenha conseguido achar o resultado do último desafio. Você está quase lá! Vamos fechar este dia de aprendizado descobrindo como gerar resultados do tipo que todo chefe gosta de ter: “Tudo bem organizado”, usando o `ORDER BY`.

```sql
SELECT * FROM sakila.actor LIMIT 10 OFFSET 4;
```


## `ORDER BY` - ordenando resultados

Veja o código a seguir:


```sql
SELECT * FROM sakila.address
ORDER BY district ASC, address DESC;
```

Ao usarmos o comando `ORDER BY`, podemos ordenar os resultados de forma alfabética ou numérica. Logo em seguida, informamos qual coluna iremos usar para ordenar os resultados. Podemos fazer de forma crescente (padrão do comando, porém pode ser usado o `ASC`) ou de forma decrescente (usando o `DESC`). Também é possível ordenar por mais de uma coluna. Assim, caso haja valores repetidos na primeira, a tabela será ordenada pelos valores da segunda, e assim por diante.

Para resumir: 

-   Para fazer pesquisas e retornar dados do banco, utilizamos o `SELECT`.
-   Para juntar (_concatenar_) duas ou mais colunas, utilizamos o `CONCAT`.
-   Para evitar dados repetidos em nossas _queries_, utilizamos o `DISTINCT`.
-   Para contar todos os dados retornados, usamos o `COUNT`.
-   Com o `LIMIT` e o `OFFSET`, podemos especificar quantos e quais serão os valores retornados.
-   E para ordenar nossos dados de maneira crescente ou decrescente, utilizamos o comando `ORDER BY`.

#### Recursos adicionais

-   [Introdução ao básico do SQL com prática](https://sqlzoo.net/wiki/SELECT_basics)
-   [W3Schools - Curso SQL online](https://www.w3schools.com/sql/)
-   [Documentação Oficial MySQL](https://dev.mysql.com/doc/refman/8.0/en/)
-   [Tutorial sobre tipos de comando SQL do W3Schools](https://www.w3schools.in/mysql/ddl-dml-dcl/)
-   [Tutorial sobre tipos de comando SQL do Java T Point](https://www.javatpoint.com/dbms-sql-command)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/727eca61-054b-45c5-bf26-b7958c09ad6d/lesson/8d5829df-e74b-448f-b74a-05e1b8a16543)