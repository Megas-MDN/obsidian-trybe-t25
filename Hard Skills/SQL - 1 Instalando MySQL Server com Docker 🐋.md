[[Banco de Dados]]
[[Docker]]
[[SQL]]


## Executando um container com MySQL

Agora vamos criar e iniciar um container **MySQL**, com o comando:

Copiar

```bash
docker container run --name container-mysql -e MYSQL_ROOT_PASSWORD=senha-mysql -d -p 3306:3306 mysql:5.7
```

### O que estamos fazendo aqui?

-   **–name**: Nomeia o container, assim facilitando a identificação do mesmo;
    
-   **-e**: Utilizada para informar nossas variáveis de ambiente.(aqui vamos manter o usuário _root_, e então, passaremos a variável _MYSQL_ROOT_PASSWORD=senha-mysql_ para poder usar dentro do container);
    
-   **-d**: Faz com que o container rode em segundo plano;
    
-   **-p**: Indica qual porta no nosso sistema operacional o docker estará em funcionamento. A porta `3306 do lado esquerdo` é a porta do nosso sistema, que receberá o container e a porta `3306 lado direito` é a porta do container. **Lembrando que 3306 é a porta padrão do _MySQL_**;
    
-   **run**: responsável por criar e iniciar o container;
    

> 👀 Observação: No comando acima, informamos a versão 5.7, ao final do comando! Se não tivéssemos informado, o docker iria utilizar a imagem mais recente (_latest_) disponível no [Docker Hub](https://hub.docker.com/_/mysql).

### Parando container

Para parar o container, você pode usar o comando:


```bash
docker container stop container-mysql
```

### Iniciando container

Para voltar a execução do container, você pode usar o comando:


```bash
docker container start container-mysql
```

### Removendo container

Para excluir o container, você pode usar o comando:


```bash
docker container rm container-mysql
```

Se você parou, ou deletou um container errado, não se preocupe. Você pode executá-lo novamente, com os comandos citados anteriormente.


## MySQL na linha de comando

Após seguir os passos anteriores, você poderá agora acessar seu servidor pela linha de comando. Para visualizar quais bancos de dados estão disponíveis, através do modo interativo do docker, você deve acessar o terminal do container-mysql:

```bash
docker exec -it container-mysql bash
```

Em seguida, acessar o mysql dentro do container. Lembre-se de usar a mesma senha usada na criação do container:


```bash
mysql -u root -p
```

É possível ver todos os bancos de dados que estão instalados atualmente digitando o seguinte comando. `Não se esqueça do ponto e vírgula :)`


```sql
SHOW DATABASES;
```

![SHOW DATABASES;](https://content-assets.betrybe.com/prod/a7cce98a-5511-46c8-b1c5-ec5e39459af9-SHOW%20DATABASES;.gif)

SHOW DATABASES;

## Comandos mais comuns

> 👀 Observação: _Por convenção, utilizamos as palavras chave do SQL em caixa alta para diferenciar das indicações de tabelas e colunas. Ah, é fundamental utilizar o `;` (ponto e vírgula) ao final de cada comando SQL, caso contrário ele não irá funcionar._

1.  O comando `USE` serve pra definir a **referência do banco de dados que será utilizado na query**:

```sql
USE nome_do_banco_de_dados_que_quero_conectar;
-- EX: USE trybe;
```

1.1 Uma outra forma de fazer referência ao banco, sem ter que rodar o `USE` é no formato `banco_de_dados.tabela`:


```sql
SELECT * FROM banco_de_dados.tabela;
-- EX: SELECT * FROM trybe.students;
```

2.  Para retornar todas as tabelas inicializadas no seu server:


```sql
SHOW TABLES;
```

3.  Visualizar estrutura de uma tabela:


```sql
DESCRIBE nome_da_tabela;
-- EX: DESCRIBE students;
```

4.  Criar um banco de dados:


```sql
CREATE DATABASE nome_do_banco_de_dados;
-- EX: CREATE DATABASE trybe;
```

## Vamos treinar!

Usando os comandos que você acabou de aprender, resolva os seguintes desafios:

1.  Entre no banco de dados `mysql`.
2.  Visualize todas as tabelas desse banco.
3.  Visualize a estrutura de pelo menos 10 tabelas diferentes e tente entender o tipo de estrutura que costuma ser utilizada.
4.  Crie um novo banco de dados com o seu nome e depois entre nele!

Pronto! Agora você pode executar comandos **SQL** dentro do seu banco de dados sem usar a interface gráfica, o que pode ser útil em alguns cenários em que você não tem acesso ao **MySQL Workbench**.










### Solução

1.  Entre no banco de dados mysql.


```bash
mysql -u root -p
```

2.  Visualize todas as tabelas desse banco.


```sql
USE nome_do_banco_de_dados_aqui;
SHOW TABLES;
```

3.  Visualize a estrutura de pelo menos 10 tabelas diferentes e tente entender o tipo de estrutura que costuma ser utilizada. Solução: Realize o comando com o nome das 10 tabelas que deseja com o seguinte comando:

```sql
DESCRIBE nome_da_tabela;
```

4.  Crie um novo banco de dados com o seu nome e depois entre nele!


```sql
CREATE DATABASE seu_nome_aqui;
USE seu_nome_aqui;
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/9ec435bd-40d0-494c-b168-d31f040f0690)

