---
layout: post
title: Aprendizado Kotlin - Alguns recursos da linguagem
date: 21/04/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Alguns recursos da linguagem
categories: [kotlin]
thumbnail: heart
---

## Introdução

Durante o [curso de Kevin Jones "Getting Started with Kotlin" da Plural Sight](https://app.pluralsight.com/library/courses/kotlin-getting-started/table-of-contents){:target="\_blank"} tive oportunidade de conhecer alguns conceitos de Kotlin que achei bastante interessante e resolver compartilhar.

No próprio site da linguagem, existem [vários tutoriais](https://kotlinlang.org/docs/tutorials/) e [recomendações de livros](https://kotlinlang.org/docs/books.html){:target="\_blank"}, alem do próprio [Getting Started do site que fala de diversas características e recursos da linguagem e ferramentas associadas](https://kotlinlang.org/docs/tutorials/getting-started.html){:target="\_blank"}. Achei também o [guia de referência da linguagem muito rico e completo](https://kotlinlang.org/docs/reference/){:target="\_blank"}.

Para quem se interessa pela estrutura da linguagem, existe disponível também a [gramática da linguagem](https://kotlinlang.org/docs/reference/grammar.html){:target="\_blank"}.

## Recursos da linguagens observadores e experimentados

Nessa seção, pretendo falar de alguns recursos que pude experimentar durante o curso, e pratiquei em um projeto piloto que está disponível em um repositório no meu github onde pretendo colocar os demos do que ando testando com Kotlin. Esse repositório é o [kotlin-lab](https://github.com/antoniolazaro/kotlin-lab){:target="\_blank"}.

### Declaração de variáveis e propriedades: val x var - Suporte a imutabilidade de objetos nativamente

Em kotlin para declarar uma variável é possível a seguinte estrutura

<val|var> <propertyName>[propertyType] = <propertyValue>

A estrutura acima é explicada da seguinte forma:

- val = Variável é imutável. Uma vez atribuído um valor, a referência não pode mais mudar. Se houver essa tentativa de atribuição, o compilador acusa erro.
- var = Variável mutável. Comum como qualquer variável.
- propertyName = nome da variável ou propriedade.
- propertyType = atributo opcional. Caso não seja declarado, será colocado por inferência pela atribuição da primeira referência. Uma vez atribuido, esse tipo não pode receber outro tipo. A linguagem Kotlin não é dinamicamente tipada como JavaScript.
- propertyValue = Valor atribuído da variável.

{% highlight kotlin %}
val teste: String;
teste = "Teste";
teste = "Teste 2"; //erro de compilação por fazer uma reatribuição
teste = 10; //erro de compilação por atribuir outro tipo
val inteiro; //erro de compilação. Não é possível fazer inferência sem atribuição e sem definir o tipo
{% endhighlight %}

#### Uso de constantes

Para declaração de constantes existe a palavra reserva **_const_**. Exemplo:

{% highlight kotlin %}
const val x = 2
{% endhighlight %}

### Tipos primitivos

Os tipos primitivos de Kotlin são objetos.

<br/>
_**Tipos primitivos inteiros e suas faixas de valores:**_
![](/static/img/kotlin/primite-integer.png)

<br/>
_**Tipos primitivos booleanos e de ponto fluante e suas faixas de valores.:**_
![](/static/img/kotlin/float-point-others.png)

### Strings

Strings são literais definidos entre _""_. Em Kotlin ela é uma sequencia imutável de códigos UTF-16.

#### String templates

Em Kotlin, é possível trabalhar com String Templates, como no JavScript, onde variáveis podem ser acessadas através do caracter _\$_, evitando assim a necessidade de concatenação de Strings. Caso seja necessário usar o caracter _\$_, deve ser feito o uso do escape: _\\\$_

Exemplo:
{% highlight kotlin %}
val name = "Anne"
val yearOfBirth = 1985
val yearNow = 2018
val message = "$name is ${yearNow - yearOfBirth} years old"
{% endhighlight %}

### Condicionais (if/else)

A condição fica entre parenteses _()_ e o corpo da condição deve ser envolvido por chaves _{}_. A condição deve ter retorno booleano.

{% highlight kotlin %}
val age = 42
if (age < 10) {
println("You're too young to watch this movie")
} else if (age < 13) {
println("You can watch this movie with a parent")
} else {
println("You can watch this movie")
}
{% endhighlight %}

Como em outras linguagens de programação, o uso da condicional sem as chaves envolve o risco de alguma condição não ser devidamente executada, por isso, é extremamente recomendado se trabalhar com essa sinalização explicitamente.

{% highlight kotlin %}
if (age < 10)
println("You're too young to watch this movie")
println("You should go home") // Erro de lógica, esse trecho de código sempre será executado, independente da condicional.
{% endhighlight %}

O if/else é também uma expressão, o que pode funcionar como um operador ternário em Java. Quando se usa essa condição, é obrigatório definir um regra para o bloco _else_.
{% highlight kotlin %}
val result = if (condition) trueBody else falseBody
{% endhighlight %}

### Comparações

Estrutura de comparação são feitas sempre com _==_ ou _!=_. Quando invocados esses símbolos, eles automaticamente invocam o equals da classe em questão.

Comparações são chamadas de equalidade estrutural e o compilador traduz a == b, conforme exemplo abaixo:
{% highlight kotlin %}
a?.equals(b) ?: (b === null)
{% endhighlight %}

Para comparação de referência, deve ser utilizado os operadores _===_ ou _!==_.

### When

Esse operador seria equivalente ao Switch do Java, só que é um switch/case muito mais robusto.

Alguns exemplos de uso:

{% highlight kotlin %}
when (x) {
1 -> print("x == 1")
2 -> print("x == 2")
else -> { // Note the block
print("x is neither 1 nor 2")
}
}
{% endhighlight %}

Combinando diversos valores para mesma condição:
{% highlight kotlin %}
when (x) {
0, 1 -> print("x == 0 or x == 1")
else -> print("otherwise")
}
{% endhighlight %}

Pode ser usada expressões como condição:
{% highlight kotlin %}
when (x) {
parseInt(s) -> print("s encodes x")
else -> print("s does not encode x")
}
{% endhighlight %}

E tem suporte a negação através do caracter _!_ e a range (intervalos), bem como coleções.
{% highlight kotlin %}
when (x) {
in 1..10 -> print("x is in the range")
in validNumbers -> print("x is valid")
!in 10..20 -> print("x is outside the range")
else -> print("none of the above")
}
{% endhighlight %}

### Estruturas de repetição

#### for

For faz iteração através de qualquer coisa que provenha um iterator. Similar ao que temos de foreach do Java.

{% highlight kotlin %}
for (item in collection) print(item) // exemplo 1
//ou
for (item: Int in ints) { // exemplo 2
// ...
}
for (i in array.indices) { //iterando um array ou uma lista indexada
println(array[i])
}
for (i in 1..3) { //interando um range de números
println(i)
}
for (i in 6 downTo 0 step 2) { //iterando uma contagem regressiva, definindo o salto
println(i)
}
for (x in 0 until 10 step 2) println(x) // Prints 0, 2, 4, 6, 8

// Iterate over the entries as objects that contain the key and the value as properties
for (entry in map) {
println("${entry.key}: ${entry.value}")
}
// Iterate over the entries as separate key and value objects
for ((key, value) in map) {
println("$key: $value")
}

// Iterate over the keys
for (key in map.keys) {
println(key)
}

// Iterate over the values
for (value in map.values) {
println(value)
}
{% endhighlight %}

#### while/do-while

Não tem muita mudança em relação a outras linguagens.

{% highlight kotlin %}
while (x > 0) {
x--
}

do {
val y = retrieveData()
} while (y != null) // y is visible here!
{% endhighlight %}

### Collections

A classe Array é equivalente ao array[] do Java. Esse tipo de lista tem um tamanho fixo. As principais estruturas de dados do Java existem em Kotlin. Além do Array, temos o List, Set (dados não se repetem baseado na regra do equals) e Map (chave/valor). O map equivale ao dicionário (dict) do Python.

Exemplo de como criar collections em Kotlin:
{% highlight kotlin %}
val strings = listOf("Anne", "Karen", "Peter") // List<String>
val map = mapOf("a" to 1, "b" to 2, "c" to 3) // Map<String, Int>
val set = setOf("a", "b", "c") // Set<String>
{% endhighlight %}

A sintaxe acima cria listas imutáveis. Não pode ser modificado nem o tamanho, nem seus elementos. Para criação de listas mutáveis, existem outros métodos:
{% highlight kotlin %}
val strings = mutableListOf("Anne", "Karen", "Peter")
val map = mutableMapOf("a" to 1, "b" to 2, "c" to 3)
val set = mutableSetOf("a", "b", "c")
{% endhighlight %}

Para criar coleções vazias, é necessário definir o tipo ou colocar a tipificação no método de criação. Como na sintaxe abaixo:
{% highlight kotlin %}
val noInts: List<Int> = listOf()
val noStrings = listOf<String>()
val emptyMap = mapOf<String, Int>()
{% endhighlight %}

Hierarquia de interfaces em Kotlin segue conforme figura abaixo:
![](/static/img/kotlin/collections-kotlin.png)

De maneira resumida:

- Collection é usada quando podemos trabalhar tanto com List quanto com Set.
  = MutableCollection é Collection com operações de escrita add/remove.
- List é usado preservando a ordem e podendo ser acessado por índice. Os índices iniciam em zero e o último elemento é list.size-1. A lista suporta elementos null, inclusive que podem se repetir. Duas listas são consideradas iguais se elas tem o mesmo tamanho e os elementos são iguais e estão na mesma posição. Implementação default é ArrayList.
- MutableList: É uma lista com operação de escritas add/remove (existem outros métodos)
- List x Array: Eles são muito similares entretanto, um array tem seu tamanho definido na sua inicialização e nunca mudará. Uma lista ela não tem um tamanho pré-definido, e pode mudar de tamanho a partir de operações de escrita.
- Set: Armazena elementos únicos (exclusivos). A ordem normalmente não é um critério relevante. Pode armazenar, um e apenas um valor null. Duas coleções desse tipo são iguais se tem o mesmo tamanho e possuem os mesmos elementos. Implementação default é LinkedHashSet que preserva ordem de inseração, porém existe HashSet que a ordem não é relevante e consequentemente é mais performática que a estrutura default;
- MutableSet: Set com operações de escrita.
- Map: Estrutura com chave/valor. Lembra um cache ou uma tabela de banco de dados. As chaves são unicas e os valores podem ser repetidos se as chaves forem diferentes. Dois maps são iguais se possuem se suas chaves/valores são iguais. A implementação default é LinkedHashMap que preserva a ordem de inserção. Como alternativa tem o HashMap que não guardar a ordem de inseração e se baseaia no código hash, como no HashSet.
- MutableMap: É um map com operação de escrita.

Um recurso bastante interessante em Kotlin é que você pode utilizar operadores _+_ e _-_ para coleções.

{% highlight kotlin %}
val numbers = listOf("one", "two", "three", "four")
val plusList = numbers + "five"
val minusList = numbers - listOf("three", "four")
println(plusList)
println(minusList)
{% endhighlight %}

## Conclusão

Nesse estudo, comparei com Java as estruturas básicas de programação com Kotlin. Nos próximos, pretendo trazer outros recursos que a linguagem oferece.

## Outras Fontes:

- Sobre atributos, variáveis (mutáveis ou não), constantes
  <br/> -- https://kotlinlang.org/docs/reference/properties.html
  <br/> -- https://kotlinlang.org/docs/tutorials/kotlin-for-py/declaring-variables.html

- Sobre strings:
  <br/> -- https://kotlinlang.org/docs/tutorials/kotlin-for-py/strings.html

- Condicional:
  <br/> -- https://kotlinlang.org/docs/tutorials/kotlin-for-py/conditionals.html

- When:
  <br/> -- https://kotlinlang.org/docs/reference/control-flow.html#when-expression

- for:
  <br/> -- https://kotlinlang.org/docs/reference/control-flow.html#for-loops

- Collections:
  <br/> -- https://kotlinlang.org/docs/reference/collections-overview.html
  <br/> -- https://kotlinlang.org/docs/tutorials/kotlin-for-py/collections.html

- whil/do-while:
  <br/> -- https://kotlinlang.org/docs/reference/control-flow.html#while-loops

- Collections:
  <br/> -- https://kotlinlang.org/docs/tutorials/kotlin-for-py/collections.html
