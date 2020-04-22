---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Object e Companion Object, interfaces e herança
date: 22/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Object e Companion Object, interfaces e herança
categories: [kotlin]
thumbnail: heart
---

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre Object e Companion Object, interfaces e herança.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Herança

Tinhamos falado no post [post]({% link _posts/2020-04-21-estudo-kotlin-parte5.md %}){:target="\_blank"} sobre classes, construtores, inicializadores e objetos. Nessa seção falaremos um pouco sobre herança em Kotlin. Toda classe herda de Any (em Java toda classe herda de Object). Se nenhuma relação de herança for feita explicitamente, o compilador automaticamente definirá que aquela classe herda de [Any](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/){:target="\_blank"}. Any fornece três métodos para todas classes, _equals_,_hashcode_ e _toString_. Por padrão, toda classe em Kotlin são final, e elas não podem ser herdadas. Uma classe para ser herdada, ela deve ser marcada com a palavra reservada _open_.

{% highlight kotlin %}
open class Base(p: Int)
class Derived(p: Int) : Base(p)
{% endhighlight %}

Se a classe pai possuir um primary constructor, a classe filha deve inicializar o mesmo na configuração da herança. Existem secondary constructors, então pode ser usado a palavra super, conforme exemplo abaixo:

{% highlight kotlin %}
class MyView : View {
constructor(ctx: Context) : super(ctx)

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)

}
{% endhighlight %}

#### Classe abstrata

Uma classe ou membros podem ser declarados como _abstract_. Métodos abstratos não tem uma implementação na classe que declara. Não é necessário registrar uma classe abstrata com open.

{% highlight kotlin %}
open class Polygon {
open fun draw() {}
}
abstract class Rectangle : Polygon() {
abstract override fun draw()
}
{% endhighlight %}

#### Sobreescrita de método

Em Kotlin, as coisas precisam ser explicitamente falada para varios recursos, a sobrescrita de métodos é uma dessas coisas. É necessário usar o modificador _override_ para definir uma sobrescrita. É necessário definir através do modificador _open_ quais métodos podem ou não ser sobrescritos, como no exemplo abaixo.

{% highlight kotlin %}
open class Shape {
open fun draw() { /_..._/ }
fun fill() { /_..._/ }
}

class Circle() : Shape() {
override fun draw() { /_..._/ }
}
{% endhighlight %}

Caso uma classe filha queira definir que suas subclasses não podem sobrescever sua implementação de um método deve ser usado a palavra _final_.

{% highlight kotlin %}
open class Rectangle() : Shape() {
final override fun draw() { /_..._/ }
}
{% endhighlight %}

Em Kotlin, existe a sobrecarga de propriedade, pode ser útil para definição de valores default de inicialização. Os tipos nesse caso devem ser compatíveis. É possível sobrescrever uma variável val com var, mas não é possível fazer o contrário.

{% highlight kotlin %}
open class Shape {
open val vertexCount: Int = 0
}

class Rectangle : Shape() {
override val vertexCount = 4
}
{% endhighlight %}

Para invocar a implementação da classe pai, existe a palavra _super_.

{% highlight kotlin %}
open class Rectangle {
open fun draw() { println("Drawing a rectangle") }
val borderColor: String get() = "black"
}

class FilledRectangle : Rectangle() {
override fun draw() {
super.draw()
println("Filling the rectangle")
}

    val fillColor: String get() = super.borderColor

}
{% endhighlight %}

Pensando em uma Inner class, é possível usar super@Outer.

{% highlight kotlin %}
class FilledRectangle: Rectangle() {
fun draw() { /_ ... _/ }
val borderColor: String get() = "black"

inner class Filler {
fun fill() { /_ ... _/ }
fun drawAndFill() {
super@FilledRectangle.draw() // Calls Rectangle's implementation of draw()
fill()
println("Drawn a filled rectangle with color \${super@FilledRectangle.borderColor}") // Uses Rectangle's implementation of borderColor's get()
}
}
}
{% endhighlight %}

Em Kotlin quando existe mais de uma implementação disponível para o mesmo método, o compilador obriga a classe filha fornecer uma implementação concreta para esse método. Isso pode ser resolvido usando qualquer uma das referências em questão.

