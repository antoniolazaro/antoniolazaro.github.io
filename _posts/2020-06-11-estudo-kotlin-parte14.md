---
layout: post
title: Aprendizado Kotlin - Scope Functions
date: 11/06/2020
author: Antonio Lazaro
summary: Aprendizado Kotlin - Scope Functions
categories: [kotlin]
thumbnail: heart
---

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Introdução

Continuando aprendizado e descoberta sobre Kotlin. Falaremos sobre scope functions. Esse post, especificamente, basicamente foi uma tradução da excelente documentação da linguagem sobre os recursos. Existem outras referências que usei para complementar, entretanto achei muito boa, a qualidade da [documentação](https://kotlinlang.org/docs/reference/scope-functions.html)){:target="\_blank"}.

## Recursos da linguagens observadores e experimentados

Recurso de scope function é um recurso de linguagens funcionais onde é possível aplicar transformações e tratamentos em um objeto em um escopo de função. A biblioteca padrão de Kotlin, oferece funções diversas para executar um bloco de código dentro do contexto de um objeto. Dentro desse contexto, é possível utilizar esse objeto sem seu nome. São 5 funções: let, run, with, apply e also. Particulamente vejo 5 formas diferentes de fazer a mesma coisa com pequenas diferenças, aumentando apenas a gama de vocabulário, acredito que com objetivo de oferecer melhores possibilidades de legibilidade do código, mas na documentação oficial, a linguagem fala sobre como o objeto se torna disponível após o bloco e qual resultado da expressão.

O uso dessas funções não incrementa nenhuma capacidade técnica adicional, o objetivo principal é fornecer uma opção de escrita de código mais consistente e com melhor legibilidade.

Basicamente tem duas principais diferenças entre essas funções:

- A forma que o contexto do objeto é referenciado
- O valor retornado pela função

Para cada função o contexto do objeto é disponibilizado por uma referência ao objeto a partir de seu nome atual. Cada scope function usa uma das duas formas para acessar o contexto do objeto:

- Como uma função lambda, onde o objeto em questão será referenciado como _this_.
- Como parâmetro de uma função lambida , onde o objeto em questão será referenciado como _it_.

Exemplo:

{% highlight kotlin %}
fun main() {
val str = "Hello"
// this
str.run {
println("The receiver string length: $length")
        //println("The receiver string length: ${this.length}") // does the same
}

    // it
    str.let {
        println("The receiver string's length is ${it.length}")
    }

}
{% endhighlight %}

Abaixo, falamos um pouco sobre this e it.

### this

Usado nas funções _run_, _with_ e _apply_, nessas funções a referência do contexto do objeto é uma função lambda. Na maioria dos casos _this_ pode ser omitido quando se tenta acessar os membros do objeto recebido, tornando o código mais enxuto. Porém, essa prática que pode dificultar legibilidade e entendimento do código porque dificulta diferenciar quais são os atributos/valores externos ao objeto e quais são interno. Esse cenário, é recomendado para lambadas que operam os atributos do objeto em questão.

{% highlight kotlin %}
val adam = Person("Adam").apply {
age = 20 // same as this.age = 20 or adam.age = 20
city = "London"
}
println(adam)
}
{% endhighlight %}

### it

Usado nas funções _let_ e _also_, nessas funções, o contexto do objeto é um argumento da função lambda e não a função em si. Se o nome do argumento não é indicado, o nome default _it_ é usado. Essas formas são mais legíveis, porque oferecem possibilidade de nomear como quiser, e _it_ é menos confuso que _this_. Esse uso é mais recomendado que o objeto é usado como arugmento da função. É recomendado também se for utilizado para múltiplos trechos no código.

{% highlight kotlin %}
fun getRandomInt(): Int {
return Random.nextInt(100).also {
writeToLog("getRandomInt() generated value \$it")
}
}

val i = getRandomInt()

//modificando nome da variável
fun getRandomInt(): Int {
return Random.nextInt(100).also { value ->
writeToLog("getRandomInt() generated value \$value")
}
}

val i = getRandomInt()
{% endhighlight %}

### Return value

- _apply_ e _also_ returna o contexto do objeto.

