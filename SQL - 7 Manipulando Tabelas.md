[[Banco de Dados]]
[[SQL]]

# Apagando e recriando um banco de dados

Como agora você começará a mexer na estrutura do banco de dados `sakila`, você deve saber recriar o banco de dados quantas vezes for necessário, em caso de alterações acidentais ou por alguma outra necessidade. Os passos para recriar o banco podem ser lidos a seguir.

Como apagar (_dropar_) o banco `sakila` e recriá-lo do zero:

1.  Abra o **MySQL Workbench** e se conecte a ele.
2.  Selecione o banco `sakila` na lista de bancos de dados com o botão direito e clique em “**Drop Schema**“.
3.  Selecione **“Drop Now”**.
    

![Excluindo o banco `sakila`](https://content-assets.betrybe.com/prod/8c6e13af-6d11-47e5-b608-fbff92775dc8-Excluindo%20o%20banco%20%60sakila%60.gif)

Excluindo o banco `sakila`

4.  Clique com o botão direito [neste link](https://lms-assets.betrybe.com/lms/sakila.sql) e salve como arquivo `.sql`.
5.  Retorne para o **MySQL Workbench**, selecione _Abrir Script SQL…_ e selecione o arquivo `sakila.sql`.
6.  Clique em executar para restaurar o banco de dados.
7.  Caso necessário, clique no botão de “atualizar schemas”.
    

![Restaurando o banco `sakila`](https://content-assets.betrybe.com/prod/8c6e13af-6d11-47e5-b608-fbff92775dc8-Restaurando%20o%20banco%20%60sakila%60.gif)

Restaurando o banco `sakila`

8.  _That’s it!_ Está pronto para ~~**quebrar**~~ brincar com ele de novo!


## `INSERT` - adicionando dados em tabelas

### Informação importante sobre os tipos de aspas

-   **Backticks ou crase (` `` `)**: são usadas para identificar nome de **tabelas** e **colunas**. São necessárias apenas quando o identificador for uma palavra reservada do **MySQL**, ou quando o nome da tabela ou coluna contiver espaços em branco.
    
-   **Aspas simples (`''`)**: devem ser usadas em valores do tipo **string**. Aspas simples são aceitas na maioria dos Sistemas de Gerenciamento de Banco de Dados, sendo assim, é preferível usar aspas simples no lugar das aspas duplas.
    

Só usaremos os **backticks** aqui nos exemplos caso sejam absolutamente necessários. Caso contrário, eles serão omitidos.

Vamos começar a dar vida ao banco `sakila`. Uma pesquisa rápida na tabela `sakila.staff` nos informa que a empresa possui apenas dois funcionários.

Acho que ela pode contar com nossa ajuda para melhorar isso. A sintaxe para inserir dados em uma tabela é a seguinte:


```sql
INSERT INTO nome_da_tabela (coluna1, coluna2)
VALUES ('valor_coluna1', 'valor_coluna2');
```

A _query_ acima vai inserir uma linha na tabela `nome_da_tabela` com os valores em suas colunas correspondentes. Apesar de ser possível inserir novos valores sem especificar os nomes das colunas, é uma boa prática sempre especificá-los porque:

1.  Caso a estrutura da tabela tenha mudado enquanto se escreve a _query_, você será alertado.
2.  Melhora a compreensão para quem estiver lendo sua _query_ futuramente.

### Inserindo várias linhas de uma vez

É possível inserir múltiplas linhas em uma tabela com uma única _query_:


```sql
INSERT INTO nome_da_tabela (coluna1, coluna2) VALUES
('valor_1','valor_2'),
('valor_3','valor_4'),
('valor_5','valor_6');
```

Dessa maneira, podemos ganhar muito tempo, tanto no quesito de quantidade de caractéres digitados como em performance de inserção. Em média, 100 linhas inseridas dessa maneira podem ser até 10 vezes mais rápidas que fazendo inserções de forma individual.

### Ignorando linhas existentes

Quando for importar uma quantidade grande de dados, pode ser preferível, em alguns cenários, que você simplesmente ignore os erros e pule os dados problemáticos, que, normalmente, interromperiam a _query_ em função de alguma restrição imposta na tabela. Ex: **_duplicidade de primary keys_**.

Podemos ignorar os erros durante a inserção usando o `INSERT IGNORE`. Considere a tabela e a _query_ a seguir:

![Tabela `pessoas`](https://content-assets.betrybe.com/prod/Tabela%20%60pessoas%60.png)

Tabela `pessoas`


```sql
INSERT IGNORE INTO pessoas (id, name) VALUES
(4,'Gloria'), -- Sem o IGNORE, essa linha geraria um erro e o INSERT não continuaria.
(5,'Amanda');

-- Pesquisando agora, você verá que a informação duplicada não foi inserida.
-- Porém os dados corretos foram inseridos com sucesso.
SELECT * FROM pessoas;
```

![Tabela pessoas](https://content-assets.betrybe.com/prod/Tabela%20pessoas.png)

Tabela pessoas

**IMPORTANTE:** Lembre-se de que o `INSERT IGNORE` vai pular os outros erros silenciosamente também.

### Inserindo valores em colunas com auto_increment

Primeiramente, é preciso saber que o **auto_increment** é uma funcionalidade que todos os bancos de dados possuem. Ela permite que valores sejam gerados automaticamente cada vez que uma nova linha é inserida em uma tabela que tem essa restrição ativa. Ao inserir um novo ator na tabela `sakila.actor`, caso outros atores ainda não tenham sido inseridos desde que o banco foi restaurado, o próximo valor que será gerado para `actor_id` será o valor do último id registrado acrescido de 1. Por exemplo: se o último id registrado foi 200, o próximo valor gerado será 200 + 1.

![Tabela sakilaactor com restrição auto increment](https://content-assets.betrybe.com/prod/Tabela%20sakilaactor%20com%20restri%C3%A7%C3%A3o%20auto%20increment.png)

Tabela `sakila.actor` com restrição auto_increment

Com isso em mente, a coluna que possui **auto_increment** é omitida no `INSERT`, uma vez que o valor já é gerado automaticamente:


```sql
INSERT INTO sakila.actor (first_name, last_name)
VALUES('Marcelo','Santos');
```

![Resultado do insert em sakilaactor](https://content-assets.betrybe.com/prod/Resultado%20do%20insert%20em%20sakilaactor.png)

Resultado do `INSERT` em `sakila.actor`

### INSERT SELECT (Inserindo dados de uma outra tabela)

É possível inserir dados a partir de outra tabela usando `INSERT INTO SELECT`:


```sql
INSERT INTO tabelaA (coluna1, coluna2)
    SELECT tabelaB.coluna1, tabelaB.coluna2
    FROM tabelaB
    WHERE tabelaB.nome_da_coluna <> 'algumValor'
    ORDER BY tabelaB.coluna_de_ordenacao;
```

Assim, estaríamos extraindo a **coluna1** e a **coluna2** da **tabelaB** e as inserindo na **tabelaA**, de acordo com a condição que for passada no `WHERE`.

É possível usar também `SELECT * FROM` e copiar todos os dados de todas as colunas de uma tabela para outra, mas nessa situação a **tabelaA** e a **tabelaB** precisam **obrigatoriamente** possuir a mesma quantidade de colunas, e os tipos de dados das colunas correspondentes devem ser iguais.

Com essa funcionalidade, é fácil criar tabelas temporárias para testes ou por necessidade. Por exemplo, para trazer os dados da tabela `sakila.staff` para a tabela `sakila.actor`, poderíamos fazer:

```sql
INSERT INTO sakila.actor (first_name, last_name)
	SELECT first_name, last_name FROM sakila.staff;
```

![Resultado do insert em sakilaactor a partir de sakilastaff](https://content-assets.betrybe.com/prod/Resultado%20do%20insert%20em%20sakilaactor%20a%20partir%20de%20sakilastaff.png)

Resultado do `INSERT` em `sakila.actor` a partir de `sakila.staff`.



## `UPDATE` - alterando dados

Você avisou na recepção que seu nome é _Rannveig_, mas, quando foi ver em seu documento, foi registrado como _Ravein_! **“Poxa, será que meu nome é tão difícil assim de se escrever?”** Sua sorte é que o `UPDATE` te permite alterar valores de uma tabela com base em alguma condição.

**Vamos resolver isso!**

![Tabela sakilastaff com first_name errado](https://content-assets.betrybe.com/prod/Tabela%20sakilastaff%20com%20first_name%20errado.png)

Tabela `sakila.staff` com `first_name` errado


```sql
UPDATE sakila.staff
SET first_name = 'Rannveig'
WHERE first_name = 'Ravein';
```

![Tabela sakilastaff com first_name correto](https://content-assets.betrybe.com/prod/Tabela%20sakilastaff%20com%20first_name%20correto.png)

Tabela `sakila.staff` com `first_name` correto

Como foi exibido no código acima, a sintaxe geral para fazer um update é:


```sql
UPDATE nome_da_tabela
SET propriedade_a_ser_alterada = 'novo valor para coluna'
WHERE alguma_condicao; -- importantíssimo aplicar o WHERE para não alterar a tabela inteira!
```

Uma curiosidade sobre o `UPDATE` e o `DELETE` no **MySQL Server** é que, por padrão, existe uma configuração chamada **safe updates mode** que só vai te permitir executá-los caso eles incluam quais IDs devem ser modificados. Então, caso você tente fazer a _query_ abaixo, ela não funcionaria por não incluir o ID.

```sql
UPDATE sakila.staff
SET first_name = 'Rannveig'
WHERE first_name = 'Ravein';
```

Para evitar essa restrição, rode o seguinte comando em uma janela de _query_ dentro do **MySQL Workbench** **sempre** que abri-lo para desabilitar essa funcionalidade, antes de executar seus comandos de `UPDATE` ou `DELETE`:


```sql
SET SQL_SAFE_UPDATES = 0;
```

## Alterando mais de uma coluna ao mesmo tempo

Cadastrou um nome e sobrenome errado? 😦 Não se preocupe! Com o UPDATE resolvemos isso de um jeito bem simples! Basta inserir o nome da coluna que deseja alterar, em seguida definir o id do usuário e voilà, nome e sobrenome alterados.

```sql
UPDATE sakila.staff
SET first_name = 'Rannveig', last_name = 'Jordan'
WHERE staff_id = 4;
```

### `UPDATE` em massa

Por questões de performance, para que apenas uma solicitação de _query_ seja enviada ao servidor, podemos fazer uma atualização em massa.

```sql
-- Opção 1 - Incluindo a lista de condições fixas
UPDATE sakila.actor
SET first_name = 'JOE'
WHERE actor_id IN (1,2,3);

-- Opção 2 - Especificando como cada entrada será alterada individualmente
UPDATE sakila.actor
SET first_name = (
CASE actor_id WHEN 1 THEN 'JOE' -- se actor_id = 1, alterar first_name para 'JOE'
              WHEN 2 THEN 'DAVIS' -- se actor_id = 2, alterar first_name para 'DAVIS'
              WHEN 3 THEN 'CAROLINE' -- se actor_id = 3, alterar first_name para 'CAROLINE'
	      ELSE first_name -- em todos os outros casos, mantém-se o first_name
END);
```

Você pode ver mais informações sobre como usar o `CASE` [neste link](https://www.w3schools.com/sql/func_mysql_case.asp).

### Fazendo um UPDATE de forma sequencial

Se o comando `ORDER BY` for usado juntamente com o `UPDATE`, os resultados serão alterados na ordem em que forem encontrados.

Se o comando `LIMIT` for usado em conjunto com o `UPDATE`, um limite será imposto na quantidade de resultados que podem ser alterados. Caso contrário, todos os resultados que satisfizerem a condição serão atualizados.

Veja a sintaxe abaixo. Lembre-se de que os valores entre colchetes (`[]`) são opcionais:


```sql
UPDATE nome_da_tabela
SET coluna1 = valor1, coluna2 = valor2
[WHERE condições]
[ORDER BY expressao [ ASC | DESC ]]
[LIMIT quantidade_resultados];

-- Exemplo:
UPDATE sakila.staff
SET password = 'FavorResetarSuaSenha123'
WHERE active = 1
ORDER BY last_update
LIMIT 2;
```

Essas são as maneiras mais comuns de utilizar o `UPDATE` no dia a dia.



## Bônus - `--safe-updates`

Para quem está ainda está se familiarizando com o MySQL, o `--safe-updates` (ou -`-i-am-a-dummy`, sim, é uma propriedade real do **MySQL**) pode ser uma configuração segura para utilizar operadores de alteração de dados. Ele é útil para casos nos quais você tenha emitido um comando `UPDATE` ou `DELETE`, mas esquecido de incluir `WHERE` para indicar quais linhas devem ser modificadas, evitando que a _query_ atualize ou exclua todas as linhas da tabela.

O `--safe-updates` exige que você inclua um valor chave (_key value_), por exemplo os _ids_ (lembrando que os valores da coluna _id_ de uma tabela são do tipo `KEY`) dos itens selecionados, para executar o `UPDATE` ou o `DELETE`. Essa camada de segurança é importante em bancos reais executando em ambientes de produção e ajuda a prevenir acidentes. Esse modo também restringe _querys_ `SELECT` que produzem resultados muito grandes, com uma quantidade excessiva de linhas.

A opção `--safe-updates` exige que o mysql execute a seguinte instrução ao se conectar ao servidor:


```sql
SET sql_safe_updates=1, sql_select_limit=1000, max_join_size=1000000;
```

-   **`sql_select_limit`=1000**: limita o conjunto de resultados `SELECT` a 1.000 linhas, a menos que a instrução inclua `LIMIT`.
-   **`max_join_size`=1.000.000**: faz com que as instruções `SELECT` de várias tabelas produzam um erro se o servidor estimar que deve examinar mais de 1.000.000 combinações de linhas.

Você pode desabilitar o `--safe-updates` utilizando o comando `SET`:

```sql
SET SQL_SAFE_UPDATES = 0;
```

Ou configurar para um modo mais conveniente para você, alterando os valores das variáveis:


```sql
SET sql_safe_updates=1, sql_select_limit=500, max_join_size=10000;
```

Quando ocorre um erro de `--safe-updates`, a mensagem de erro inclui o primeiro diagnóstico que foi produzido, para fornecer informações sobre o motivo da falha. A mensagem pode, por exemplo, indicar que o `UPDATE` está sendo executado com um operador `WHERE` que não se refere a uma coluna do tipo `KEY` (veja o código abaixo). Nesse caso, você pode **desabilitar** o `--safe-updates`, ou utilizar uma coluna `KEY` como referência do seu operador `WHERE`. Lembre-se de que ler e interpretar os erros vai ajudar na sua solução!


```sql
-- Mensagem de erro retornada pelo workbench.

-- Error Code: 1175. You are using safe update mode and you tried to update a table without WHERE that uses a KEY column.
-- To disable safe mode, toogle the option in Preferences -> SQL Editor an reconnect.
```

Este erro ocorreu devido ao _Safe Update Mode_ estar habilitado.


## `DELETE` - removendo dados de uma tabela

Antes de aprender a excluir dados de uma tabela, é importante entender que nem sempre que você clicar em excluir, dentro de um sistema ou site, a informação terá sido **de fato** excluída do banco de dados. Em muitos casos, a funcionalidade de **“excluir”** apenas marcará a informação como inativa ou excluída, ou algum campo equivalente.

Isso ocorre pela necessidade de seguir normas ou regulamentos sobre disponibilidade e segurança de dados. Relatórios podem necessitar de informações que já foram “excluídas” ou pode ser necessário manter logs de uso (históricos de acontecimentos no sistema) de seu software.

## Excluindo dados de uma tabela

Para excluir dados de forma básica, temos a seguinte sintaxe:


```sql
DELETE FROM banco_de_dados.tabela
WHERE coluna = 'valor';
-- O WHERE é opcional. Porém, sem ele, todas as linhas da tabela seriam excluídas.
```

Exemplo no banco `sakila`:

```sql
DELETE FROM sakila.film_text
WHERE title = 'ACADEMY DINOSAUR';
```

⚠️ Importante: Novamente, caso o modo `--safe-updates` esteja habilitado, o comando `DELETE` só funcionaria se os IDs fossem incluídos em suas _queries_. Para fins de prática, vamos desabilitá-lo.

Novamente, para desabilitar o modo `--safe-updates`, rode o seguinte comando em uma janela de _query_ dentro do MySQL Workbench, sempre que abri-lo, antes de executar seus comandos `DELETE`:

Copiar

```sql
SET SQL_SAFE_UPDATES = 0;
```

## Meu `DELETE` não foi permitido…

Caso haja relações entre as tabelas (**primary key** e **foreign keys**) e existam restrições aplicadas a elas, ao executar o `DELETE` ocorrerá uma ação de acordo com a restrição que tiver sido imposta na criação da **foreign key**. Essas restrições podem ser as seguintes:

```sql
-- Rejeita o comando DELETE.
ON DELETE NO ACTION;

-- Rejeita o comando DELETE.
ON DELETE RESTRICT;

-- Permite a exclusão dos registros da tabela pai, e seta para NULL os registros da tabela filho.
ON DELETE SET NULL;

-- Exclui a informação da tabela pai e registros relacionados.
ON DELETE CASCADE;
```

Vamos analisar um exemplo prático:

```sql
DELETE FROM sakila.actor
WHERE first_name = 'GRACE';
```

Se tentar rodar essa _query_, você vai se deparar com o erro exibido na imagem abaixo:

![Erro ON DELETE RESTRICT](https://content-assets.betrybe.com/prod/Erro%20ON%20DELETE%20RESTRICT.png)

Erro ON DELETE RESTRICT

O banco de dados não vai permitir que você delete o ator chamado “GRACE”. Isso acontece porque a coluna `actor_id` da tabela `film_actor` é uma chave estrangeira (_foreign key_) que aponta para a coluna `actor_id` na tabela `actor`, e essa chave estrangeira possui a restrição `ON DELETE RESTRICT`. Se essa restrição não existisse, o ator seria deletado, deixando nosso banco de dados em um estado inconsistente, pois haveria linhas na tabela `film_actor` com um `actor_id` que não mais existiria!

Para conseguir excluir este ator em `actors`, precisamos primeiro excluir todas as referências a ele na tabela `sakila.film_actor`:

```sql
DELETE FROM sakila.film_actor
WHERE actor_id = 7; -- actor_id = 7 é o Id de GRACE
```

Após excluir as referências, podemos excluir o ator com o nome “GRACE”:

```sql
DELETE FROM sakila.actor
WHERE first_name = 'GRACE';
```

Antes de excluir dados que possuem restrições de chave estrangeira, como o exemplo que acabamos de ver, analise se você realmente deve excluir essa informação do banco de dados e depois, caso precise, faça de acordo com as restrições que foram impostas durante a criação da tabela.

As regras e restrições que acompanham _querys_ de alteração do banco (como o `UPDATE` e o `DELETE`) são importantes para manter a **Integridade dos Dados**, pois evitam mudanças involuntárias e garantem que as taxas de erro sejam menores, resultando em economia de tempo na solução de problemas. Um banco de dados que possui um sistema de integridade de dados bem controlado e bem definido aumenta a **estabilidade** das informações, **desempenho** das operações e **manutenção** das tabelas. Se existem restrições, não faz sentido simplesmente ignorá-las, temos que entender as motivações.

## `DELETE` VS `TRUNCATE`

Se tem certeza absoluta de que quer excluir os registros de uma tabela de uma maneira mais rápida, para efeitos de testes ou necessidade, o `TRUNCATE` é mais rápido que o `DELETE`. A função principal e única do `TRUNCATE` é de limpar (excluir todos os registros) de uma tabela, não sendo possível especificar o `WHERE`. Por isso, o `TRUNCATE` só pode ser usado nesse cenário.

```sql
TRUNCATE banco_de_dados.tabela;
```

Caso precise excluir condicionalmente, usando regras e especificações, use sempre o comando `DELETE` juntamente com o `WHERE`.


Todos os conceitos apresentados para se operar as informações em um banco de dados podem ser resumidos pelo conceito de [CRUD](https://developer.mozilla.org/pt-BR/docs/Glossary/CRUD).

-   **Adicionar** novas informações ao banco de dados, utilizamos o conceito **C**REATE com o comando:
    `INSERT INTO banco.tabela (coluna1, coluna2) VALUES (‘valor_A’, ‘valor_B’);`
    
-   **Obter** as informações armazenadas no bando de dados, utilizamos o conceito **R**EAD, com o comando:
    `SELECT colunaA, colunaB FROM banco.tabela;`
    
-   **Atualizar** informações existentes no banco de dados, utilizamos o conceito **U**PDATE com o comando:
    `UPDATE banco.tabela SET coluna1='valor' WHERE alguma_condicao;`
    
-   **Remover** informações existentes no banco de dados, utilizamos o conceito **D**ELETE com o comando:
    `DELETE FROM banco.tabela WHERE alguma_condicao;`


#### Recursos adicionais (opcional)

-   [Tutorial sobre `INSERT` do Guru99](https://www.guru99.com/insert-into.html)
-   [Tutorial sobre `INSERT` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-insert-statement.aspx)
-   [Tutorial sobre `UPDATE` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-update-data.aspx)
-   [Tutorial sobre `DELETE` e `UPDATE` do Guru99](https://www.guru99.com/delete-and-update.html)
-   [Tutorial sobre `DELETE` do MySQL Tutorial](https://www.mysqltutorial.org/mysql-delete-statement.aspx)
-   [Tutorial sobre `DELETE` do Tech On The Net](https://www.techonthenet.com/mysql/delete.php)
-   [Documentação sobre restrições de chaves estrangeiras no MySQL](https://dev.mysql.com/doc/refman/5.7/en/create-table-foreign-keys.html)


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/a66b200c-8dc8-4231-a33a-4262877856af/lesson/a9afd7c8-dc77-4670-982e-c4b28f64ee67)