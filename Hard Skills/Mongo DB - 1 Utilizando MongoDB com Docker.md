[[Mongo DB]]

Agora vamos aprender a utilizar o **Mongo** via **Docker,** dispensando a necessidade de um serviço sempre em execução na sua máquina de desenvolvimento.

Antes de iniciar os trabalhos, certifique-se de que o Docker está instalado em sua máquina e em execução.

Com o Docker rodando, agora nós precisamos obter a imagem do Mongo que será o molde para criarmos nossos containers. Para isto, executamos o comando abaixo.

Copiar

```bash
1docker pull mongo:4
```

Note que estamos baixando a versão 4 do Mongo, a qual será utilizada nesta seção. Caso queira baixar uma outra versão, basta alterar a tag - que representa a versão desejada - em `mongo:tag`.

## Iniciando uma instância do Mongo Server

Para executar esta imagem você pode usar a linha abaixo.

> De olho na dica 👀: caso queira usar um software externo para acessar o servidor, como Mongo for Vscode ou Mongo Compass, é necessário mapear a porta 27017 do container para o seu localhost com o `-p`.

Copiar

```bash
1docker run --name <nome-do-container> -d mongo:4
```

No comando abaixo você disponibiliza um container mapeando sua porta 27017 para a porta 27017 do localhost.

Copiar

```bash
1docker run --name <nome-do-container> -d -p 27017:27017 mongo:4
```

## Executando o shell do Mongo no Docker

O comando `docker exec` permite que você execute comandos dentro de um container do Docker. O comando a seguir executará o Mongo dentro do container Docker que criamos anteriormente.

Copiar

```bash
1docker exec -it <nome-do-container-ou-id> mongo
```

**Obs:** você pode usar o comando `mongosh` no lugar de `mongo` para ter acesso ao shell com [novos recursos](https://www.mongodb.com/blog/post/introducing-the-new-shell).

## Importando arquivos locais para dentro do container utilizando `mongoimport`

A ferramenta [`mongoimport`](https://docs.mongodb.com/database-tools/mongoimport/) importa conteúdo de um arquivo `JSON`, `CSV` ou `TSV` criada por `mongoexport` ou, potencialmente, outra ferramenta de exportação de terceiros. Utilizamos esse recurso num container da seguinte forma:

1.  No primeiro passo, copiamos o arquivo que será importado para dentro do nosso container.

Copiar

```bash
1docker cp nome-do-arquivo.json <nome-do-container-ou-id>:/tmp/nome-do-arquivo.json
```

2.  No segundo passo, realizamos a importação do arquivo `JSON` para o MongoDB.

Copiar

```bash
1docker exec <nome-do-container-ou-id> mongoimport -d <nome-do-banco> -c <nome-da-coleção> --file /tmp/nome-do-arquivo.json
```

## Importar uma matriz JSON (`Array` de dados) com `mongoimport`

Pode ocorrer casos onde você terá vários documentos contidos em uma matriz `JSON` em um único arquivo, similar ao exemplo a seguir:

Copiar

```json
1 [
2    { title: "Informação 1", description: "Valor de exemplo 1"},
3    { title: "Informação 2", description: "Valor de exemplo 2"}
4 ]
```

Você poderá importar dados usando a seguinte sintaxe de exemplo adicionando o parâmetro `--jsonArray`:

Copiar

```bash
1 docker exec <nome-do-container-ou-id> mongoimport --collection='from_array_file' --file='one_big_list.json' --jsonArray
```

Importante observar que caso esqueça de adicionar a opção `--jsonArray`, `mongoimport` falhará com o erro:

Copiar

```bash
1  cannot decode array into a Document.
```

Isso ocorre porque os documentos são equivalentes a objetos `JSON`, não arrays. Você pode armazenar um array como um _value_ em um documento, mas um documento não pode ser um array.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/da82d65f-2261-4bcb-87bb-71e6a7e565f5/lesson/aa623c56-1ee6-4ab8-acde-2571ecc86e25)