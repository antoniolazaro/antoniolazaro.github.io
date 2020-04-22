---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Outros tipos de classes
date: 21/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Outros tipos de classes
categories: [kotlin]
thumbnail: heart
---

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre outros tipos de classes.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Enum Classes

Enums seguem mesma estrutura conhecida do mundo Java. Cada constante de uma enum é um objeto. O Enum pode ser inicializado no construtor como no exemplo abaixo.

{% highlight kotlin %}
enum class Color(val rgb: Int) {
RED(0xFF0000),
GREEN(0x00FF00),
BLUE(0x0000FF)
}
{% endhighlight %}

Um recurso interessante do Kotlin é que uma Enum pode implementar uma interface (porém não pode herdar de uma classe). Para isso, é necessário ela fornecer uma implementação do método da interface para cada entrada da enum.

{% highlight kotlin %}
enum class IntArithmetics : BinaryOperator<Int>, IntBinaryOperator {
PLUS {
override fun apply(t: Int, u: Int): Int = t + u
},
TIMES {
override fun apply(t: Int, u: Int): Int = t \* u
};

    override fun applyAsInt(t: Int, u: Int) = apply(t, u)

}
{% endhighlight %}

Por default, enum em Kotlin oferece possibilidade de obter pelo nome e a lista de enum através de métodos da própria API nativa da linguagem. Caso uma busca por nome, seja de alguma constante não defiinda na Enum, um erro _IllegalArgumentException_ é levantado.

{% highlight kotlin %}
EnumClass.valueOf(value: String): EnumClass
EnumClass.values(): Array<EnumClass>
{% endhighlight %}

As enums em Kotlin oferece acesso a duas propriedades, o nome e a posição dela dentro da declaração da Enum.

{% highlight kotlin %}
val name: String
val ordinal: Int
{% endhighlight %}

Enums, implementam Comparable e a ordem natural padrão é a ordem na qual ela foi declarada na classe que criou a enum.

### Sealed CLasses

Esse tipo de classes são utilizadas para representar restrições para hierarquia de heranças. Quando um valor pode ter um dos tipos limitados de um subtipo, mas não pode ter qualquer tipo dentro da herança. É como se fosse um Enum para classes, uma vez que o domínio é restrito. A diferença básica é que Enum são singletons (só possui uma instância).

Uma classe selada pode ter subclasses mas todas elas precisam ser declaradas no mesmo arquivo da classe em questão. Exemplo:

{% highlight kotlin %}
sealed class Expr
data class Const(val number: Double) : Expr()
data class Sum(val e1: Expr, val e2: Expr) : Expr()
object NotANumber : Expr()
{% endhighlight %}

Esse tipo de classe é abstrato e não pode ser instanciado diretamente. Pode ter membros abstractos. Por serem abstratos não podem ter construtores não privados. Construtores são privados por padrão.

Esse [texto](https://medium.com/@joelamalio){:target="\_blank"} de [Joel Amálio](https://twitter.com/joelamalio){:target="\_blank"}, descreve com outros exemplos, o uso de Sealed classes em Kotlin.

### Nested Classes

Classes que são aninhadas em outras classes.

{% highlight kotlin %}
class Outer {
private val bar: Int = 1
class Nested {
fun foo() = 2
}
}
val demo = Outer.Nested().foo() // == 2
{% endhighlight %}

#### Inner classes

São nested classes que podem acessar membros da classe externa. Kotlin define uma referência para um objeto da classe externa.

{% highlight kotlin %}
class Outer {
private val bar: Int = 1
inner class Inner {
fun foo() = bar
}
}

val demo = Outer().Inner().foo() // == 1
{% endhighlight %}

#### Anonymous Inner classes

Inner classes criadas usango uma expressão de objeto.

{% highlight kotlin %}
window.addMouseListener(object : MouseAdapter() {

    override fun mouseClicked(e: MouseEvent) { ... }

    override fun mouseEntered(e: MouseEvent) { ... }

})
{% endhighlight %}

Na JVM se um objeto é instancia de uma interface funcional do Java (interface com apenas um método abstrato), é possível criar usando uma expressão lambada um objeto pelo tipo da interface.

{% highlight kotlin %}
val listener = ActionListener { println("clicked") }
{% endhighlight %}

### Inline Classes

Recurso disponível na linguagem, a partir da versão 1.3 e atualmente para fazer uso, é necessário habilitar uma parametrização conforme esse [link](https://kotlinlang.org/docs/reference/inline-classes.html){:target="\_blank"}. Confesso que não vi muita aplicabilidade para esse recurso, porém como é algo que existe, trouxe para mencionar. Mais detalhe pode ser entendido na [documentação](https://kotlinlang.org/docs/reference/inline-classes.html){:target="\_blank"}.

## Conclusão

Até o momento, me parece que Kotlin resolve muitos problemas de design do Java e vem como uma opção muito moderna para quem trabalha usando a JVM. Até o momento, o aprendizado tem sido bastante produtivo.

## Outras Fontes:

- https://kotlinlang.org/docs/tutorials/kotlin-for-py/classes.html
- https://kotlinlang.org/docs/reference/enum-classes.html
- https://kotlinlang.org/docs/reference/sealed-classes.html
- https://kotlinlang.org/docs/reference/nested-classes.html
- https://kotlinlang.org/docs/reference/inline-classes.html
- https://kotlinlang.org/docs/reference/inline-classes.html#experimental-status-of-inline-classes
