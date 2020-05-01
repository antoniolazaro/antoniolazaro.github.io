---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Palavras chaves, identificadores, gramática e código-fonte da linguagem
date: 01/05/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Palavras chaves, identificadores, gramática e código-fonte da linguagem
categories: [kotlin]
thumbnail: heart
---

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre as palavras chaves, gramática e código-fonte da linguagem.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Palavras-chave

Toda linguagem de programação de um mapa de palavras reservadas. Essas palavras não podem ser usadas como nome de variáveis porque o compilador/interpretador da linguagem reserva para instruções específicas. Em Kotlin temos uma lista de 28 palavras reservadas. A título de comparação, [Java tem 50 palavras reservadas](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html){:target="\_blank"}.

Abaixo a tabela de palavras-chaves do Kotlin:
![](/static/img/kotlin/keywords.png)

Essas são as hard keywords de Kotlin. Existem palavras que são reservadas a depender do contexto. Exemplo **public**, é reservada quando usada para declaração de um membro de uma classe. Mas é possível criar uma variável chamada **public**.

{% highlight kotlin %}
class TestClass {
public val name = "Kotlin"
}
val public = true
{% endhighlight %}

Kotlin também possui o conceito de modifier keywords que tem o mesmo comportamento das Soft Keywords.

A lista completa dessas palavras pode ser vista no [site da linguagem](https://kotlinlang.org/docs/reference/keyword-reference.html){:target="\_blank"}.

#### Gramática

Ainda sobre essa parte de palavra-chave, é possível ler a gramática de Kotlin no [link da documentação da linguagem](https://kotlinlang.org/docs/reference/grammar.html){:target="\_blank"}.

#### Code-style Kotlin

Alguns links com code-style de Kotlin que são bastante parecidos com o de Java.

- [Oficial da linguagem](https://kotlinlang.org/docs/reference/coding-conventions.html){:target="\_blank"}
- [Documentação JetBrains](https://www.jetbrains.com/help/idea/code-style-kotlin.html#){:target="\_blank"}
- [Repositório do github bacana](https://github.com/raywenderlich/kotlin-style-guide){:target="\_blank"}
- [Link1 da documentação da linguagem](https://kotlinlang.org/docs/reference/code-style-migration-guide.html){:target="\_blank"}

### Identificadores

Algumas regras para identificadores em Kotlin:

1. Não podem ser ter espaço em branco
1. São casesensitive
1. Não podem ter caracteres especiais como: @, #,\$, %, etc.
1. Como toda linguagem de programação, deve se buscar dar nomes significativos.
1. CammelCase para definir classes e arquivos, e primeira letra minuscula para funções e variáveis.

### Código-fonte

Por ser opensource, Kotlin tem seu código-fonte no github. É possível acessar através do [link](https://github.com/JetBrains/kotlin){:target="\_blank"}.

## Conclusão

Nos dois links abaixo é possível brincar um pouco online com ranges em Kotlin. A documentação da linguagem também é auto-explicativa e provê muitos recursos.

- [Link1](https://try.kotlinlang.org/#/Examples/Basic%20syntax%20walk-through/Use%20ranges%20and%20in/Use%20ranges%20and%20in.kt){:target="\_blank"}
- [Link2](https://try.kotlinlang.org/#/Kotlin%20Koans/Conventions/In%20range/Task.kt){:target="\_blank"}

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

https://kotlinlang.org/docs/reference/keyword-reference.html
https://www.programiz.com/kotlin-programming/keywords-identifiers
https://beginnersbook.com/2017/12/kotlin-keywords-identifiers/
https://medium.com/jay-tillu/keywords-in-kotlin-a429247a1802

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