Exemplo de uso:
{% highlight kotlin %}
val numberList = mutableListOf<Double>()
numberList.also { println("Populating the list") }
.apply {
add(2.71)
add(3.14)
add(1.0)
}
.also { println("Sorting the list") }
.sort()

fun getRandomInt(): Int {
return Random.nextInt(100).also {
writeToLog("getRandomInt() generated value \$it")
}
}

val i = getRandomInt()

{% endhighlight %}

- _let_, _run_ e _with_ returna o resultado da função lambda.

{% highlight kotlin %}
val numbers = mutableListOf("one", "two", "three")
val countEndsWithE = numbers.run {
add("four")
add("five")
count { it.endsWith("e") }
}
println("There are \$countEndsWithE elements that end with e.")

val numbers = mutableListOf("one", "two", "three")
with(numbers) {
val firstItem = first()
val lastItem = last()  
 println("First item: $firstItem, last item: $lastItem")
}
{% endhighlight %}

Baseado nesses dois critérios acima explicados, você deve avaliar e utilizar a função que faz mais sentido para seu cenário de uso.

## Uso de cada função

Explicado o contexto, a idéia é mostrar exemplos mais detalhados de cada função. Tecnicamente as funções são intercambiáveis na maioria dos cenários.

### let

- Contexto do objeto é disponibilizado como um argumento (it).
- Valor de retorno é o resultado de uma lambda.
- Sugestão de uso: Invocar uma ou mais funções no resultado de uma chamada aninhada. O exemplo abaixo imprime o resultado de duas operações em uma collection.

{% highlight kotlin %}
//sem uso de let
val numbers = mutableListOf("one", "two", "three", "four", "five")
val resultList = numbers.map { it.length }.filter { it > 3 }
println(resultList)

//com uso de let
val numbers = mutableListOf("one", "two", "three", "four", "five")
numbers.map { it.length }.filter { it > 3 }.let {
println(it)
// and more function calls if needed
}

/\_ Se o código contem apenas uma função que recebe it como argumento, pode ser usado a sintaxe de método reference ao invés da função lambda, tornando o código mais curto. \*/
val numbers = mutableListOf("one", "two", "three", "four", "five")
numbers.map { it.length }.filter { it > 3 }.let(::println)

{% endhighlight %}

Normalmente _let_ é usado para executar blocos de código com valores não nulos. Para objetos em objetos que podem ser null, deve ser usado o operador _?_.

{% highlight kotlin %}
val str: String? = "Hello"  
//processNonNullString(str) // compilation error: str can be null
val length = str?.let {
println("let() called on \$it")  
 processNonNullString(it) // OK: 'it' is not null inside '?.let { }'
it.length
}
{% endhighlight %}

### with

- Contexto do objeto é passado como argumento, dentro de uma lambda e está disponível através de _this_.
- O retorno do valor é o resultado do lambda.
- Sugestão de uso: Chamada de função no contexto do objeto sem oferecer o resultado da função lambda. O exemplo abaixo pode ser lido como "com este objeto, faça o seguinte".

{% highlight kotlin %}
val numbers = mutableListOf("one", "two", "three")
with(numbers) {
println("'with' is called with argument $this")
    println("It contains $size elements")
}

val numbers = mutableListOf("one", "two", "three")
val firstAndLast = with(numbers) {
"The first element is ${first()}," +
    " the last element is ${last()}"
}
println(firstAndLast)
{% endhighlight %}

### run

- Contexto do objeto é passado como argumento, dentro de uma lambda e está disponível através de _this_.
- O retorno do valor é o resultado do lambda.
- _run_ faz o mesmo de _with_ mas ele invoca _let_ como uma extension function do contexto do objeto
- Sugestão de uso: Quando a função lambda contém ambos, a inicialização do objeto e o resultado da computação, que é retornado no valor.

{% highlight kotlin %}
val service = MultiportService("https://example.kotlinlang.org", 80)

val result = service.run {
port = 8080
query(prepareRequest() + " to port \$port")
}

// the same code written with let() function:
val letResult = service.let {
it.port = 8080
it.query(it.prepareRequest() + " to port \${it.port}")
}

val hexNumberRegex = run {
val digits = "0-9"
val hexDigits = "A-Fa-f"
val sign = "+-"

    Regex("[$sign]?[$digits$hexDigits]+")

}

for (match in hexNumberRegex.findAll("+1234 -FFFF not-a-number")) {
println(match.value)
}

{% endhighlight %}

### apply

- Contexto do objeto é passado como argumento, dentro de uma lambda e está disponível através de _this_.
- O retorno do valor é o próprio objeto
- Sugestão de uso: Normalmente usado para configuração do objeto.

{% highlight kotlin %}
val adam = Person("Adam").apply {
age = 32
city = "London"  
}
println(adam)
{% endhighlight %}

### also

- Contexto do objeto é disponível como argumento através de _it_.
- O retorno do valor é o próprio objeto.
- Sugestão de uso: Para ações que é necessário o contexto do objeto como argumento. Necessário para ações que é importante ter acesso as propriedades e funções.

{% highlight kotlin %}
val numbers = mutableListOf("one", "two", "three")
numbers
.also { println("The list elements before adding new one: \$it") }
.add("four")
{% endhighlight %}

## Resumo da ópera

| Function | Object reference | Return value        |      É uma extension function?      |
| :------- | :--------------- | :------------------ | :---------------------------------: |
| let      | it               | Resultado da lambda |                 Sim                 |
| run      | this             | Resultado da lambda |                 Sim                 |
| run      | -                | Resultado da lambda | Não: chamado sem contexto do objeto |
| with     | this             | Resultado da lambda | Não: usa o contexto como argumento  |
| apply    | this             | Objeto              |                 Sim                 |
| also     | it               | Objeto              |                 Sim                 |

### let

- Execução de lambdas em objetos não nulos.
- Introduz uma expressão como uma variável em escopo local.

### apply

- Configuração de objeto.

### run

- Configuração de objeto e computação de resultado.
- Execução de comandos onde uma expressão é requerida.

### also

- Configurações adicionais

### with

- Agrupamento de chamada de funções em um objeto

## takeIf e takeUnless

Kotlin oferece ainda em sua biblioteca padrão, as funções _takeIf_ e _takeUnless_ que basicamente servem para verificação de estados de objeto a partir de uma chamada de função.

- **_takeIf_**: Returna o objeto se o resultado do predicado é verdadeiro, caso contrário retorna null.
- **_takeUnless_**: Returna o objeto se o resultado do predicado não é verdadeiro, caso contrário retorna null.

{% highlight kotlin %}
val number = Random.nextInt(100)

val evenOrNull = number.takeIf { it % 2 == 0 }
val oddOrNull = number.takeUnless { it % 2 == 0 }
println("even: $evenOrNull, odd: $oddOrNull")

//exemplo 2
val str = "Hello"
val caps = str.takeIf { it.isNotEmpty() }?.toUpperCase()
//val caps = str.takeIf { it.isNotEmpty() }.toUpperCase() //compilation error
println(caps)
{% endhighlight %}

## Conclusão

Até o momento, me parece que Kotlin resolve muitos problemas de design do Java e vem como uma opção muito moderna para quem trabalha usando a JVM. Até o momento, o aprendizado tem sido bastante produtivo. Essas funções são bastante produtivas e otimizam a legibilidade do código.

A figura abaixo, sintetiza bacana, ela foi extraída do texto do [post.](<(https://kotlinlang.org/docs/reference/scope-functions.html)>){:target="\_blank"}

![](/static/img/kotlin/resume-scope-function.png)
<br/>

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})

## Outras Fontes:

- https://kotlinlang.org/docs/reference/scope-functions.html
- https://www.baeldung.com/kotlin-scope-functions
- https://proandroiddev.com/kotlin-scope-functions-made-simple-c59b97a04ca2
- https://dzone.com/articles/examining-kotlins-also-apply-let-run-and-with-intentions
- https://medium.com/androiddevelopers/kotlin-demystified-scope-functions-57ca522895b1
- https://medium.com/@elye.project/mastering-kotlin-standard-functions-run-with-let-also-and-apply-9cd334b0ef84

<br/>
[Voltar para o índice da série de Kotlin]({% link _posts/2020-04-20-estudo-kotlin-indice-serie.md %})
