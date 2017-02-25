## A plataforma Java, a linguagem Java, a JVM e o suporte a outras linguagens

Hoje, trocando idéia com [Mateus](https://twitter.com/mmalaquias1) discutiamos sobre o poder da plataforma Java, e em um grupo de WhatsApp que participamos para ajudar estudantes com dúvidas de Java, ele levantou um questionamento se a galera sabia quantas linguagens a [JVM - Java Virtual Machine](https://docs.oracle.com/javase/specs/jvms/se7/html/jvms-1.html#jvms-1.2) rodava. Quando falamos a palavra Java, temos que ter consciência que temos dois significados. Uma é referente a [linguagem de programação Java](http://docs.oracle.com/javase/tutorial/java/), a outra é referente [a plataforma Java](http://www.oracle.com/technetwork/java/javase/overview/index.html). A base da plataforma Java, é a JVM. Ela que é responsável por ler o código-fonte, compilar para byte-code e esse é interpretado para código de máquina, no sistema operacional onde a JVM está hospedada.

Mas você sabia que sobre a JVM, é possível executar código de outras linguagens além da linguagem Java? Pois é, conversando com a galera, eles ficaram surpresos, por não saber a diferença entre um e outro, e esse foi o motivo que me incentivou a escrever esse post.

Fiz um levantamento (referências na seção de fontes) e encontrei diversas listas de linguagens da JVM.
As mais citadas foram:

- [Clojure](https://clojure.org/), a functional Lisp dialect
- [Groovy](http://www.groovy-lang.org/), a dynamic programming and scripting language
- [Scala](https://www.scala-lang.org/), a statically-typed object-oriented and functional programming language[1]
- [Kotlin](https://kotlinlang.org/), a statically-typed language from JetBrains, the developers of IntelliJ IDEA
- [JRuby](http://jruby.org/), an implementation of Ruby
- [Jython](http://www.jython.org/), an implementation of Python
- [FANTOM](http://fantom.org/)
- [CEYLON](https://ceylon-lang.org/)
- [XTEND](http://www.eclipse.org/xtend/) 

Me parece, que Scala, Groovy e Clojure são as mais usadas depois do Java. Kotlin tem feito ruído. Sei que em Groovy, o projeto mais famoso que eu conheço é o [Grails Framework](https://grails.org/). Nas outras linguagens, confesso que não conheço muitos projetos. 

Até JavaScript, a linguagem da moda, tem suporte na JVM. No passado existia o [projeto Rhino](https://github.com/mozilla/rhino) da fundação Mozilla, cuja evolução, virou o [projeto Nashorn](http://www.oracle.com/technetwork/articles/java/jf14-nashorn-2126515.html) a partir do Java 8. Lembrando que esse suporte a linguagens de scripts foi adicionado na release 6 do Java, através da JSR 223 ([esse link mostra a evolução do Java desde a versão 1.4](https://antoniolazaro.github.io/java/2017/01/03/evolucao-java/)).

Como na pesquisa que fiz achei um tema curioso, sobre como criar sua própria linguagem, resolvi compartilhar com vocês, alguns materiais sobre o tema:
- https://www.toptal.com/software/creating-jvm-languages-an-overview
- https://www.infoq.com/news/2011/04/new-jvm-lang
- http://help.eclipse.org/kepler/index.jsp?topic=%2Forg.eclipse.xtext.doc%2Fcontents%2F035-domainmodel-java.html

Como estamos falando de linguagens, compartilho com vocês uns sites que exibe os rankings de linguagens mais usadas. O Tiobe é o mais conhecido, na minha opnião (a depender da demanda, posso tentar escrever um post sobre isso). Java é unanime nas primeiras posições de todos rankings o que a torna uma linguagem bastante interessante para aprender.

- http://www.tiobe.com/tiobe-index/
- http://pypl.github.io/PYPL.html
- http://redmonk.com/sogrady/2016/07/20/language-rankings-6-16/
- http://www.oracle.com/technetwork/articles/java/jf14-nashorn-2126515.html

E você? Programa em outra linguagem na JVM? Compartilhe conosco o que acha sobre o tema. Gostou do post? Dá um feedback nos comentários.

[Atualização em 24/02 09:22] Nosso amigo [Ivan Queiroz](https://twitter.com/ivanqueiroz) fez [um post introdutório](http://blog.ivanqueiroz.com/2017/01/linguagens-jvm-kotlin.html) sobre [Kotlin](https://kotlinlang.org/)) em seu blog. Confiram depois e vejam como é o uso de outra linguagem dentro da JVM. Acompanhem também, o [blog de Ivan](http://blog.ivanqueiroz.com/), que tem diversos conteúdos bem interessantes. Como a série sobre padrões de projeto usando os novos recursos do Java 8.

Fontes:
- http://www.oracle.com/technetwork/articles/java/architect-languages-2266279.html
- http://www.infoworld.com/article/2627426/application-development/top-five-scripting-languages-on-the-jvm.html
- https://github.com/statusque/jvmstats/blob/master/JVM-language-activity.md
- http://www.stackoverkill.com/ranking/jvm-langs
- https://www.infoq.com/research/next-jvm-language
- https://blog.newrelic.com/2016/08/18/popular-programming-languages-2016-go/
- https://zeroturnaround.com/rebellabs/the-adventurous-developers-guide-to-jvm-languages-java-scala-groovy-fantom-clojure-ceylon-kotlin-xtend/
