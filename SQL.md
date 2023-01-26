[[Banco de Dados]]

  
Atualmente, a análise de dados é indispensável para empresas e pessoas em processos de tomada de decisão. Essa é uma das maneiras mais eficientes de gerar conhecimento, tanto utilizando dados passados quanto fazendo projeções futuras.

Feita uma análise inicial dos dados, seus resultados serão transformados em _informações_ que, depois de estudadas, podem vir a gerar _conhecimentos_ que, por sua vez, se tornam uma vantagem competitiva para as empresas, além de um norte para decisões individuais.

Uma das formas de como nós, profissionais da tecnologia da informação, podemos contribuir para isso, é gerando e disponibilizando os dados necessários para análise. Isso pode ser feito através de tabelas e consultas criadas dentro de um **banco de dados**, utilizando a linguagem **SQL**.

![Diagrama front-end x back-end](https://content-assets.betrybe.com/prod/Diagrama%20front-end%20x%20back-end.png)

Para entendermos mais sobre como podemos gerenciar essas informações a nosso favor, precisamos entender um pouco sobre o fluxo de trabalho de uma pessoa desenvolvedora back-end que lida com banco de dados. Ele funciona assim:

O front-end faz a requisição para o back-end, o back-end faz a conexão e consulta o banco de dados. Então o banco retorna alguma informação para o back-end, e é aqui que a API (Application Programming Interface) trabalha. O back-end será responsável por processar essas informações, recebendo requisições, enviando respostas e, por sua vez, alimentando o front-end.

## O que é SQL?

**SQL** (_Structured Query Language_) é a linguagem mais usada para criar, pesquisar, extrair e também manipular dados dentro de um _banco de dados relacional_. Para que isso seja possível, existem comandos como o `SELECT`, `UPDATE`, `DELETE`, `INSERT` e `WHERE`, entre outros.

## Como essas informações (tabelas) são armazenadas?

Todas as pesquisas realizadas dentro de um banco de dados são feitas em tabelas. Tabelas possuem linhas e colunas. Linhas representam um exemplo, ou instância, daquilo que se deseja representar, ao passo que colunas descrevem algum aspecto da entidade representada.

Por exemplo, a imagem a seguir apresenta uma tabela com dados sobre pessoas. Cada linha na tabela representa uma pessoa específica. As colunas descrevem uma característica que queremos armazenar sobre as pessoas; nesse caso, são nome, sobrenome e email.

![Ilustração de linhas e colunas em uma tabela](https://content-assets.betrybe.com/prod/Ilustra%C3%A7%C3%A3o%20de%20linhas%20e%20colunas%20em%20uma%20tabela.png)

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/695be3a1-74b5-4c1d-9381-b3655397a00f)

