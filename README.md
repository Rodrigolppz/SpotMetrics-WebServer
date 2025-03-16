<h1 align=center> SPOT Metrics <img src="https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/images/spotmetrics_logo.jpg" width="28"/> - Web server com Docker e Traefik</h1>

### Desafio: 
<b>Configurar um ambiente Docker com Traefik como reverse proxy para expor um serviço web.</b>

### Tarefa:

1 - Criar um Docker Compose com Traefik configurado para rotear requisições
para um serviço web simples (por exemplo, um container rodando um servidor
Python Flask ou um pequeno site estático com Node.js).

2 - Configurar um roteamento dinâmico no Traefik (usando labels no docker-
compose.yml).

3 - Criar um dashboard do Traefik para visualizar os serviços expostos.

4 - Escrever instruções claras sobre como rodar o ambiente.

# 

# 1 - Criar o arquivo Docker Compose 

Para essa primeira etapa, criei o arquivo [docker-compose.yaml](https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/spot-project/docker-compose.yaml). 

Neste arquivo configurei dois containers: um para o Traefik, que atua como proxy reverso e load balancer, e outro para o Flask, que hospeda o Web Server da aplicação.

# 

# 2 - Criar labels para configurar o roteamento dinâmico no Traefik

Dentro do docker-compose.yml, no serviço web (container Flask), configurei as labels para que o Traefik faça o roteamento dinâmico automaticamente, sem necessidade de configurações manuais adicionais.

```
labels:
      - "traefik.enable=true"
      - "traefik.http.routers.web.rule=Host(`localhost`)" # Roteia para localhost
      - "traefik.http.services.web.loadbalancer.server.port=80"
```

<b>traefik.enable=true</b> → Habilita o serviço Flask no Traefik.

<b>traefik.http.routers.flask.rule=Host(localhost)</b> → Define a regra de roteamento, ou seja, todas as requisições para http://localhost serão direcionadas para o Flask.

<b>traefik.http.services.flask.loadbalancer.server.port=5000</b> → Diz ao Traefik que o Flask está rodando na porta 5000.

# 3 - Criar um dashboard do Traefik 

No serviço <b>Traefik</b> dentro do docker-compose.yaml, tem a seguinte linha:

```
"--api.insecure=true"
```
Isso habilita a interface web do Traefik.

E esta linha nos <b>ports</b> expõe o dashboard na porta 8080:

```
- "8080:8080"
```

# 4 - Instruções sobre como testar na sua máquina

Para testar esse projeto é necessário que esteja utilizando Linux. Vou ensinar o passo a passo tanto usando WSL quanto usando Linux como host principal ou VM.

## Passo a passo WSL

1 - Instale no windows o [Docker desktop](https://www.docker.com/products/docker-desktop/) (o docker desktop já vem com o docker compose instalado)

2 - Após instalado, ative a integração do Docker desktop com o WSL. ( No docker destkop, Engrenagem canto superior direito > Resources > WSL_Integration >  Enable integration with my default WSL distro > apply and restart)

3 - Abra o WSL e digite `docker ps` para testar se o docker está funcionando corretamente.

5 - Clone este repositório utilizando `git clone https://github.com/Rodrigolppz/SpotMetrics-WebServer.git`

6 - Mova-se até o diretório onde se encontra o arquivo <b>docker-compose.yaml</b> -> `cd /SpotMetrics-WebServer/spot-project`

7 - Para iniciar a aplicação, digite `docker-compose up -d`

8 - Por fim, basta abrir o seu browser e digitar `localhost:8080`. Na porta 8080 é aonde está o dashboard do traefik mostrando as rotas e detalhes da nossa aplicação. Digitando `localhost:80` será mostrada a seguinte mensagem > "Hello World from Flask in a uWSGI Nginx Docker container with Python 3.8 (default)", indicando que o servidor Flask dentro do contêiner Nginx está ativo e funcionando corretamente.

## Passo a passo LINUX 

1 - Instale docker utilizando o comando `sudo apt install docker-cli` ou `sudo apt install docker`

2 - Instale docker-compose utilizando `sudo apt install docker-compose`

3 - Clone este repositório utilizando `git clone https://github.com/Rodrigolppz/SpotMetrics-WebServer.git`

4 - Mova-se até o diretório onde se encontra o arquivo <b>docker-compose.yaml</b> -> `cd /SpotMetrics-WebServer/spot-project`

5 - Para iniciar a aplicação, digite `sudo docker-compose up -d`

6 - Por fim, basta abrir o seu browser e digitar `localhost:8080`. Na porta 8080 é aonde está o dashboard do traefik mostrando as rotas e detalhes da nossa aplicação. Digitando `localhost:80` será mostrada a seguinte mensagem > "Hello World from Flask in a uWSGI Nginx Docker container with Python 3.8 (default)", indicando que o servidor Flask dentro do contêiner Nginx está ativo e funcionando corretamente.

![imagem](https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/images/webserver.jpg)

![imagem](https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/images/dashboard.jpg)

