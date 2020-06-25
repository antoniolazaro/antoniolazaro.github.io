---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Classes e objetos
date: 21/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Classes e objetos
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre classes e objetos

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Classes

As classes em Kotlin não são dinamicamente modificáveis. Para declarar uma classe se usa a palavra reservada _class_. Para criar uma classe basta invocar o construtor, sem necessidade de usar a palavra _new_, como no Java.

{% highlight kotlin %}
class Empty
val object = Empty()
{% endhighlight %}

Toda classe em Kotlin, é filha de Any e Any provê três métodos básicos:

- toString: Retorna uma string que representa o objeto. Imprime os valores de seus atributos
- equals: Verifica se um objeto é igual ao outro
- hashcode: Oferece um inteiro como código de hash.

#### Properties

Classes são compostas normalmente por propriedades (também conhecidas como atributos). É possível declarar propriedades conforme sintaxe abaixo:

{% highlight kotlin %}
class Person {
var name = "Anne"
var age = 32
}
val a = Person()
val b = Person()
println("${a.age} ${b.age}") // Prints "32 32"
a.age = 42
println("${a.age} ${b.age}") // Prints "42 32"
val object = Empty()
{% endhighlight %}

Em Kotlin não existe o conceito de atributo de classe (static class).

#### Constructores e blocos de inicialização

Propriedades que não possuem valor default serão inicializadas através dos construtores das classes. Em Kotlin existe o conceito de construtor primário e o construtor suporta recursos de função como default value param, tornando a criação de construtor mais flexível. Em Kotlin, é possível definir um bloco default para inicializar o objeto pós construtor. Seria equivalente ao _@PostConstruct_ que existe tanto para _CDI_ quanto para o _Spring_. Normalmente os atributos de nossas classes assumem valores _val_ para os atributos, mas pode ser declarado como var.

É possível também a definição de outros construtores, através do conceito de secondary constructors. Que é uma função precedida pela palavra _constructor_.

Exemplos:

{% highlight kotlin %}
class Person(firstName: String, lastName: String, yearOfBirth: Int) {
val fullName = "$firstName $lastName"
var age: Int

init {
age = 2018 - yearOfBirth
}
}

class Person(val name: String, var age: Int)//inline constructor

//secondary constructor
class Person(val name: String, var age: Int) {
constructor(name: String) : this(name, 0)
constructor(yearOfBirth: Int, name: String)
: this(name, 2018 - yearOfBirth)
}

//exemplo uso:
val a = Person("Jaime", 35)
val b = Person("Jack") // age = 0
val c = Person(1995, "Lynne") // age = 23
{% endhighlight %}

#### getters and setters

Kotlin fornece por padrão para cada propriedade dois métodos de acesso, um get e set. Se a variável é do tipo val, só é fornecido o get. É possível sobrescrever um ou ambos acessos. A sintaxe abaixo define como fazer isso.

{% highlight kotlin %}
class Person(age: Int) {
var age = 0
set(value) {
if (value < 0) throw IllegalArgumentException(
"Age cannot be negative")
field = value
}

    init {
        this.age = age
    }

}
{% endhighlight %}

#### Member functions

Uma classe pode ter métodos associados a ela. Se dentro da classe Pessoa defino a função present, é possível chamar conforme sintaxe abaixo:

{% highlight kotlin %}
val p = Person("Claire")
p.present() // Prints "Hello, I'm Claire!"

fun present() {
println("Hello, I'm \$name!")
}
{% endhighlight %}

#### lateinit

Kotlin tem um recurso que requerer que toda property deve ser inicializada durante a construção. Porém, em alguns momentos, a classes pretende ser usada em um contexto onde no momento da construção nem todas informações estão disponíveis para fazer a configuração e nao é possível definir um valor default. Para esses casos, é possível utilizar a palavra _lateinit_. Com isso, o compilador saberá que aquela propriedade será configurado após a construção do objeto. Podendo ser diretamente ou via alguma função. Caso a propriedade seja lida antes dela ser configurada, será lançada uma exceção de runtime _UninitializedPropertyAccessException_.

{% highlight kotlin %}
lateinit var name: String
{% endhighlight %}

#### Operators overloading

A maioria dos operadores de Kotlin, são reconhecidos por ter um nome textual e estão disponíveis para implementação em suas classes. Exemplo, o operador +, é chamado plus, então é possível sobrescrever o comportamento em uma determinada classe com a sintaxe abaixo, obtendo um resultado interessante.

{% highlight kotlin %}
operator fun plus(spouse: Person) {
println("$name and ${spouse.name} are getting married!")
}
lisa + anne // Prints "Lisa and Anne are getting married!"
{% endhighlight %}

#### Data Classes

Esse tipo de classes são usados como DTOs, Entity, Models. São dados que contém dados. Por default, eles fornecem implementação de toString, equals e hashcode, além do método copy que fornece uma cópia nova do objeto. Essas classes não podem ser Open, abstract, Sealed ou inner.

{% highlight kotlin %}
data class ContentDescriptor(val kind: ContentKind, val id: String) {
override fun toString(): String {
return kind.toString() + ":" + id
}
}
{% endhighlight %}

##### Copy

Essa função tem como objetivo fornecer uma cópia do objeto com alguns valores alterados, mas manteendo o restante igual.

{% highlight kotlin %}
val jack = User(name = "Jack", age = 1)
val olderJack = jack.copy(age = 2)
{% endhighlight %}

##### Desestruturação

Similar ao JavaScript, é possível quebrar propriedades do objeto em variáveis.

{% highlight kotlin %}
val jane = User("Jane", 35)
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"

//como compilador gera o código.
val name = person.component1()
val age = person.component2()
{% endhighlight %}

Retornando dois valores de uma função:

{% highlight kotlin %}
data class Result(val result: Int, val status: Status)
fun function(...): Result {
// computations

return Result(result, status)
}

// Now, to use this function:
val (result, status) = function(...)
{% endhighlight %}

## Conclusão

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/docs/tutorials/kotlin-for-py/classes.html
- https://kotlinlang.org/docs/reference/operator-overloading.html
- https://kotlinlang.org/docs/reference/data-classes.html
- https://kotlinlang.org/docs/reference/multi-declarations.html

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
