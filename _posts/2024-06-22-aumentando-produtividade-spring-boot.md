---
layout: post
title: Aumentando produtividade com Spring Boot
date: 22/06/2024
author: Antonio Lazaro
summary: Aumentando produtividade com Spring Boot
categories: [spring, springboot, produtividade]
thumbnail: heart
---

## Sprint boot + Hot reload

Em outras linguagens de programacao e ambientes de desenvolvimentos (IDEs) como node.js com VS Code e GoLang vi que existiam formas de automaticamente a IDE identificar mudancas e fazer reload do projeto. Pesquisei como poderia ter isso em um ambiente Java com Spring Boot e Intelij e vi que existia uma feature que eu pouco utilizava.

Estou usando o Spring Boot 3.3.1 e Maven, porém acredito que seja agnóstico ao gerenciador de dependencias e deve funcionar com Gradle também. Configuracões de Beans, nem sempre funcionam bem, e em alguns casos, é necessário restart manual, mas para muitos cenário de mudancas que testei funcionou.

Configurar no pom.xml

{% highlight xml %}
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
{% endhighlight %}

No Intelij é necessário habilitar o suporte a compilacão automática.

Marcar as duas opcões abaixo:

Settings -> Build, Execution, Deployment -> Compiler -> Marcar a opcão (Build project automatically)
![](/static/img/build-automatically.png)

Settings -> Advanced Settings -> Marcar a opcão 'Allow auto-make to start even if developed application is currently running'
![](/static/img/advance-settings-intelij.png)

## Conclusão

Existem outros recursos no Spring Boot dev tools, porém , só esse recurso que eu precisava no momento e os demais, tentarei usar posteriormente, mas a documentacão está disponível nas referências e é possível descobrir mais pontos que podem ajudar na produtividade.

Features disponíveis:

- Property Defaults: Usado para desenvolvimento de frontend com Thymeleaf
- Automatic Restart - Usado para desenvolvimento de APIs
- LiveReload - Usado para desenvolvimento com front end para recarregar browser
- Remote Debug Tunneling: Usado para debug remoto
- Remote Update and Restart: Usado para debug remoto

Caso deseje desabilitar basta configurar essa propriedade: <b>spring.devtools.restart.enabled=false</b>

## Fontes

- <https://docs.spring.io/spring-boot/reference/using/devtools.html>
- <https://www.baeldung.com/spring-boot-devtools>
- <https://www.javatpoint.com/spring-boot-devtools>
