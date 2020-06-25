---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - Outras características (Null Safety) + Java e Kotlin no mesmo projeto
date: 22/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - Outras características (Null Safety) + Java e Kotlin no mesmo projeto
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre Outras características (Null Safety) + Java e Kotlin no mesmo projeto.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Modificadores de visibilidade

Em Kotlin, classes, objetos, interfaces, construtores, funções e propriedades podem ser diferentes visibilidades. Elas existem em 4 níveis (ordenados aqui pelo nível de visibilidade): _private_ < _protected_ < _internal_ < _public_. Se nenhum modificador é usado, por padrão é definido como _public_.

#### Funções, propriedades, classes podem ser declaradas em alto nível, diretamente em um pacote, como no exemplo abaixo:

{% highlight kotlin %}
// file name: example.kt
package foo

fun baz() { ... }
class Bar { ... }
{% endhighlight %}

Para esse contexto, os modificadores atendem o comportamento abaixo:

Protected = Não está disponível para declarações de alto-nível
Private = Apenas no arquivo em questão.
Internal = Dentro do mesmo módulo (conjunto de arquivos Kotlin compilados juntos. Dependência)
Public = Menos restritivo modificador possível

#### Para classes e interfaces a estrutura segue a seguinte hierarquia:

Protected = Private+ visíveis em subclasses também
Private = Apenas na classe em questão
Internal = Dentro do mesmo módulo (conjunto de arquivos Kotlin compilados juntos. Dependência)
Public = Menos restritivo modificador possível

Variáveis locais não tem recurso de modificadores de acesso e para construtores o único aplicado é o private.

### Type aliases

É possível oferecer nomes alternativos para tipos existentes. Se o nome é muito longo e você quer colocar um nome mais curto ou mais lógico. Exemplos de uso:

{% highlight kotlin %}
typealias NodeSet = Set<Network.Node>

typealias FileTable<K> = MutableMap<K, MutableList<File>>

typealias MyHandler = (Int, String, Any) -> Unit

typealias Predicate<T> = (T) -> Boolean

class A {
inner class Inner
}
class B {
inner class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner

{% endhighlight %}

### Null Safety

Uma variável que não aponta para nenhum referência, aponta para null. Null não é um objeto. É como no Java, uma palavra reservada para fazer uma variável referenciar nenhum endereço de memória específico. Porém, em Java, existe uma exceção clássica chamada _NullPointerException_ (NPE). Essa exceção é conhecida como o erro de um bilhão de dólares [(referência)](https://www.eximiaco.ms/pt/2019/11/30/como-c-esta-tentando-superar-um-erro-de-muito-mais-que-um-bilhao-de-dolares/){:target="\_blank"}. Esse erro é muito comum e normalmente causado por ausência de tratativa de possibilidades de atribuição de uma variável gerando impacto na execução do programa. Kotlin, encoraja você a não usar null, tanto quanto for possível. Uma variável por padrão não pode receber null, a não ser que ela explicitamente informe isso, através do sufico _?_.

{% highlight kotlin %}
fun test(a: String, b: String?) {
}
test("a", "b") // execução ok
test("a", null) // execução ok
test(null, "b") //erro de compilação
test(null, null) //erro de compilação
{% endhighlight %}

Em Kotlin, é possível fazer chamadas seguras, através da sintaxe _x?.y_ ou x?.y(). O que faz o compilador somente avançar na invocação, se e somente se, a variável _x_ for != null.

Existe um outro recurso chamado, Elvis Operator, que tem a sintaxe _x ?: y_, onde, caso x, seja null, o valor de Y, é atribuído, que também é uma forma de tratar expressões com _null_ em Kotlin.

Existe uma outra sintaxe, que caso, você coloque em uso, será levantada uma exceção _NPE_.

{% highlight kotlin %}
val x: String? = javaFunctionThatYouKnowReturnsNonNull()
val y: String = x!!//se X vier null, será levantada uma exceção.
{% endhighlight %}

O contexto acima citado, pode ser tratado de maneira elegante, especificando uma exceção do projeto, conforme sintaxe abaixo:
{% highlight kotlin %}
val y: String = x ?: throw SpecificException("Useful message")
y.importantFunction()
{% endhighlight %}

Em resumo, as únicas formas em Kotlin de existir um NPE são as seguintes:

- Uma chamada explicita a NPE
- Uso do operador _!!_
- Inconsistência de dados na inicialização.
- Interoperabilidade com o Java.

### Cast e Type Casts

Em Kotlin, para verificar o tipo de um objeto existem os operadores _is_ e _!is_. Eles seriam equivalente ao uso do operador instanceOf do Java.

Kotlin tem o recurso de Smart Cast para valores imutáveis.

O uso de smart casts não funciona quando o compilador não pode garantir que a variável não pode mudar entre a checagem e o uso.

Exemplo:
{% highlight kotlin %}

fun demo(x: Any) {
if (x is String) {
print(x.length) // x is automatically cast to String
}
}
if (x !is String) return

print(x.length) // x is automatically cast to String
// x is automatically cast to string on the right-hand side of `||`
if (x !is String || x.length == 0) return

// x is automatically cast to string on the right-hand side of `&&`
if (x is String && x.length > 0) {
print(x.length) // x is automatically cast to String
}
when (x) {
is Int -> print(x + 1)
is String -> print(x.length + 1)
is IntArray -> print(x.sum())
}
{% endhighlight %}

### Interoperabilidade entre Java e Kotlin no mesmo projeto

É possível em um projeto Kotlin ter código Java e vice-versa. A IDE IntelliJ tem uma ferramenta que converte código Java em Kotlin.

{% highlight kotlin %}
public class Customer {

    private String name;

    public Customer(String s){
        name = s;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void placeOrder() {
        System.out.println("A new order is placed by " + name);
    }

}
val customer = Customer("Phase")
println(customer.name)
println(customer.placeOrder())

{% endhighlight %}

No [link](https://kotlinlang.org/docs/tutorials/mixing-java-kotlin-intellij.html){:target="\_blank"} tem uns demos da IDE funcionando.

## Conclusão

Nesse estudo, apresentei alguns recursos do Kotlin que são bastante inovadores para mim que vim da linguagem Java. Espero continuar aprendendo.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/docs/reference/properties.html
- https://kotlinlang.org/docs/reference/visibility-modifiers.html
- https://kotlinlang.org/docs/reference/type-aliases.html
- https://kotlinlang.org/docs/tutorials/kotlin-for-py/null-safety.html
- https://kotlinlang.org/docs/reference/null-safety.html#nullable-types-and-non-null-types
- https://kotlinlang.org/docs/tutorials/mixing-java-kotlin-intellij.html
- https://kotlinlang.org/docs/reference/java-interop.html
- https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
