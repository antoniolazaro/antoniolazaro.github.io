---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Exception
date: 22/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Exception
categories: [kotlin]
thumbnail: heart
---

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre Exception.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab).

### Exceptions

Exceptions em Kotlin todas descedem de _Throwable_. Todas possuem uma mensagem, stack trace e uma causa que é um parâmetro Exceptional.

Sintaxe da linguagem para exceções:

{% highlight kotlin %}
try {
// some code
}
catch (e: SomeException) {
// handler
}
finally {
// optional finally block
}

{% endhighlight %}

Em Kotlin, existe o try é uma expressão, e consegue ser usada como abaixo:

{% highlight kotlin %}
val a: Int? = try { parseInt(input) } catch (e: NumberFormatException) { null }
{% endhighlight %}

Kotlin não possui exceções checadas. Segundo Brucel Eckel, ele disse:

_Examination of small programs leads to the conclusion that requiring exception specifications could both enhance developer productivity and enhance code quality, but experience with large software projects suggests a different result – decreased productivity and little or no increase in code quality._

Outros textos sobre exceções checadas no Java:

- Java's checked exceptions were a mistake (Rod Waldhoff)
- The Trouble with Checked Exceptions (Anders Hejlsberg)

Em Kotlin existe o tipo _Nothing_ que é uma expressão retornada quando throw é lançado. Não possui instância. Quando o compilador vê esse objeto, ele nunca retorna normalmente e irá seguir o fluxo da operação, assumindo que houve uma exceção. É como se fosse um "abafar" exception provido pela linguagem.

Exemplo de uso:

{% highlight kotlin %}
val s = person.name ?: fail("Name required")
println(s) // 's' is known to be initialized at this point
{% endhighlight %}

## Conclusão

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/docs/tutorials/kotlin-for-py/exceptions.html
- https://kotlinlang.org/docs/reference/exceptions.html
- https://taverna.devall.com.br/t/o-s-erro-s-de-1-bilhao-de-dolares-bem-mais/276
- https://medium.com/@gustavoramos00/option-x-null-o-erro-de-1-bilh%C3%A3o-de-d%C3%B3lares-7c746480519c
- https://medium.com/@joelamalio/kotlin-exce%C3%A7%C3%B5es-865767f7e46

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
