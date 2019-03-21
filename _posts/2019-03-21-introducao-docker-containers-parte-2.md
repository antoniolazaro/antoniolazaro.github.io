---
layout:     post
title:      Introdução docker e containers - Parte 2
date:       21/03/2019
author:     Antonio Lazaro
summary:    Introdução a docker
categories: [docker,container,devops]
thumbnail:  heart

---
![](/static/img/docker.png)

Continuando a série de posts sobre Docker e containers, baseado na <a href="https://docs.docker.com/get-started/part2/" target="_blank">documentação oficial do docker</a>. 


## Um pouco de teoria

Nesse post falaremos sobre como criar um container. Caso tenha perdido a definição de container, você pode ir no [post anterior da série](https://antoniolazaro.dev/docker/container/devops/2019/03/21/introducao-docker-containers.html).
<br/> _Dockerfile:_ Arquivo de configuração que descreve o que o container conterá. Configurações de rede, portas que o mundo externo enxergará, bem como file system, devem ser configurados nesse arquivo. Preste atenção pois o nome do arquivo é *Dockerfile* e isso faz total diferença pro Docker que é case sentive.

## Prática
Falando rapidamente sobre o conceitual, vamos para a parte prática do objetivo do post.

Para usuários de Linux Debian based (Ubuntu, Mint). Segue passo a passo. Meu caso, utilizei Mint 19.

1. Crie um diretório vazio em sua máquina: `mkdir teste-docker`
1. Entre no diretório: ```cd teste-docker```
1. Crie um arquivo chamado ```Dockerfile``` (atenção para o nome) com o conteúdo abaixo:
<br/>

```Dockerfile 
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]

### Comandos
```
1. Crie um arquivo chamado ```app.py``` no mesmo diretório com o conteúdo abaixo: <br/>

```python
from flask import Flask
from redis import Redis, RedisError
import os
import socket

# Connect to Redis
redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)

app = Flask(__name__)

@app.route("/")
def hello():
    try:
        visits = redis.incr("counter")
    except RedisError:
        visits = "<i>cannot connect to Redis, counter disabled</i>"

    html = "<h3>Hello {name}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>" \
           "<b>Visits:</b> {visits}"
    return html.format(name=os.getenv("NAME", "world"), hostname=socket.gethostname(), visits=visits)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

1. Crie um arquivo chamado ```requirements.txt``` no mesmo diretório com o conteúdo abaixo: <br/>

```
Flask
Redis
```
1. Caso não tenha o pip (<a href="https://pypi.org/project/pip/" target="_blank">gerenciador pacotes Python.</a>) instalado em sua máquina rodar o comando ```sudo apt-get install python-pip```. 
1. Após isso executar o comando: ```docker build --tag=friendlyhello .```. Esse comando construirá uma imagem com a tag _friendlyhello_.
1. Para verificar listar através do comando ```docker image ls```.
1. Certificando que a imagem foi criada, executar ela através do comando: ```docker run -p 4000:80 friendlyhello```.
1. Para testar acessar o navegador através do endereço: <a href="http://localhost:4000" target="_blank"> http://localhost:4000.</a> 
<br/>![](/static/img/docker-http-run-result.png)
1. Ou executar o comando: ```curl http://localhost:4000```
<br/>![](/static/img/docker-curl-run-result.png)

1. Para matar a sessão no terminal ```CTRL+C```.
1. Para rodar em background ```docker run -d -p 4000:80 friendlyhello```. (_-d_)
1. Para verificar a imagem: ```docker container ls```
1. Para parar a imagem: ```docker container stop id_imagem```

## Comapartilhando sua imagem docker com outras pessoas.

Através do <a href="https://hub.docker.com" target="_blank"> portal dockerhub</a> é possível obter imagens e fornecer suas imagens para comunidade. Funciona como um repositório de imagens docker. Para fazer isso com a imagem criada na etapa anterior, basta seguir o passo a passo:

1. ```docker login``` (então você entra com seu username e senha do docker hub. Atenção porque ele pede username e não email.).
1. ```docker tag friendlyhello gordon/get-started:part2```. Esse comando "comita" localmente sua imagem no seu repositório local de imagens.
1. ```docker image ls``` e você verá a imagem.
1. ```docker push username/repository:tag``` para você criar sua imagem remotamente e partir dai outros devem podem ter acesso a sua imagem.
1. ```docker run -p 4000:80 username/repository:tag```. Para testar a imagem publicada.

## Lista de novos comandos aprendidos:

1. ```docker build -t friendlyhello .```  # Create image using this directory's Dockerfile
1. ```docker run -p 4000:80 friendlyhello```  # Run "friendlyname" mapping port 4000 to 80
1. ```docker run -d -p 4000:80 friendlyhello```         # Same thing, but in detached mode
1. ```docker container ls```                                # List all running containers
1. ```docker container ls -a```             # List all containers, even those not running
1. ```docker container stop <hash>```           # Gracefully stop the specified container
1. ```docker container kill <hash>```         # Force shutdown of the specified container
1. ```docker container rm <hash>```        # Remove specified container from this machine
1. ```docker container rm $(docker container ls -a -q)```         # Remove all containers
1. ```docker image ls -a```                             # List all images on this machine
1. ```docker image rm <image id>```            # Remove specified image from this machine
1. ```docker image rm $(docker image ls -a -q)```   # Remove all images from this machine
1. ```docker login```             # Log in this CLI session using your Docker credentials
1. ```docker tag <image> username/repository:tag```  # Tag <image> for upload to registry
1. ```docker push username/repository:tag```            # Upload tagged image to registry
1. ```docker run username/repository:tag```                   # Run image from a registry

### Fontes:
1. https://docs.docker.com/get-started/part2/
1. https://leanpub.com/dockerparadesenvolvedores (*livro Fantástico*) <a href="https://twitter.com/gomex" target="_blank">Autor: Gomex</a>
