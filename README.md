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


 

