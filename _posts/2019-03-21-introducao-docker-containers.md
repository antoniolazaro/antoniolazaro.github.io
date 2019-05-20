---
layout:     post
title:      Introdução docker e containers - Parte 1
date:       21/03/2019
author:     Antonio Lazaro
summary:    Introdução a docker
categories: [docker,container,devops]
thumbnail:  heart

---

## Introdução

![](/static/img/docker.png)

O objetivo desse post é mostrar como fazer um hello word com docker no linux

## Um pouco de teoria
No início a confusão mais comum entre quem inicia estudando sobre docker, acredito que seja que se pensa muito em virtualização (VM), o que nos remete a softwares como <a href="https://www.virtualbox.org/" target="_blank">Virtual Box</a> ou <a href="https://www.vmware.com/" target="_blank">VMware</a>. A diferença basicamente é que quando se fala em containers ainda estamos falando em virtualização, porém em um nível diferente da virtualização usando máquinas virtuais. A máquina virtual roda um sistema operacional inteiro em cima de uma outra máquina acessando os recursos através de um hypervisor.

Containers é uma tecnologia criada no sistema Linux que permite empacotar e isolar processos de maneira completa em uma estrutura de diretórios fazendo com  oque o sistema que está dentro do container esteja isolado do restante do sistema operacional.

Containers docker nada mais são que processos isolados que utilizam recursos do SO para executar um determinado software (Banco de dados, servidor de aplicação, etc).

A figura abaixo ilustra a diferença.
<br/>
![](/static/img/docker-virtualizacao.png)
<br/>_fonte:<a href="https://docs.docker.com/get-started/" target="_blank">Docker Get Started</a>_

## Prática
Falando rapidamente sobre o conceitual, vamos para a parte prática do objetivo do post.

Para usuários de Linux Debian based (Ubuntu, Mint). Segue passo a passo. Meu caso, utilizei Mint 19.

1. ```sudo apt-get update```
1. ```sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common```
1. ```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```
1. ```sudo apt-key fingerprint 0EBFCD88```
1. Resultado deve ser conforme tela abaixo:
<br/>![](/static/img/docker-finger-print.png)
1. ```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"```
1. ```sudo apt-get update```
1. ```sudo apt-get install docker-ce docker-ce-cli containerd.io```
1. ```sudo docker run hello-world```
<br/>![](/static/img/docker-hello-world.png)
1. Para instalar uma outra imagem com um ubuntu instalado: ```docker run -it ubuntu bash```
1. Para sair do Ubuntu digite ```exit```

### Comandos

1. Listar todas as imagens instaladas: ```docker image ls```
<br/>![](/static/img/docker-ls-result.png)
1. Listar todos processos docker rodando: ```docker ps_``` ou ```docker container ls```
<br/>![](/static/img/docker-ps-result.png)
1. Mostrar versão instalada do docker: ```docker --version``` ou ```docker version```
1. Help: ```docker container --help```
1. Informações sobre docker na máquina: ```docker info```

### Fontes:
1. https://docs.docker.com/get-started/
1. https://docs.docker.com/install/
1. https://leanpub.com/dockerparadesenvolvedores (*livro Fantástico*) <a href="https://twitter.com/gomex" target="_blank">Autor: Gomex</a>
