[[Docker]]
[[Docker - 11 Docker Compose]]

Vimos na seção anterior como criar nosso arquivo _Compose_, chamado de `docker-compose.yaml`. Configuramos da seguinte maneira:

-   Três serviços, um deles usando uma imagem Docker **pronta** e dois com arquivo **Dockerfile**;
-   Mapeamos as portas de conexão;
-   Configuramos a política de reinicialização;
-   Criamos uma variável de ambiente;
-   Definimos a ordem de subida dos serviços.

Agora é o momento de finalmente fazer o _Compose_ trabalhar e seguir a nossa **receita** de serviços!

## Subindo todos os serviços

Chamamos o ato de executar todos os serviços do _Compose_ de **subir**. Para subir todos os serviços, utilizamos o comando `docker-compose up` no terminal.

> ⚠️ Lembre-se que o arquivo `docker-compose.yaml` deve estar na mesma pasta da execução deste comando.

Vamos começar?

![Vamos subir!](https://content-assets.betrybe.com/prod/Vamos%20subir!.gif)
`Vamos subir!`

Execute o comando abaixo:

```bash
docker-compose up -d
```

Veja um exemplo de saída da execução deste comando:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose up -d
Creating network "aula-docker-compose_default" with the default driver
Creating aula-docker-compose_database_1 ... done
Creating aula-docker-compose_backend_1  ... done
Creating aula-docker-compose_frontend_1 ... done
pessoa@trybe:~/aula-docker-compose$
```

Você deve ter percebido que usamos uma flag (`-d`) no comando acima. A flag `-d` serve para executarmos todos os serviços no modo **segundo plano**. Sem esta flag, os logs dos três serviços aparecem no console simultaneamente, dificultando a leitura. Porém, nós podemos ler os logs de cada um dos serviços posteriormente, usando o comando `docker-compose logs <nome-do-serviço>`.

> 👀 **De olho na dica:** a flag `-d` do _Compose_ funciona da mesma forma quando executamos um container em segundo plano usando o comando `docker run -d <nome-da-imagem>` com o **Docker**!

O _Compose_ vai respeitar as regras de ordem de inicialização que especificamos, conforme a figura abaixo:

![Ordem da criação dos serviços](https://content-assets.betrybe.com/prod/Ordem%20da%20cria%C3%A7%C3%A3o%20dos%20servi%C3%A7os.png)

Ordem da criação dos serviços

O _Compose_ vai executar todos os containers especificados, baixando as imagens do Registry (Docker Hub), de acordo com o que foi especificado no arquivo. Outro detalhe importante é que, nesse momento, além de executar os containers, o _Compose_ vai criar uma **rede virtual padrão** entre esses containers, permitindo a comunicação entre eles, conforme podemos ver na figura abaixo.

![Rede virtual padrão permite a comunicação entre todos os serviços](https://content-assets.betrybe.com/prod/Rede%20virtual%20padr%C3%A3o%20permite%20a%20comunica%C3%A7%C3%A3o%20entre%20todos%20os%20servi%C3%A7os.png)

Rede virtual padrão permite a comunicação entre todos os serviços

## Verificando o status dos serviços

Agora precisamos visualizar o **status** dos nossos serviços, faremos isso usando o comando `docker-compose ps`. Este comando traz um resumo do nome interno dos containers, se os containers estão saudáveis e se as portas foram mapeadas corretamente. Veja um exemplo da saída da execução deste comando:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose ps
             Name                           Command               State                    Ports                  
------------------------------------------------------------------------------------------------------------------
aula-docker-compose_backend_1    npm start                        Up      0.0.0.0:3001->3001/tcp,:::3001->3001/tcp
aula-docker-compose_database_1   docker-entrypoint.sh mongod      Up      27017/tcp                               
aula-docker-compose_frontend_1   npm start                        Up      0.0.0.0:3000->3000/tcp,:::3000->3000/tcp
pessoa@trybe:~/aula-docker-compose$
```

Podemos observar que os três serviços estão saudáveis e com as portas mapeadas!

_Vamos acessar o nosso front-end e verificar se deu tudo certo?_ 🤔

Para isso, abra um navegador web e acesse o endereço `http://localhost:3000`. Você verá a seguinte página abaixo:

![Página inicial do nosso frontend](https://content-assets.betrybe.com/prod/P%C3%A1gina%20inicial%20do%20nosso%20frontend.png)

Página inicial do nosso frontend

Ufa, deu tudo certo! 🚀

## Reconstruindo a Imagem Docker

É comum fazer várias alterações em nosso código durante a fase de desenvolvimento. Algumas dessas alterações nos obrigam a **reconstruir** a Imagem Docker, ou seja, precisamos _forçar_ a execução do `docker build` novamente.

Para exemplificar,vamos alterar o arquivo Dockerfile do **front-end**, onde substituiremos a linha de ENTRYPOINT. O novo arquivo `~/aula-docker-compose/frontend/Dockerfile` ficará assim:


```dockerfile
FROM betrybe/docker-compose-example-frontend:v1
ENTRYPOINT ["sh", "-c", "npm start > /var/log/frontend/logs.txt"]
```

Podemos deixar nítido que as imagens precisam ser construídas novamente usando o _Compose_. Para isso, utilizamos a flag `--build`, junto com o comando `docker-compose up`. Veja o exemplo de saída do comando abaixo:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose up -d --build
Building backend
[...]
Successfully tagged aula-docker-compose_backend:latest
Building frontend
[...]
Successfully tagged aula-docker-compose_frontend:latest
aula-docker-compose_database_1 is up-to-date
aula-docker-compose_backend_1 is up-to-date
Recreating aula-docker-compose_frontend_1 ... done
pessoa@trybe:~/aula-docker-compose$
```

> 🥇 Veja que legal: ambas as imagens acima foram reconstruídas, **back-end** e **front-end**. Entretanto, o _Compose_ fez a atualização apenas do serviço **front-end**, o qual foi o único que sofreu alterações de fato em sua Imagem Docker.

## Descendo todos os serviços

Chamamos o ato de parar a execução de todos os serviços do _Compose_ de **descer**. Se quisermos descer nossos serviços, podemos utilizar o comando `docker-compose down`. Com ele, todos os containers serão parados e removidos. Vamos testar?

![Se conseguimos subir, precisamos aprender a descer!](https://content-assets.betrybe.com/prod/Se%20conseguimos%20subir,%20precisamos%20aprender%20a%20descer!.gif)
`Se conseguimos subir, precisamos aprender a descer!`

Veja um exemplo da saída da execução deste comando:


```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose down
Stopping aula-docker-compose_frontend_1 ... done
Stopping aula-docker-compose_backend_1  ... done
Stopping aula-docker-compose_database_1 ... done
Removing aula-docker-compose_frontend_1 ... done
Removing aula-docker-compose_backend_1  ... done
Removing aula-docker-compose_database_1 ... done
Removing network aula-docker-compose_default
pessoa@trybe:~/aula-docker-compose$
```

Perceba que o comando parou todos os serviços em execução, e após isso, também removeu os containers e a rede virtual padrão criada pelo comando `docker-compose up`.

## Subindo serviços específicos

Além de subir e descer, é possível **subir apenas parte dos serviços**! Por exemplo: imagine que precisamos apenas executar o serviço de **back-end**. Logo, os únicos serviços necessários nesta demanda são o **database** e o próprio **back-end**. Para isso, podemos usar o comando `docker-compose up <serviço>`.

Se fizermos isso, o _Compose_ vai incluir também suas dependências, como podemos ver no exemplo abaixo, seguindo com nosso arquivo `docker-compose.yaml`, se rodarmos o comando:


```bash
docker-compose up backend
```

Agora, veja o exemplo de saída da execução deste comando:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose up -d backend
Creating network "aula-docker-compose_default" with the default driver
Creating aula-docker-compose_database_1 ... done
Creating aula-docker-compose_backend_1  ... done
pessoa@trybe:~/aula-docker-compose$
```

Veja que o _Compose_ também criou e executou o serviço **database**, o qual definimos no `docker-compose.yaml` como dependência do **back-end**, por meio do parâmetro `depends_on`. Veja a figura abaixo ilustrando o processo:

![Subindo apenas o serviço de backend e suas dependências](https://content-assets.betrybe.com/prod/Subindo%20apenas%20o%20servi%C3%A7o%20de%20backend%20e%20suas%20depend%C3%AAncias.png)

Subindo apenas o serviço de backend e suas dependências

## Visualizando os logs dos serviços

Outro comando importante do _Compose_ é o `docker-compose logs <nome-do-serviço>`. Com este comando, podemos ver os _logs_ de nossos serviços de maneira semelhante como fazemos unitariamente com os containers. Aqui, podemos especificar um serviço para visualizar seus _logs_, ou ver todos os _logs_ de todo o ambiente, conforme o arquivo do _Compose_.

![Precisamos saber ler os logs sempre!](https://content-assets.betrybe.com/prod/Precisamos%20saber%20ler%20os%20logs%20sempre!.gif)

Precisamos saber ler os logs sempre!

Dado que já executamos os serviços de **back-end** e **database**, vamos visualizar seus logs usando o comando abaixo:

```bash
docker-compose logs backend
```

Agora, veja o exemplo de saída da execução deste comando:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose logs backend
Attaching to aula-docker-compose_backend_1
backend_1   | 
backend_1   | > back@1.0.0 start /opt/compose-example-back
backend_1   | > node .
backend_1   | 
backend_1   | Rodando o aplicativo de back-end na porta 3001
pessoa@trybe:~/aula-docker-compose$
```

Para limitar a quantidade de linhas de _logs_ retornadas pelo comando, podemos usar a flag `--tail` especificando quantas linhas desejamos que o comando retorne. Para isso, execute o seguinte comando abaixo:

```bash
docker-compose logs --tail 5 database
```

Agora veja o exemplo de saída da execução deste comando, que retorna as últimas 5 linhas de _log_ do serviço de **database**:

```bash
pessoa@trybe:~/aula-docker-compose$ docker-compose logs --tail 5 database
Attaching to aula-docker-compose_backend_1
database_1  | {"t":{"$date":"2022-05-06T18:58:38.078+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1651863518:78878][1:0x7f9d38ef9700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 26, snapshot max: 26 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 7"}}
database_1  | {"t":{"$date":"2022-05-06T18:59:38.089+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1651863578:89135][1:0x7f9d38ef9700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 28, snapshot max: 28 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 7"}}
database_1  | {"t":{"$date":"2022-05-06T19:00:38.135+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1651863638:135455][1:0x7f9d38ef9700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 30, snapshot max: 30 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 7"}}
database_1  | {"t":{"$date":"2022-05-06T19:01:38.156+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1651863698:156695][1:0x7f9d38ef9700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 32, snapshot max: 32 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 7"}}
database_1  | {"t":{"$date":"2022-05-06T19:02:38.174+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1651863758:174719][1:0x7f9d38ef9700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 34, snapshot max: 34 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 7"}}
pessoa@trybe:~/aula-docker-compose$
```

> 👀 **De olho na dica:** de maneira similar ao comando no **Docker**, podemos utilizar a flag `-f` ou `--follow` para acompanhar em tempo real as saídas dos containers. Para sair, use `Ctrl+C` ou `Command+C`.

E aí, o que achou dos comandos básicos do _Compose_? Entendeu a importância dele de permitir gerenciar múltiplos containers de uma vez? Agora vamos deixar nosso arquivo `docker-compose.yaml` mais robusto, pois vamos aprender a criar **redes e volumes virtuais** para nossos serviços. Bora? 🐋

Não se esqueça de descer todos os serviços para continuarmos na próxima seção! 🤘

```bash
docker-compose down
```



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/5987fa2d-0d04-45b2-9d91-1c2ffce09862/day/2f1a5c4d-74b1-488a-8d9b-408682c93724/lesson/9ddf6558-dc4c-4fca-a841-13684ae8df25)