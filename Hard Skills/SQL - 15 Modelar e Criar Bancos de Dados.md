[[Banco de Dados]]
[[SQL]]

[Normatização](#Normatização)

# Database Design - Como modelar um banco de dados

1.  Identificar as **entidades**, **atributos** e **relacionamentos** com base na descrição do problema:
    
    1.1 Por exemplo, a entidade `álbum` possui os atributos `título` e `preço` e se relaciona com a entidade `artista`.
    
2.  Construir um **diagrama entidade-relacionamento** para representar as entidades encontradas no passo 1:
    
    2.1 O diagrama serve como um guia para que você possa visualizar as entidades (tabelas) que irão se relacionar.
    
3.  **Criar um banco de dados** para conter suas tabelas:
    
    3.1 Após analisar e criar um diagrama de como o seu banco de dados vai ser estruturado, você pode dar início a criação dele.
    
4.  **Criar e relacionar tabelas** tendo o diagrama do passo 2 como base:
    
    4.1 Após criar seu banco de dados, você pode começar a criar e relacionar as tabelas de acordo com o diagrama.
    

A seguir, você vai aprender com mais detalhes cada um desses passos.

## 1) Identificando entidades, atributos e relacionamentos

Primeiramente você deve identificar as **entidades**, **atributos** e **relacionamentos** com base na descrição do problema, que é criar um catálogo de álbuns musicais. Porém, antes disso é necessário entender o significado de cada um deles.

### Entidades

São uma representação de algo do mundo real dentro do banco de dados e que normalmente englobam toda uma ideia. São armazenadas em formato de tabelas em um banco de dados.

**Hora de praticar 💻:** Busque identificar quais objetos devem se tornar entidades no seu catálogo de álbuns musicais e depois expanda o código abaixo para verificar.

↓ Ver entidades

### Atributos

Um atributo é tudo aquilo que pode ser usado para descrever algo. Por exemplo, uma entidade **pessoa** pode ter **nome**, **altura**, **peso** e **idade** como atributos.

**Hora de praticar 💻:** Considerando a história sobre um catálogo de álbuns musicais, tente deduzir quais propriedades descrevem cada uma das entidades encontradas anteriormente.

↓ Ver atributos

### Relacionamentos:

Os relacionamentos servem para representar como uma entidade deve estar ligada com outra(s) no banco de dados. Há três tipos de relacionamentos possíveis em um banco de dados, são eles:

-   Relacionamento Um para Um (1..1);
-   Relacionamento Um para Muitos ou Muitos para Um (1..N);
-   Relacionamento Muitos para Muitos (N..N).

**Hora de praticar 💻:** Volte à estrutura de tabelas do **Catálogo de Álbuns** e tente identificar quais tipos de relacionamentos existem entre as tabelas. Escreva-os em algum lugar e depois expanda abaixo para ver os relacionamentos.

↓ Ver Relacionamentos

> _Se sua interpretação foi diferente, não se preocupe. A maneira como você modelará o banco de dados varia de acordo com a sua interpretação e escala._

### 2) Construindo um diagrama entidade-relacionamento

No segundo passo, será construído um **diagrama entidade-relacionamento** para representar as entidades encontradas no passo 1.

Existem diversas ferramentas para modelar os relacionamentos em um banco de dados. Hoje será usada a [**draw.io**](https://draw.io/)

Agora é preciso montar um diagrama de relacionamento básico que demonstra como uma entidade é relacionada com a outra, usando o modelo `EntidadeA` + verbo + `EntidadeB`.

Considerando as entidades `Álbum`, `Artista`, `Estilo Musical` e `Canção`, foi construído o seguinte diagrama:

![Relacionamento entre as entidades `Álbum`, `Artista`, `Estilo Musical` e `Canção`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Relacionamento%20entre%20as%20entidades%20%60%C3%81lbum%60,%20%60Artista%60,%20%60Estilo%20Musical%60%20e%20%60Can%C3%A7%C3%A3o%60.png)

Relacionamento entre as entidades `Álbum`, `Artista`, `Estilo Musical` e `Canção`

O que você deve fazer quando estiver construindo seu próprio banco de dados é entender quantas vezes uma entidade pode se relacionar com uma outra, para, a partir disso, você poder criar esse primeiro diagrama, como o do exemplo acima, que mostra como as entidades estão relacionadas entre si.

### Montando um diagrama mais detalhado

Para diagramas ER (entidade-relacionamento) mais detalhados, deve-se incluir o nome das tabelas, suas chaves primárias e estrangeiras, suas colunas e seus relacionamentos.

> **De olho na dica 👀:** Por questão de convenções e boas práticas na criação de tabelas, não são usados acentos ou espaços entre os nomes das tabelas. **Lembre-se 🧠:** Existem várias maneiras de se modelar um banco de dados. Então, caso pense diferente do modelo abaixo, entenda que existem diversas formas de se resolver um mesmo problema.

![Relacionamento detalhado entre as tabelas `Artista`, `Album`, `EstiloMusical` e `Cancao`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Relacionamento%20detalhado%20entre%20as%20tabelas%20%60Artista%60,%20%60Album%60,%20%60EstiloMusical%60%20e%20%60Cancao%60.png)

Relacionamento detalhado entre as tabelas `Artista`, `Album`, `EstiloMusical` e `Cancao`

**Relacionamentos presentes entre as tabelas acima:**

-   Tabelas `Artista` e `Album`:
    
    As tabelas `Artista` e `Album` possuem um relacionamento de **um para muitos** (1..N), em que um artista pode possuir um ou mais álbuns.
    

![Tabelas `Artista` e `Album`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Tabelas%20%60Artista%60%20e%20%60Album%60.png)

Tabelas `Artista` e `Album`

-   Tabelas `Album` e `Cancao`:
    
    A tabela `Album` possui um relacionamento de **um para muitos** (1..N) com a tabela `Cancao`, uma vez que um álbum pode conter várias canções.
    

![Tabelas `Album` e `Cancao`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Tabelas%20%60Album%60%20e%20%60Cancao%60.png)

Tabelas `Album` e `Cancao`

-   Tabelas `Album` e `EstiloMusical`:
    
    A tabela `EstiloMusical` também possui um relacionamento de **um para muitos** (1..N) com a tabela `Album`, uma vez que um estilo musical pode estar contido em vários álbuns.
    

![Tabelas `Album` e `EstiloMusical`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Tabelas%20%60Album%60%20e%20%60EstiloMusical%60.png)

Tabelas `Album` e `EstiloMusical`

> **Anota aí 📣:** A ideia de um diagrama ER é prover uma **representação gráfica** para a estrutura de seu banco de dados, **descrevendo suas entidades com seus atributos e como elas se relacionam**. Essa visualização pode te ajudar tanto a criar e modelar seu banco de dados quanto a entender se sua modelagem precisa ser alterada ou se houve algum erro ao pensar na organização de suas entidades. Com esse diagrama você consegue pensar um pouco mais antes de começar a escrever as _queries_ para criar as tabelas.

Hora de voltar ao **MySQL Workbench** e criar um banco de dados!

![Doc Brown feliz em voltar para o MySQL Workbench](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Doc%20Brown%20feliz%20em%20voltar%20para%20o%20MySQL%20Workbench.gif)

Doc Brown feliz em voltar para o MySQL Workbench

Fonte: [https://www.tenor.com](https://www.tenor.com/)

### 3) Criando um banco de dados para conter suas tabelas

Agora que você já tem um diagrama que representa as tabelas que precisam ser criadas, já pode botar a mão no código. 💻

Ao lidar com a criação e gerenciamento de um banco de dados, você precisará conhecer os seguintes comandos:

```sql
-- Cria um banco de dados com o nome especificado.
CREATE DATABASE nome_do_banco_de_dados;

-- `CREATE DATABASE` ou `CREATE SCHEMA` fazem a mesma coisa.
CREATE SCHEMA nome_do_banco_de_dados;

-- Verifica se o banco de dados ainda não existe.
-- Essa verificação é comumente utilizada junto ao CREATE DATABASE para evitar
-- a tentativa de criar um banco de dados duplicado, o que ocasionaria um erro.
IF NOT EXISTS nome_do_banco_de_dados;

-- Lista todos os bancos de dados existentes.
SHOW DATABASES;

-- Define o banco de dados ativo para uso no momento.
USE nome_do_banco_de_dados;
```

Considerando o problema que precisa ser resolvido, hora de criar um banco de dados chamado `albuns`.

```sql
CREATE DATABASE IF NOT EXISTS albuns;
```

![Banco de dados `albuns` criado com sucesso](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Banco%20de%20dados%20%60albuns%60%20criado%20com%20sucesso.png)

Banco de dados `albuns` criado com sucesso

### 4) Criando e modelando tabelas de acordo com um diagrama ER

O objetivo para essa seção é criar as seguintes tabelas:

![Relacionamento detalhado entre tabelas `Artista`, `Album`, `EstiloMusical` e `Cancao`](https://content-assets.betrybe.com/prod/375f1fdf-bfba-4540-9321-a432910a545b-Relacionamento%20detalhado%20entre%20as%20tabelas%20%60Artista%60,%20%60Album%60,%20%60EstiloMusical%60%20e%20%60Cancao%60.png)

Relacionamento detalhado entre tabelas `Artista`, `Album`, `EstiloMusical` e `Cancao`

# Normalização

Os conceitos de normalização permitem que você aprofunde seus conhecimentos nas estruturas relacionais fundamentais, o que colabora para a tomada de decisões mais assertivas e seguras.

Essa confiança será importantíssima no momento de fazer modificações em estruturas de bancos de dados existentes ou criar novas estruturas do zero.

## 1ª Forma Normal

Para iniciar a organização de um banco de dados, devemos nos atentar para a `Primeira Forma Normal` - base de todas as outras. Seus preceitos são:

-   Colunas devem possuir apenas um valor;
-   Valores em uma coluna devem ser do mesmo tipo de dados;
-   Cada coluna deve possuir um nome único;
-   A ordem dos dados registrados em uma tabela não deve afetar a integridade dos dados.


## 2ª Forma Normal

Para a `Segunda Forma Normal`, devemos atentar para o seguinte:

-   A tabela deve estar na 1ª Forma Normal;
-   A tabela não deve possuir dependências parciais.

Uma dependência parcial pode ser considerada como qualquer coluna que não depende exclusivamente da chave primária da tabela para existir. Por exemplo, considere uma tabela **Pessoa Estudantes** que possui as seguintes colunas:

id | nome | data_matricula | curso
---|---| --- | --- 
1 | Samuel | 2020-09-01 | Física
2 | Joana | 2020-08-15 | Biologia
3 | Taís | 2020-07-14 | Contabilidade
4 | André | 2020-06-12 | Biologia

A coluna `curso` pode ser considerada uma dependência parcial, pois é possível mover os valores dessa coluna para uma outra tabela exclusiva para cursos. Os dados dessa tabela exclusiva para cursos podem existir independente de existir uma `pessoa estudante` vinculada a esse `curso` ou não. Dessa forma, depois de normalizar, teríamos duas tabelas:

## Cursos

id | nome
---| ---
1 | Física
2 | Biologia
3 | Contabilidade


## Pessoas Estudantes

id | nome | data_matricula | curso_id
-- | -- |-- | -- 
 1 | Samuel | 2020-09-01 | 1
2 | Joana | 2020-08-15 | 2
3 | Taís | 2020-07-14 | 3
4 | André | 2020-06-12 | 2

Dessa forma, foi possível aplicar a `Segunda Forma Normal` na tabela **Pessoas Estudantes**. Lembre-se que a função da normalização não é necessariamente reduzir o número de colunas mas remover redundâncias e possíveis anomalias de inclusão, alteração ou remoção de dados.


## 3ª Forma Normal

Por fim, a `Terceira Forma Normal` estabelece que:

-   A tabela deve estar na 1ª e 2ª Formas Normais;
-   A tabela não deve conter atributos (colunas) que não sejam **dependentes exclusivamente da _PK_** (chave primária).

## Livros

livro_id | categoria_id | categoria | valor
-- | -- | -- | --
1 | 1 | Romance | 29,90
2 | 2 | Policial | 34,90
3 | 3 | Ficção | 19,90
4 | 4 | Terror | 44,90

Observando a tabela acima, podemos notar que a coluna `categoria` depende da coluna `categoria_id`, que não é a _PK_ da tabela.

Quando um atributo (coluna) for dependente de outra coluna que não seja _PK_ ou que não seja dependente **unicamente** da _PK_, como é o caso do exemplo acima, sua adequação à `Terceira Forma Normal` poderá se dar separando esse atributo em uma outra tabela. Dessa forma, ficaríamos com as tabelas assim:

## Livros, tabela normalizada

livro_id | categoria_id | valor
-- | -- | --
1 | 1 | 29,90
2 | 2 | 34,90
3 | 3 | 19,90
4 | 4 | 44,90

## Categorias

categoria_id | categoria
-- | --
1 | Romance
2 | Policial
3 | Ficção
4 | Terror


Você pode conferir [aqui](https://docs.microsoft.com/pt-br/office/troubleshoot/access/database-normalization-description#normalizing-an-example-table) um resumo sobre cada uma das Formas Normais, bem como sua aplicação na prática.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/a10ee6b2-77b9-493f-ab76-a8f9822c5608/day/c04b45a4-0412-45ee-b2a9-de3d923a4ded/lesson/7f07a687-f50b-42e9-bab4-1bde21ad9207)