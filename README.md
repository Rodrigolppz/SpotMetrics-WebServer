<h1 align=center> SPOT Metrics <img src="https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/images/spotmetrics_logo.jpg" width="28"/> - Web server com Docker e Traefik</h1>

### Desafio: 
<b>Configurar um ambiente Docker com Traefik como reverse proxy para expor um serviço web.</b>

### Tarefa:

1 - Criar um Docker Compose com Traefik configurado para rotear requisições
para um serviço web simples (por exemplo, um container rodando um servidor
Python Flask ou um pequeno site estático com Node.js)

2 - Configurar um roteamento dinâmico no Traefik (usando labels no docker-
compose.yml).

3 - Criar um dashboard do Traefik para visualizar os serviços expostos.

4 - Escrever instruções claras sobre como rodar o ambiente.

# 

# 1 - Criar o Docker Compose com Traefik configurado

Para essa primeira etapa, criei o arquivo [docker-compose.yaml](https://github.com/Rodrigolppz/SpotMetrics-WebServer/blob/main/spot-project/docker-compose.yaml). 

Neste arquivo configurei dois containers: um para o Traefik, que atua como proxy reverso e gerenciador de tráfego, e outro para o Flask, que hospeda o Web Server da aplicação.

 

