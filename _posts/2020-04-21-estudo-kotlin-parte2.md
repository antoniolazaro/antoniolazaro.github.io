---
layout: post
title: Aprendizado Kotlin - Configurando ambiente de desenvolvimento Kotlin
date: 21/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Configurando ambiente de desenvolvimento Kotlin
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

A [Plural Sight](https://www.pluralsight.com/offer/2020/free-april-month){:target="\_blank"} está com uma promoção para o mês de abril onde os cursos da plataforma estão todos abertos devido a situação da COVID-19. Diante disso, me cadastrei na plataforma e fiz o curso ["Getting Started With Kotlin"](https://app.pluralsight.com/library/courses/8251eea9-5847-4881-bc94-1c3e0dc8b42e/table-of-contents){:target="\_blank"} by [Kevin Jones](https://app.pluralsight.com/profile/author/kevin-jones){:target="\_blank"} (conta dele no [twitter:](https://twitter.com/kevinrjones?lang=en){:target="\_blank"}).

Meu primeiro contato com Kotlin foi durante a seleção da Jaya onde fiz um projeto usando [Kotlin e Gradle com Javalin, Koin e Exposed](https://github.com/antoniolazaro/octo-events){:target="\_blank"}.

O curso ele tem duração de 2h, e cobre uma introdução, fala um pouco sobre programação orientada a objetos, funcional, interoperabilidade Java x Kotlin e vice-versa, e fala sobre a ferramenta de testes Spek.

## Configurando ambiente desenvolvimento Kotlin em ambientes Unix based

Para quem não tem a JVM instalada, particulamente, acho a o [SDKMan](https://sdkman.io/){:target="\_blank"} a melhor forma de configurar itens do ambiente Java para ambientes Unix based. Usuários de Windows, não sei se tem uma forma de configurar o SDKMan no Windows.

Segue passo a passo de como testar e configurar ambiente Kotlin em ambiente Unix based:

1- [Instalar o SDK Man](https://sdkman.io/install){:target="\_blank"}
<br/>2- Usando Sdk Man, [instalar o Kotlin](https://sdkman.io/sdks#kotlin)
<br/>3- Você pode ver que a variável de ambiente KOTLIN_HOME foi setada através do comando {% highlight powershell %}echo \$KOTLIN_HOME{% endhighlight %}

4- Testar a instalação do Kotlin através do comando kotlinc. Deve aparecer conforme abaixo.
![](/static/img/kotlin/kotlin-demo.png){:target="\_blank"}

## Hello World

A forma mais fácil de testar Kotlin sem necessidade de instalar nenhum software é através do site da própria linguagem [Try Kotlin](https://try.kotlinlang.org/#/Examples/Hello,%20world!/Simplest%20version/Simplest%20version.kt){:target="\_blank"} que est[a sendo considerado obsoleto e eles recomendam agora o [Kotlin Playground](https://play.kotlinlang.org){:target="\_blank"}.

Arquivos de código-fonte Kotlin eles tem a extensão .kt. O hello World Kotlin pode ser feito da seguinte forma (pode ser executado diretamente no terminal ou salvo como arquivo):
{% highlight kotlin %}
fun main(args: Array<String>){
println("Hello, World")
}
{% endhighlight %}

Assim como no Java existe a função public static void main, em Kotlin essa função é o main, descrito acima. É como a JVM interpreta que o Kotlin executará um programa.

Para compilar via linha de comando será necessário digitar o comando abaixo no diretório onde o arquivo foi salvo.
{% highlight powershell %}
kotlinc nome-arquivo-fonte.kt
{% endhighlight %}

Para converter esse código Kotlin em um jar executável da JVM é necessário rodar o comando abaixo:
{% highlight powershell %}
kotlinc nome-arquivo-fonte.kt -include-runtime -d nome-binario-executavel.jar
{% endhighlight %}

## IDEs

Dificilmente, alguém utilizará para projetos reais a estrutura acima, de executar manualmente, compilar, etc. Normalmente trabalhamos com IDEs em projetos reais. Não testei no Netbeans porque, particulamente não conheço e não uso, porém para as 3 IDEs que tenho na minha máquina (Eclipse,IntelliJ e VSCode) vi que o Kotlin tem plugin e suporte.

- IntelliJ: Instalar plugin Kotlin
- Eclipse: Instalar no Market Place o plugin para Kotlin
- VsCode: Instalar o plugin para Kotlin (baixei o que tinha mais download em minha busca, que foi do editor: mathiasfrohlich)

## Conclusão

Até o momento, estou utilizando IntelliJ como IDE para programar em Kotlin e tenho gostado do resultado. Achei conceitualmente muito parecido com Java, porém mais simples. A interoperabilidade com Java é muito bem feita para os testes incialmente feitos.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:
