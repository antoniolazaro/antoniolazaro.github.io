---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem - When, uma versão melhorada do switch do Java
date: 05/05/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem - When, uma versão melhorada do switch do Java
categories: [kotlin]
thumbnail: heart
---

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Existe uma boa prática de programação que recomenda que se faça aninhamento excessivo de condições if-else, para evitar códigos conforme da figura abaixo.
<br/>
![](/static/img/kotlin/if-else-avoid.jpg)
<br/>

Algumas soluções e padrões de projeto podem ser aplicados, desde uso de estrutura de dados (Maps/Dicionários), a padrão de projetos (strategy. explicado no excelente [post](https://ivanqueiroz.dev/2017/01/revisando-padroes-java-8-o-padrao-strategy.html){:target="\_blank"} de [@ivanqueiroz](https://twitter.com/ivanqueiroz){:target="\_blank"}).

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Um pouco de teoria

O if/else demasiadamente, não deve ser evitado apenas por questões de legibilidade mas também porque impacta na performance e na complexidade do algorítimo. A complexidade sintomática é uma métrica de software utilizada para definir a complexidade de um programa. Ela é medida como a medida quantitativa do número linar de caminhos que um programa pode percorrer através de seu código-fonte. Explicações mais detalhadas sobre o tema pode ser obtidas nos links [1](https://en.wikipedia.org/wiki/Cyclomatic_complexity){:target="\_blank"},[2](https://pt.stackoverflow.com/questions/193665/o-que-%C3%A9-complexidade-ciclom%C3%A1tica){:target="\_blank"} e [3](https://artesoftware.com.br/2019/02/09/complexidade-ciclomatica/){:target="\_blank"}. Existe toda uma teoria matemática que fundamenta essa explicação e de maneira "grosseira" porém, objetiva temos um resumo da seguinte forma:

- Se temos entre 0 e 5 condições - Provávelmente o programa é ok
- Se temos entre 6 e 10 - Devemos pensar em simplificar essa rotina
- Se temos mais de 10 - devemos quebrar essa rotina em subrotinas

Falando exclusivamente pelo viés da performance, a tendência é que o algorítimo do primeiro anexo de código, seja mais performático do que o segundo.

{% highlight java %}
if("visa".equals(transaction.getNetwork())){
//do visa stuff
} else if ("diners".equals(transaction.getNetwork())) {
//do diners stuff
} else if ("mastercard".equals(transaction.getNetwork())) {
//do mastercard stuff
} else if ("amex".equals(transaction.getNetwork())) {
//do amex stuff
}
//common stuff in there
return transaction;

{% endhighlight %}

_Implementação 2:_

{% highlight kotlin %}
if("visa".equals(transaction.getNetwork())){
//do visa stuff
return doCommonStuff(transaction);
}

if ("diners".equals(transaction.getNetwork())) {
//do diners stuff
return doCommonStuff(transaction);
}

if ("mastercard".equals(transaction.getNetwork())) {
//do mastercard stuff
return doCommonStuff(transaction);
}

if ("amex".equals(transaction.getNetwork())) {
//do amex stuff
return doCommonStuff(transaction);
}
{% endhighlight %}

### Quando temos um contexto onde é necessário se testar essas condições, o que podemos usar?

Em computação poucas perguntas não podem ser respondidas com a simples palavra _depende_. Existem contextos e estruturas onde é necessário trabalhar com diversas condicionais, então o que as linguagens oferecem como recurso mais elegante que o if/else. A grande vantagem de utilizar recursos nativos da linguagem, é que a mesma oferece uma implementação para reduzir a complexidade sintomática. Instruções como Switch (Java) e When (Kotlin), reduzem significativamente o impacto do grafo de decisão do algoritimo pois a condição da expressão é avaliada apenas uma vez. O compilador normalmente trata e garante uma otimização no uso desse tipo de instrução.

#### Java

Em Java, temos a instrução switch/case, que desde a release 8 vem sofrendo diversas melhorias mas apresenta algumas limitações, como por exemplo, no passado não suportava Strings dentro das condições.

Sintaxe da instrução switch/case em Java.

{% highlight Java %}
switch(expression) {
case x:
// code block
break;
case y:
// code block
break;
default:
// code block
}
{% endhighlight %}

Como isso funciona:

1. A instrução boolean dentro do switch é avaliada uma única vez.
2. O resultado dessa expressão é avaliado com cada _case_.
3. Se algum acontece o _match_, o bloco dentro do case é executado.
4. É opcional utilização de _break_ e _default_.

Evolução Switch/case no Java vem acontecendo e ele atualmente suporta comparação com Strings (desde o Java 7) e outros recursos que vou tentar enumerar logo abaixo:

1. [Switch Expressions - Preview Java 12](http://openjdk.java.net/jeps/325){:target="\_blank"}
1. [Switch Expressions - Preview Java 13](http://openjdk.java.net/jeps/354){:target="\_blank"}
1. [Switch Expressions - Standard Java 14](http://openjdk.java.net/jeps/361){:target="\_blank"}

O que é possível com esses recursos:

{% highlight java %}
boolean result = switch (ternaryBool) {
case TRUE -> true;
case FALSE -> false;
case FILE_NOT_FOUND -> throw new UncheckedIOException(
"This is ridiculous!",
new FileNotFoundException());
// as we'll see in "Exhaustiveness", `default` is not necessary
default -> throw new IllegalArgumentException("Seriously?! 🤬");

//exemplo 2
enum Person {
Mozart, Picasso, Goethe, Dostoevsky, Prokofiev, Dali
}

static void print(Person person) {
String title = switch (person) {
case Dali, Picasso -> "painter";
case Mozart, Prokofiev -> "composer";
case Goethe, Dostoevsky -> "writer";
};
System.out.printf("%s was a %s%n", person, title);
}

    //exemplo 3:
    static int factorial(int n) {
    return switch (n) {
        case 0, 1 -> 1;
        case 2    -> 2;
        default   -> factorial(n - 1) * n;
    };

}

{% endhighlight %}

#### Kotlin

Mas e como o Kotlin fornece trata esse problema? Eu particulamente achei muito simples e eficiente a forma como Kotlin traz isso. Como é uma linguagem mais nova e não precisa pensar em retrocompatibilidade, já nasceu da maneira otimizada e baseada em linguagens menos verbosas que o Java.

##### When

A instrução foi pensada para compensar diversos recursos não suportados nativamente pelo _switch/case_ do Java.

A primeira grande vantagem é que o _when_ já nasceu como uma expressão (suporta um valor a ser calculado em tempo de execução). A instrução é executada quando uma das condições é satisfeita. _When_ pode ser usada tanto como expressão, como comando. _When_ suporta um bloco _else_ que tem comportamento similar a um _else_ de uma instrução _if_.

_When_ suporta <a href="/kotlin/2020/05/01/estudo-kotlin-parte10.html" target="_blank">ranges</a>
e expressões como condicionais, também é possível utilizar a função _is_.

Exemplos de uso diversos:

{% highlight kotlin %}
when (x) {
1 -> print("x == 1")
2 -> print("x == 2")
else -> { // Note the block
print("x is neither 1 nor 2")
}
}

when (x) {
0, 1 -> print("x == 0 or x == 1")
else -> print("otherwise")
}

when (x) {
parseInt(s) -> print("s encodes x")
else -> print("s does not encode x")
}

when (x) {
in 1..10 -> print("x is in the range")
in validNumbers -> print("x is valid")
!in 10..20 -> print("x is outside the range")
else -> print("none of the above")
}

fun hasPrefix(x: Any) = when(x) {
is String -> x.startsWith("prefix")
else -> false
}

when {
x.isOdd() -> print("x is odd")
x.isEven() -> print("x is even")
else -> print("x is funny")
}

// a partir do Kotlin 1.3 é possível capturar um variável, visível ao escopo do when apenas.
fun Request.getBody() =
when (val response = executeRequest()) {
is Success -> response.body
is HttpError -> throw HttpException(response.status)
}

//when como expressão
val objectType = when (directoryType) {
UnixFileType.D -> "d"
UnixFileType.HYPHEN_MINUS -> "-"
UnixFileType.L -> "l"
}
val result = when (fileType) {
UnixFileType.L -> "linking to another file"
else -> "not a link"
}
val result: Boolean = when (fileType) {
UnixFileType.HYPHEN_MINUS -> true
else -> throw IllegalArgumentException("Wrong type of file")
}

//when sem argumento
val objectType = when {
fileType === UnixFileType.L -> "l"
fileType === UnixFileType.HYPHEN_MINUS -> "-"
fileType === UnixFileType.D -> "d"
else -> "unknown file type"
}

//when em coleção
val isRegularFileInDirectory = when (regularFile) {
in directory.children -> true
else -> false
}

//when com range
val isCorrectType = when (fileType) {
in UnixFileType.D..UnixFileType.L -> true
else -> false
}

//when com operador _is_
val result = when (unixFile) {
is UnixFile.RegularFile -> unixFile.content
is UnixFile.Directory -> unixFile.children.map { it.getFileType() }.joinToString(", ")
is UnixFile.SymbolicLink -> unixFile.originalFile.getFileType()
}

//when com auto-casting do Kotlin
when (view) {
is TextView -> toast(view.text)
is RecyclerView -> toast("Item count = ${view.adapter.itemCount}")
    is SearchView -> toast("Current query: ${view.query}")
else -> toast("View type not supported")
}

{% endhighlight %}

A gramática do _when_ pode ser vista no [link da linguagem](https://kotlinlang.org/docs/reference/grammar.html#whenExpression){:target="\_blank"}

## Conclusão

Conhecemos mais um recurso bacana e muito rico da linguagem Kotlin. A medida que for descobrindo mais, vou registrando aqui como nota mental e para compartilhar com outras pessoas que possam estar estudando mesmo tópico.

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- http://www.thedevpiece.com/why-you-should-avoid-if-else-statements/
- https://www.w3schools.com/java/java_switch.asp
- https://blog.codefx.org/java/switch-expressions/
- https://medium.com/better-programming/a-look-at-the-new-switch-expressions-in-java-14-ed209c802ba0
- https://www.baeldung.com/java-switch
- https://www.baeldung.com/kotlin-when
- https://kotlinlang.org/docs/reference/control-flow.html
- https://superkotlin.com/kotlin-when-statement/

<br/>
[Conheça a série sobre Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
