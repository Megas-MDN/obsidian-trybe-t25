[[Banco de Dados]]
[[SQL]]

## _Constraints_ (restrições), chaves primárias e chaves estrangeiras

Uma das grandes vantagens de armazenar seus dados em um banco de dados é possibilitar a criação de restrições ou regras (_constraints_, em inglês). Essas restrições limitam os tipos de dados de uma coluna em uma determinada tabela, o que fornece assertividade e confiabilidade em seu banco de dados. Em outras palavras, podemos dizer que se você tentar executar alguma ação que viole as regras da _constraint_, a ação não será concluída.

Como as _constraints_ são aplicadas às **colunas** das tabelas, é possível assegurar que os dados inseridos nelas serão consistentes **conforme as regras definidas**. Veja alguns tipos de _constraints_:

-   **NOT NULL** - Garante que aquele campo **não pode conter valores nulos**, ou seja, se não houver um valor padrão (`DEFAULT`) definido, será sempre necessário passar um valor para esse campo durante a inserção ou alteração de dados.
-   **UNIQUE** - Garante que o valor inserido na coluna da tabela é **único**, isto é, não pode haver outro valor igual para esta coluna registrado nesta tabela.
-   **PRIMARY KEY** - Garante que o valor seja a _chave primária_ da tabela, ou seja, que a coluna que possui essa _constraint_ aplicada seja **o identificador único da tabela**. Ela também é, por definição, **não nula** (mesmo efeito da _constraint NOT NULL_) e **única** (mesmo efeito da _constraint UNIQUE_).
-   **FOREIGN KEY** - Garante que o valor seja uma _chave estrangeira_ da tabela, ou seja, faça referência à chave primária (valor em uma coluna com a _constraint PRIMARY KEY_) **de outra tabela**, permitindo um relacionamento entre tabelas.
-   **DEFAULT** - Garante que, caso nenhum valor seja inserido na coluna (ou caso a pessoa usuária insira um valor nulo), a _constraint_ **colocará o valor padrão passado para ela**.

Assim, durante a criação de uma tabela, ao se pensar em suas colunas, podemos avaliar quais _constraints_ podemos aplicar àquela informação. Por exemplo, imagine uma tabela que liste os sabores de sorvete de uma sorveteria. Nessa tabela, temos três colunas: um código identificador, o nome do sabor do sorvete e o código identificador de quem fornece. Vamos ver cada coluna e pensar em quais _constraints_ podemos adicionar a elas:

-   **Código identificador (id)** - Para o id do sorvete, precisamos que ele _identifique e represente_ o sabor do sorvete na tabela, então podemos adicionar como _constraint_ a **PRIMARY KEY**.
-   **Nome** - Aqui, queremos que os valores sejam únicos, afinal, não temos a necessidade de cadastrar um novo sabor de sorvete que já conste na tabela. Além disso, queremos que, ao cadastrar, o valor não seja nulo. Então, como _constraints_, podemos adicionar **UNIQUE** e **NOT NULL**.
-   **Código identificador de quem fornece (id)** - Suponha que já possuímos uma tabela onde listamos todas as empresas fornecedoras, e que nessa tabela, os valores estão sendo representados por uma _primary key_. Então, podemos atribuir como _constraint_ a **FOREIGN KEY**.


# O que é uma entidade?

Quando se fala de entidades de um banco de dados, estamos normalmente falando de uma tabela que representa algum conceito do mundo real que você quer descrever (pessoa, eventos, acontecimentos) e suas propriedades (altura, horário do evento, nome do acontecimento). A entidade **_pessoa_**, por exemplo, pode ter as propriedades de altura, peso e idade. Uma entidade **_festa_** pode possuir as propriedades horário do evento, público-alvo e data da festa. Por fim, uma entidade **_venda_** pode possuir as propriedades valor da venda, dia da venda, produto vendido etc.

**Entidade**: Pessoa. **Propriedades**: Altura, peso, idade.

A entidade é nossa tabela dentro de um banco de dados e as propriedades fazem parte dessa tabela.

Em alguns desses casos, as entidades são individuais e não se relacionam entre si, porém, às vezes, elas são ligadas umas às outras através de relacionamentos.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/d0e24258-bb98-4676-86e4-ad8b84a5d1c9)