---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Ranges
date: 01/05/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Ranges
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre Ranges.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Ranges

Kotlin tem um mecanismo que lida com intervalos chamado Range.
Um range define um intervalo fechado entre dois pontos e os pontos são incluídos nesse intervalo. Eles são definidos por tipos comparáveis que possuem critério de ordem. Qualquer classe que implemente a interface Comparable pode criar um Range. Um uso muito comum é para intervalos númericos, datas e textos. Alguns exemplos seguem abaixo:

{% highlight kotlin %}
val start = Date.valueOf("2017-01-01")
val end = Date.valueOf("2017-12-31")
val range = start..end
println(range) // 2017-01-01..2017-12-31

println("Date.valueOf("2017-05-27") in range is ${Date.valueOf("2017-05-27") in range}") // true
println("Date.valueOf("2018-01-01") in range is ${Date.valueOf("2018-01-01") in range}") // false
println("Date.valueOf("2018-01-01") !in range is \${Date.valueOf("2018-01-01") !in range}") // true

val range = 1.0..100.0
println(range) // 1.0..100.0

println("3.14 in range is ${3.14 in range}") // true
println("100.1 in range is ${100.1 in range}") // false

val range = 1f..100f
println(range) // 1.0..100.0

println("3.14f in range is ${3.14f in range}") // true
println("100.1f in range is ${100.1f in range}") // false
{% endhighlight %}

Para utilização de ranges é necessário seguir a seguinte sintaxe **inicioRange*..*fimRange**. Para testes condicionais é possível utilizar as funções _in_ e _!in_. Ranges númericos ((IntRange, LongRange, CharRange) tem um recurso adicional que eles podem ser iterados. Esses ranges também são progressões (uma sequência numérica que a diferença entre os números tem uma valor constante).

Para iterar na ordem reversa os números, existe a função **downTo** ao invés de _.._, como mostra o exemplo abaixo:

{% highlight kotlin %}
for (i in 1..4) print(i) //1,2,3,4
for (i in 4 downTo 1) print(i) //4,3,2,1
{% endhighlight %}

É possível definir também o salto (o padrão é um) para uma iteração de um range, usando a sintaxe **step**.

{% highlight kotlin %}
for (i in 1..8 step 2) print(i)
println()
for (i in 8 downTo 1 step 2) print(i)
{% endhighlight %}

Como podemos observar no exemplo acima, os intervalos de um range são inclusivos. Caso queira excluir o último elemento deve ser usado a função **until**, como no exemplo abaixo:

{% highlight kotlin %}
for (i in 1 until 10) { // i in [1, 10), 10 is excluded
print(i)
}
{% endhighlight %}

_Exemplo de range de characteres:_
{% highlight kotlin %}

    for (c in 'a'..'k')
        print("$c ")

    println()

    for (c in 'k' downTo 'a')
        print("$c ")

print(i)
}

{% endhighlight %}

### forEach e iterator

Para iterar um range também existe a possibilidade de utilizar um forEach ou usar um iterator, como no exemplo abaixo:
{% highlight kotlin %}
(1..5).forEach(::println)

    (1..5).reversed().forEach { e -> print("$e ") }

    val chars = ('a'..'f') //usando range como variável.

val it = chars.iterator()

    {% endhighlight %}

### Range suporta operações filter, reduce e map

{% highlight kotlin %}
val rnums = (1..15)

    println(rnums)

    val r = rnums.filter { e -> e % 2 == 0 }
    println(r)

    val r2 = rnums.reduce { total, next -> next * 2 - 1 }
    println(r2)

    var r3 = rnums.map { e -> e * 5 }
    println(r3)

{% endhighlight %}

### Range possui operações pre-definidas de min, max, sum,count, average, distinct

{% highlight kotlin %}
val r = (1..10)

    println(r.min())
    println(r.max())
    println(r.sum())
    println(r.average())
    println(r.count())

    val repeated = listOf(1, 1, 2, 4, 4, 6, 10)

print(repeated.distinct()) // Print [1, 2, 4, 6, 10]

    {% endhighlight %}

### Função reversed para iteração em ordem reversa

{% highlight kotlin %}
(1..9).reversed().forEach {
print(it) // Print 987654321
}

(1..9).reversed().step(3).forEach {
print(it) // Print 963
}
{% endhighlight %}

### Encontrar primeiro, último e step.

{% highlight kotlin %}
print((1..9).first) // Print 1
print((1..9 step 2).step) // Print 2
print((3..9).reversed().last) // Print 3
{% endhighlight %}

### Qualquer objeto pode ser colocado como Range, desde que implemente a interface Comparable

{% highlight kotlin %}
enum class Color(val rgb: Int) : Comparable<Color> {
BLUE(0x0000FF),
GREEN(0x008000),
RED(0xFF0000),
MAGENTA(0xFF00FF),
YELLOW(0xFFFF00);
}

val range = red..yellow
if (range.contains(Color.MAGENTA)) println("true") // Print true
if (Color.RED in Color.GREEN..Color.YELLOW) println("true") // Print true
if (Color.RED !in Color.MAGENTA..Color.YELLOW) println("true") // Print true

fun main(args: Array<String>) {
for (c in Color.BLUE.rangeTo(Color.YELLOW)) println(c) // for-loop range must have an iterator() method
}
{% endhighlight %}

## Conclusão

Nos dois links abaixo é possível brincar um pouco online com ranges em Kotlin. A documentação da linguagem também é auto-explicativa e provê muitos recursos.

- [Link1](https://try.kotlinlang.org/#/Examples/Basic%20syntax%20walk-through/Use%20ranges%20and%20in/Use%20ranges%20and%20in.kt){:target="\_blank"}
- [Link2](https://try.kotlinlang.org/#/Kotlin%20Koans/Conventions/In%20range/Task.kt){:target="\_blank"}

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/docs/reference/ranges.html
- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/range-to.html
- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/-int-range/
- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/-long-range/
- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/-char-range/
- http://zetcode.com/kotlin/ranges/
- https://www.baeldung.com/kotlin-ranges
- https://www.geeksforgeeks.org/kotlin-ranges/
- https://beginnersbook.com/2019/02/kotlin-ranges/

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
