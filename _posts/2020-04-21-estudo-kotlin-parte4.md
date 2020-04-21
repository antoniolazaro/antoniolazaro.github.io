---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - parte 2 (Funções)
date: 21/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - parte 2 (Funções)
categories: [kotlin]
thumbnail: heart
---

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre funções

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab).

### Funções

A palavra reservada _fun_ define uma função em Kotlin. Os parametros são declarados com seus tipos e nomes e pode ser informado (ou não) um tipo de retorno da função. O corpo da função é envolvido por um bloco separado por chaves _{}_.

{% highlight kotlin %}
fun happyBirthday(name: String, age: Int): String {
return "Happy ${age}th birthday, $name!"
}
{% endhighlight %}

A invocação da função acontece pelo nome dela com passagem de parâmetro. Se não existe um valor de retorno, essa função não será atribuída a nenhuma variável.

{% highlight kotlin %}
val greeting = happyBirthday("Anne", 32)
{% endhighlight %}

Kotlin tem suporte a overload (sobrecarga) de funções. Uma função é diferenciada da outra devido a sua lista de parâmetros. Os parâmetros+retorno compõem a assinatura do método, entretanto o tipo de retorno não pode ser diferente entre funções sobrecarregadas.

Exemplo:
{% highlight kotlin %}
fun square(number: Int) = number _ number
fun square(number: Double) = number _ number
{% endhighlight %}

#### Suporte a varargs e optional/named parameters

Em Kotlin é possível usar a palavra varargs para passar um número X de valores para um parâmetro.
Também é possível definir um valor default para um parâmetro, tornando a chamada do método opcional para aquele parâmetro. O recurso de default para parâmetro, reduz necessidade de sobrecarga comparado com Java.

Exemplo:

Varargs:
{% highlight kotlin %}
fun countAndPrintArgs(vararg numbers: Int) {
println(numbers.size)
for (number in numbers) println(number)
}
{% endhighlight %}

Optional parameters:
{% highlight kotlin %}
fun foo(decimal: Double, integer: Int, text: String = "Hello") { ... }

foo(3.14, text = "Bye", integer = 42)
foo(integer = 12, decimal = 3.4)
{% endhighlight %}

Named parameters:
{% highlight kotlin %}
un foo(bar: Int = 0, baz: Int) { /_..._/ }

foo(baz = 1) // The default value bar = 0 is used

//outro exemplo

fun reformat(str: String,
normalizeCase: Boolean = true,
upperCaseFirstLetter: Boolean = true,
divideByCamelHumps: Boolean = false,
wordSeparator: Char = ' ') {
/_..._/
}

reformat(str) //call 1
reformat(str, true, true, false, '_') //call 2
reformat(str,
normalizeCase = true,
upperCaseFirstLetter = true,
divideByCamelHumps = false,
wordSeparator = '_'
)//call 3
reformat(str, wordSeparator = '\_') //call 4

{% endhighlight %}

#### Unit Value

Se uma função não tem nenhum valor de retorno, Kotlin assume que retorno é Unit. Esse valor não precisa ser reclarado explicitamente.

{% highlight kotlin %}
fun printHello(name: String?): Unit {
if (name != null)
println("Hello \${name}")
else
println("Hi there!")
// `return Unit` or `return` is optional
}

fun printHello(name: String?) { ... }

{% endhighlight %}

#### Single expression functions

Quando uma função retorna uma expressão, o corpo pode ser especificado após o símbolo _=_.

{% highlight kotlin %}
fun double(x: Int): Int = x _ 2
fun double(x: Int) = x _ 2 // omitindo tipo de retorno para compilador gerar por inferência
{% endhighlight %}

### Extension functions/properties

Kotlin oferece o mecanismo para que uma classe seja extendida com uma nova feature sem necessidade de trabalhar com herança ou outro tipo de técnica, como uso de Decorator, por exemplo. Existe uma declaração específica chamada extensão. Exemplo de uso: É necessário escrever um recurso para uma classe de uma biblioteca de terceiros que não é extensível.

Exemplo de aplicação:
{% highlight kotlin %}
fun MutableList<Int>.swap(index1: Int, index2: Int) {
val tmp = this[index1] // 'this' corresponds to the list
this[index1] = this[index2]
this[index2] = tmp
}
//exemplo de uso
val list = mutableListOf(1, 2, 3)
list.swap(0, 2) // 'this' inside 'swap()' will hold the value of 'list'
{% endhighlight %}

A referência this, dentro da implementação da função, corresponde a classe em questão. O recurso não modifica as classes, por definição ele não adiciona novos membros na classes mas basicamente faz as funções serem chamados dentro de um escopo de classe.

## Conclusão

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo. Próximo passo, é fazer algum projeto demo usando a linguagem.

## Outras Fontes:

- https://kotlinlang.org/docs/tutorials/kotlin-for-py/functions.html
- https://kotlinlang.org/docs/reference/extensions.html
- https://kotlinlang.org/docs/reference/functions.html
