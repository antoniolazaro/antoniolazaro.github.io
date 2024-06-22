---
layout: post
title: Aumentando produtividade com Spring Boot + Docker
date: 22/06/2024
author: Antonio Lazaro
summary: Aumentando produtividade com Spring Boot + Docker
categories: [spring, springboot, produtividad, docker]
thumbnail: heart
---

## Sprint boot + Docker

O Spring Boot conta com um módulo de desenvolvimento capaz de gerar o arquivo compose do docker baseado nas dependencias do projeto a partir do [Spring Initializer](https://start.spring.io/).

Estou usando o Spring Boot 3.3.1 e Maven, porém acredito que seja agnóstico ao gerenciador de dependencias e deve funcionar com Gradle também. Configuracões de Beans, nem sempre funcionam bem, e em alguns casos, é necessário restart manual, mas para muitos cenário de mudancas que testei funcionou.

Configurar no pom.xml

{% highlight xml %}
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-docker-compose</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
{% endhighlight %}

### Pré-requisitos

Você precisa ter os aplicativos CLI docker e docker compose (ou docker-compose) no seu caminho. A versão mínima suportada do Docker Compose é 2.2.0.

### Ciclo de vida será

Por padrão, a aplicação do Spring Boot executa o comando docker compose up, que criará os contêineres definidos no arquivo, como por exemplo compose.yml, e os inicializarão. Os detalhes de conexão dos beans para esses serviços serão utilizados sem a necessidade de configurações adicionais.

- Quando este módulo é incluído como uma dependência, o Spring Boot fará o seguinte:
- Procurar por um compose.yml e outros nomes de arquivo comuns do compose em seu diretório de trabalho
- Chamar docker compose up com o compose.yml descoberto
- Criar beans de conexão de serviço para cada contêiner suportado
- Chamar docker compose stop quando o aplicativo for desligado

### Imagens suportadas

A lista completa pode ser obtida na [documentacão do Spring](https://docs.spring.io/spring-boot/reference/features/dev-services.html#features.dev-services.docker-compose)

Algumas imagens suportadas:

- Cassandra - cassandra
- Elasticsearch - elasticsearch
- Oracle database - gvenzl/oracle-xe
- MariaDB - mariadb
- Microsoft SQL server - mssql/server
- MySQL - mysql
- PostgreSQL - postgres
- MongoDB - mongo
- RabbitMQ - rabbitmq
- Redis - redis
- Zipkin - openzipkin/zipkin

### Exemplo de imagem

No meu teste com postgres e o módulo PgVector, ele baixou uma imagem do postgres com pgVector já habilitada.

{% highlight yml %}
services:
  pgvector:
    image: 'pgvector/pgvector:pg16'
    environment:
      - 'POSTGRES_DB=mydatabase'
      - 'POSTGRES_PASSWORD=secret'
      - 'POSTGRES_USER=myuser'
    labels:
      - "org.springframework.boot.service-connection=postgres"
    ports:
      - '5432'
{% endhighlight %}

## Conclusão

Outros poderosos recursos podem ser usados, como o suporte a imagem customizadas, não usar todos containers especificamente. Um outro projeto interessante que estou testando é o [Test Containers](https://java.testcontainers.org/) que cria containers para o escopo de testes, mas pretendo registrar o aprendizado em um post especifico dele.

Pra quem usa Intelij, ainda sugiro a instalacão do Plugin Docker ![](/static/img/plugin-docker.png)

## Fontes

- https://docs.spring.io/spring-boot/reference/features/dev-services.html#features.dev-services.docker-compose
- [<https://www.baeldung.com/spring-boot-devtools>](https://www.baeldung.com/docker-compose-support-spring-boot)
