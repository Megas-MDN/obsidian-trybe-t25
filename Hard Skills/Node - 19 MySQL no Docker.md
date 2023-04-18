[[Node]]
[[Mysql]]
[[Docker]]


Chegou o grande momento no qual você realizará consultas a um banco de dados MySQL por meio de uma API REST desenvolvida com o auxílio do _Express_. 🥳

Além disso, colocaremos _Docker_ nessa receita! Ou melhor, criaremos uma receita com o _docker compose_ que permitirá o uso do _MySQL_ dentro de um _container Docker_!

Utilizar containers para acessar serviços `prontos para o uso` em vez de instalar tudo no seu computador tem se tornado uma prática comum no mercado de trabalho.

Dessa forma você está criando um ambiente de desenvolvimento flexível, que pode ser facilmente versionado em um repositório, facilitando o seu compartilhamento e garantindo que ele se comporte da mesma forma em diferentes computadores, evitando o famoso problema **na minha máquina funciona**.

Ao final do dia, você terá uma aplicação que fará todas as operações de um **CRUD** e conseguirá entender ainda como integrar todos os conhecimentos adquiridos até agora no módulo de Back-end, construindo uma _API REST_ com _Express_, utilizando _MySQL_ e _Docker_!

![Não acredito, quero ver!](https://content-assets.betrybe.com/prod/56bf3cfa-796d-4611-bed5-b96b9373f660-N%C3%A3o%20acredito,%20quero%20ver!.gif)
Não acredito, quero ver!

Chegou a hora de colocar a mão na massa! Vamos então colocar o container docker para funcionar?

Você criará um `docker compose` que iniciará um ambiente com o container _MySQL_ que você utilizará ao longo do dia. 😎

Na raiz do projeto (diretório **trybecash-api**), vamos criar o arquivo `docker-compose.yaml` com o seguinte conteúdo:

```yaml
version: '3'
services:
  database:
    image: mysql:8.0.29
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: trybecashdb
    ports:
      - "33060:3306"
```

No arquivo `docker-compose.yaml` criado, foi definido um serviço chamado **database**. Esse serviço inicializará um container _Docker_ com a imagem do Servidor MySQL versão 8.0.29.

O parâmetro **restart** define a política de reinício do container como **always**. Assim, o container sempre será reiniciado automaticamente em caso de parada. Na seção **environment** foi definido o valor de duas variáveis dentro do container:

-   **MYSQL_ROOT_PASSWORD**: Essa variável define a senha do usuário root do MySQL (será a senha que utilizaremos para acessar o MySQL);
-   **MYSQL_DATABASE**: Essa variável define o nome do banco de dados que será criado ao iniciar MySQL, caso ele não exista.

Já a seção **ports** está vinculando uma **porta** do seu computador local (a porta 33060) a uma **porta** dentro do container (a porta 3306).

> ⚠️ **Atenção:** estamos utilizando a porta `33060` como a porta vinculada ao seu computador local com o container MySQL com a intenção de evitar um possível conflito de portas, caso você possua uma instalação do MySQL em seu computador usando a porta `3306`! 😉

Para iniciar nossos containers, precisaremos criar um arquivo chamado `Dockerfile` na raiz do projeto, com o seguinte conteúdo:

```dockerfile
 FROM node:16
 # o expose serve apenas para sinalizar em qual porta rodaremos o container
 # a definição da porta se dá no arquivo docker-compose.yaml
 EXPOSE 3000
 WORKDIR /
 # aqui copiamos apenas o package.json e o package-lock.json, pois assim
 # garantimos que quando as dependências forem instaladas, suas versões não vão ser alteradas.
 COPY package*.json ./
 RUN npm install
 COPY . .
 CMD [ "npm", "start" ]
```

Após a criação do `Dockerfile`, devemos configurar um container para rodar nossa aplicação Node.js em nosso arquivo `docker-compose.yaml`. Dessa forma, garantimos que ambos os ambientes funcionarão corretamente.

Deixaremos, portanto, nosso arquivo `docker-compose.yaml` da seguinte forma:

Copiar

```yaml
 version: '3'
 services:
   node:
     build: 
       dockerfile: ./Dockerfile
       context: .
     # Imagem base do container
     image: node:16
     # Nome do container para facilitar execução
     container_name: trybecash_api
     # Restarta a imagem caso algo a faça parar
     restart: always
     # Diretório padrão de execução
     working_dir: /app
     # Lista de volumes (diretórios) mapeados de fora para dentro do container
     volumes:
       # Monta o diretório atual, com todos os dados da aplicação, dentro do diretório /app
       - ./:/app
     ports:
       # Expõe a porta padrão da aplicação: altere aqui caso use outra porta
       # na notação porta_de_fora:porta_de_dentro
       - 3000:3000
     # Informa ao docker, para que o container node seja iniciado após o container database
     depends_on:
       - "database"
   database:
     image: mysql:8.0.29
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: root
       MYSQL_DATABASE: trybecashdb
     ports:
       - "33060:3306"
```

Após a criação dos arquivos com o conteúdo apresentado. Comece inicializando o container em segundo plano com o uso do seguinte comando:

```bash
docker-compose up -d
```

Nesse ponto, a estrutura de arquivos e diretórios do seu projeto deve estar assim:

Copiar

```bash
.
 ├── tests/
     │   └── -
     ├── docker-compose.yaml
     ├── Dockerfile
     └── package.json
```

Agora que temos dois containers, um com a aplicação Node e outro com o MySQL, podemos iniciar o desenvolvimento do projeto **TryberCash**.

![Vamos que vamos!](https://content-assets.betrybe.com/prod/Vamos%20que%20vamos!.gif)
Vamos que vamos!


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/6b700197-22c6-4a2d-b791-b66d5247d3f0/lesson/fd58ce04-aa48-4b7b-8f8a-575afafdd734)
