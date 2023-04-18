[[Docker]]
[[Docker - 11 Docker Compose]]


Vimos na seção anterior os comandos básicos para interagir com o _Compose_: subir e descer todos os serviços, visualizar seus logs e verificar seu status. Porém, podemos ter arquiteturas mais complexas de serviços dentro do _Compose_, por exemplo:

-   💾 Criar **volumes**: são pastas dentro de um serviço que é **persistente**, ou seja, mesmo após descer o serviço, esta pasta ainda mantém seus arquivos na próxima vez que os serviços subirem.
    
-   📶 Criar **redes virtuais**: onde alguns serviços podem se comunicar apenas em uma rede virtual #1, enquanto outros serviços podem se comunicar apenas em uma rede virtual #2.
    

## Criando Volumes

Os **volumes** nos permitem persistir arquivos entre execuções dos nossos serviços. Essa funcionalidade é super importante quando subimos serviços como **banco de dados**, onde precisamos manter os dados caso o serviço seja reiniciado.

![Não podemos deixar acontecer isso com os dados! 😅](https://content-assets.betrybe.com/prod/N%C3%A3o%20podemos%20deixar%20acontecer%20isso!%20%F0%9F%98%85.gif)

Não podemos deixar acontecer isso com os dados! 😅

Para criar volumes, vamos continuar com o mesmo arquivo `docker-compose.yaml` da seção anterior. Vamos criar um volume para o serviço **database** e para o **front-end**, demonstrando que mesmo descendo os serviços e subindo novamente, os dados ainda persistirão.

Veja nosso arquivo `docker-compose.yaml` abaixo. Copie e substitua seu arquivo local para acompanhar os exemplos. 😉

```yaml
version: "3"
services:
  frontend:
    build: frontend/
    restart: always
    ports:
      - 3000:3000
    depends_on:
      - backend
    volumes:
      - ./logs:/var/log/frontend
  backend:
    build: backend/
    restart: always
    ports:
      - 3001:3001
    environment:
      - DB_HOST=database
    depends_on:
      - database
  database:
    image: betrybe/docker-compose-example-database:v1
    restart: always
    volumes:
      - dados-do-banco:/data/db

volumes:
  dados-do-banco:
```

![Tem algo diferente nesse docker-compose.yaml!](https://content-assets.betrybe.com/prod/53e5e172-c23a-402e-973b-cd0631da7a0a-Tem%20algo%20diferente%20nesse%20docker-compose.yaml!.gif)

Tem algo diferente nesse docker-compose.yaml!

Vamos focar primeiro no final do arquivo, onde temos uma chave nova, chamada `volumes`. Nesta chave, especificamos para o _Compose_ que ele deve criar um volume virtual com o nome `dados-do-banco`. Porém, ainda precisamos mapear este volume para dentro de algum serviço!

```yaml
volumes:
  dados-do-banco:
```

Isso é feito pela nova chave `volumes` que está dentro do serviço **database**! Você pode perceber que esta chave é uma lista com um item e recebeu os dados no seguinte formato: `<nome-do-volume>:<caminho-no-container-para-montar>`. Ou seja: no serviço **database**, o caminho `/data/db` será **persistido**, mesmo se a gente descer e subir este serviço novamente! 🤩



```yaml
    volumes:
      - dados-do-banco:/data/db    # nome do disco virtual : caminho no container
```

> **Por que mapeamos o caminho “/data/db”?** 🤔 como este banco de dados é um MongoDB, seus dados são armazenados nesta pasta específica, segundo sua [documentação](https://www.mongodb.com/docs/manual/reference/configuration-options/#mongodb-setting-storage.dbPath).

Também tivemos um mapeamento de volume no serviço de **front-end**! Em sua nova chave `volumes`, temos um mapeamento diferente: neste caso, estamos mapeando uma pasta do nosso computador local (`./logs`) para uma pasta dentro do serviço de front-end (`/var/log/frontend`). Desta maneira, não precisamos criar volumes virtuais, pois estamos usando uma pasta do nosso próprio computador! 🤯

```yaml
    volumes:
      - ./logs:/var/log/frontend    # caminho no computador : caminho no container
```

Veja na figura abaixo uma ilustração das nossas alterações neste `docker-compose.yaml`:

![Integração entre volumes e serviços no Compose](https://content-assets.betrybe.com/prod/Integra%C3%A7%C3%A3o%20entre%20volumes%20e%20servi%C3%A7os%20no%20Compose.png)

Integração entre volumes e serviços no Compose

Agora, vamos subir os serviços com o comando abaixo e verificar como o _Compose_ se comporta com esta nova configuração.



```bash
docker-compose up -d
```

Veja o exemplo de saída da execução deste comando:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose up -d
Creating network "aula-docker-compose_default" with the default driver
Creating volume "aula-docker-compose_dados-do-banco" with default driver
Creating aula-docker-compose_database_1 ... done
Creating aula-docker-compose_backend_1  ... done
Creating aula-docker-compose_frontend_1 ... done
pessoa@trybe:~/aula-docker-compose$
```

Agora, vamos conferir se a pasta `logs` realmente foi criada na pasta atual, de acordo com o mapeamento de volume que fizemos para o serviço de **front-end**:

```bash
pessoa@trybe:~/aula-docker-compose$ ls
backend  docker-compose.yaml  frontend  logs
pessoa@trybe:~/aula-docker-compose$ cd logs/
logs.txt
pessoa@trybe:~/aula-docker-compose$ cat logs.txt

> front@0.1.0 start /opt/compose-example-front
> react-scripts start

ℹ ｢wds｣: Project is running at http://172.27.0.4/
ℹ ｢wds｣: webpack output is served from 
ℹ ｢wds｣: Content not from webpack is served from /opt/compose-example-front/public
ℹ ｢wds｣: 404s will fallback to /
Starting the development server...

Compiled successfully!

You can now view front in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://172.27.0.4:3000

Note that the development build is not optimized.
To create a production build, use yarn build.

pessoa@trybe:~/aula-docker-compose$
```

Viu que legal? Dentro do serviço de **frontend**, a aplicação está configurada para que os _logs_ sejam escritos no caminho `/var/log/frontend/logs.txt`. Entretanto, agora este mesmo arquivo aparece também em nossa pasta `logs` local. Perceba que isso serve como uma **ponte** entre nosso computador local e o serviço criado pelo _Compose_! 🤯

Agora, vamos **descer** nossos serviços e verificar se o volume virtual `dados-do-disco` é removido ou não. Vamos executar o comando `docker-compose down` e validar:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose down
docker-compose down
Stopping aula-docker-compose_frontend_1 ... done
Stopping aula-docker-compose_backend_1  ... done
Stopping aula-docker-compose_database_1 ... done
Removing aula-docker-compose_frontend_1 ... done
Removing aula-docker-compose_backend_1  ... done
Removing aula-docker-compose_database_1 ... done
Removing network aula-docker-compose_default
pessoa@trybe:~/aula-docker-compose$
```

Agora, vamos **subir** os serviços novamente e verificar se o volume `dados-do-disco` é recriado:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose up -d
Creating network "aula-docker-compose_default" with the default driver
Creating aula-docker-compose_database_1 ... done
Creating aula-docker-compose_backend_1  ... done
Creating aula-docker-compose_frontend_1 ... done
pessoa@trybe:~/aula-docker-compose$
```

Perceba que o _Compose_ não mostrou a linha **“Creating volume “aula-docker-compose_dados-do-banco” with default driver”**, como na execução do último comando de `docker-compose up`. Como o volume virtual já existe, ele manteve os arquivos e apenas fez o mapeamento deste volume já existente para o serviço **backend**! 🤩

## Criando redes virtuais

Da mesma forma que podemos criar volumes virtuais, o _Compose_ nos permite criar múltiplas **redes virtuais** entre os serviços. Isso é **muito importante**, pois nos permite criar arquiteturas mais seguras, por exemplo:

-   O serviço **front-end** só precisa se comunicar diretamente com o **back-end**;
-   O serviço **back-end** precisa se comunicar tanto com o **front-end** quanto com o **database**;
-   O serviço **database** só precisa se comunicar diretamente com o **back-end**.

Ao limitar as comunicações entre os serviços que não necessitam se comunicar de fato, acabamos criando uma arquitetura _segura_ e _robusta_ para os nossos serviços! Bora aprender como fazer isso? 👊

Primeiramente, vamos continuar utilizando o arquivo `docker-compose.yaml` que usamos para criar os volumes. Porém, o arquivo sofreu algumas modificações. Confira o arquivo completo abaixo:

```yaml
version: "3"
services:
  frontend:
    build: frontend/
    restart: always
    ports:
      - 3000:3000
    depends_on:
      - backend
    volumes:
      - ./logs:/var/log/frontend
    networks:
      - rede-virtual-1
  backend:
    build: backend/
    restart: always
    ports:
      - 3001:3001
    environment:
      - DB_HOST=database
    depends_on:
      - database
    networks:
      - rede-virtual-1
      - rede-virtual-2
  database:
    image: betrybe/docker-compose-example-database:v1
    restart: always
    volumes:
      - dados-do-banco:/data/db
    networks:
      - rede-virtual-2

volumes:
  dados-do-banco:

networks:
  rede-virtual-1:
  rede-virtual-2:
```

![Tem algo diferente nesse docker-compose.yaml novamente!](https://content-assets.betrybe.com/prod/53e5e172-c23a-402e-973b-cd0631da7a0a-Tem%20algo%20diferente%20nesse%20docker-compose.yaml!.gif)

Tem algo diferente nesse docker-compose.yaml novamente!

Vamos entender as novas alterações em nosso arquivo `docker-compose.yaml`:

-   No final do arquivo existe uma nova chave de primeiro nível `networks`:
    
    -   Em cada linha declaramos o nome de uma nova rede virtual;
    -   As redes virtuais permitem criar isolamento entre os serviços;
    -   Ao utilizar esta chave, o _Compose_ **não vai mais criar a rede virtual padrão**, como estava fazendo antes!
-   Dentro de cada serviço, também temos a nova chave `networks`:
    
    -   Para o **front-end**, declaramos que ele está presente na `rede-virtual-1`;
    -   Para o **back-end**, declaramos que ele está presente na `rede-virtual-1` e na `rede-virtual-2`;
    -   Para o **database**, declaramos que ele está presente na `rede-virtual-2`.

Veja na figura abaixo uma ilustração das nossas alterações neste `docker-compose.yaml`:

![Integração entre redes virtuais e serviços no Compose](https://content-assets.betrybe.com/prod/Integra%C3%A7%C3%A3o%20entre%20redes%20virtuais%20e%20servi%C3%A7os%20no%20Compose.png)

Integração entre redes virtuais e serviços no Compose

Simples, não? 🧐 Agora podemos criar quantas redes virtuais forem necessárias para o nível de isolamento que precisamos entre nossos serviços!


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/2f1a5c4d-74b1-488a-8d9b-408682c93724/lesson/5e65eb9b-6ffa-452d-ab14-1e4e2d47887f)