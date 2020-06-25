---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Função repeat
date: 05/05/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Função repeat
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre a estrutura de repetição _repeat_ que em Kotlin é uma _função inline_. Falamos de maneira macro no [capítulo 3 da série]({% link _posts/2020-04-21-estudo-kotlin-parte3.md %}){:target="\_blank"}. Nesse post, pretendo ser mais específico sobre essa estrutura de repetição presente em outras linguagens como Python e ausente no Java. O recurso é bastante simples.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Repeat

O comportamento pode ser obtido através da chamada da função inline repeat. A sintaxe da declaração da função segue abaixo, bem como exemplo de uso.

Por se tratar de uma função, não é possível utilizar lógica dentro do repeat com a expectativa de uso de _continue_ e _break_, como é feito em laços, como _while_, _do/while_ e _for_.

![](/static/img/kotlin/repeat-error.png)

Exemplo de uso da função.

{% highlight kotlin %}

//declaração da função na documentação da linguagem
inline fun repeat(times: Int, action: (Int) -> Unit)

// greets three times
repeat(3) {
println("Hello")
}

repeat(0) {
error("We should not get here!")
}

{% endhighlight %}

## Conclusão

Com suporte de função é possível vermos como a linguagem Kotlin é extensível e podemos desenvolver novos comandos a partir de funções. Isso é muito útil.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/repeat.html
- https://riptutorial.com/kotlin/example/9112/repeat-an-action-x-times
- https://www.jworks.io/loops-in-kotlin/

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