{% highlight kotlin %}
open class Rectangle {
open fun draw() { /_ ... _/ }
}

interface Polygon {
fun draw() { /_ ... _/ } // interface members are 'open' by default
}

class Square() : Rectangle(), Polygon {
// The compiler requires draw() to be overridden:
override fun draw() {
super<Rectangle>.draw() // call to Rectangle.draw()
super<Polygon>.draw() // call to Polygon.draw()
}
}
{% endhighlight %}

### Object expressions

Em Kotlin é possível criar um objeto com sensíveis modificações da classe de origem sem necessariamente criar uma subclasse explicitamente. É possível fazer isso de duas formas, através das expressões.

{% highlight kotlin %}
window.addMouseListener(object : MouseAdapter() {
override fun mouseClicked(e: MouseEvent) { /_..._/ }

    override fun mouseEntered(e: MouseEvent) { /*...*/ }

})
}
{% endhighlight %}

Esse recurso é inicializado e executado imediatamente onde aparecer a referência no código.

### Object declarations

Esse tipo de recurso cria Singletons de maneira bem simples em Kotlin.

{% highlight kotlin %}
object DataProviderManager {
fun registerDataProvider(provider: DataProvider) {
// ...
}

    val allDataProviders: Collection<DataProvider>
        get() = // ...

}

DataProviderManager.registerDataProvider(...)

{% endhighlight %}

Esse recurso é inicializado de maneira lazy, apenas no primeiro acesso.

### Companion Object

Kotlin não possui o recursos _static_ do Java para atributos ou métodos de classes. O que existe é uma forma de você declarar um singleton da classe através do compation object e criar essa estrutura dentro da classe, como nos exemplos abaixo:

{% highlight kotlin %}
class MyClass {
companion object Factory {
fun create(): MyClass = MyClass()
}
}
val instance = MyClass.create()

class MyClass {
companion object { }
}

val x = MyClass.Companion

{% endhighlight %}

Para compatibilidade com Java, é necessário usar a anottation _@JvmStatic_.

Esse tipo de objeto é inicializado quando a classe que carrega ele é carregada/resolvida. Lembra muito o comportamento da incialização static do Java.

### Interfaces

Interfaces podem conter métodos abstratos bem como implementações. As interfaces diferem da classe abstrata por não guardar estado. Elas podem ter propriedades mas essas precisam ser abstratas ou fornecer implementações para os métodos de acesso.

Uma classe pode implementar diversas interfaces.

{% highlight kotlin %}
interface MyInterface {
fun bar()
fun foo() {
// optional body
}
}

class Child : MyInterface {
override fun bar() {
// body
}
}

//propriedades em interface
interface MyInterface {
val prop: Int // abstract

    val propertyWithImplementation: String
        get() = "foo"

    fun foo() {
        print(prop)
    }

}

class Child : MyInterface {
override val prop: Int = 29
}
{% endhighlight %}

Uma interface pode herdar de outras interfaces. Apenas as classes são obrigatórias a definir implementação para interfaces, mas elas podem prover implementações.

{% highlight kotlin %}
interface Named {
val name: String
}

interface Person : Named {
val firstName: String
val lastName: String

override val name: String get() = "$firstName $lastName"
}

data class Employee(
// implementing 'name' is not required
override val firstName: String,
override val lastName: String,
val position: Position
) : Person
{% endhighlight %}

Esse exemplo ilustra o aspecto da herança e como tratar conflito de sobrescrita de implementação de interfaces:

{% highlight kotlin %}
interface A {
fun foo() { print("A") }
fun bar()
}

interface B {
fun foo() { print("B") }
fun bar() { print("bar") }
}

class C : A {
override fun bar() { print("bar") }
}

class D : A, B {
override fun foo() {
super<A>.foo()
super<B>.foo()
}

    override fun bar() {
        super<B>.bar()
    }

}
{% endhighlight %}

## Conclusão

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

## Outras Fontes:

- https://kotlinlang.org/docs/reference/classes.html
- https://kotlinlang.org/docs/reference/object-declarations.html
- https://kotlinlang.org/docs/reference/properties.html
