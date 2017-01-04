---
layout:     post
title:      Evolução Java
date:       03/01/2017
author:     Antonio Lazaro
summary:    Evolução Java
categories: java
thumbnail:  heart
tags:
 - jdk
 - jvm
 - java

---

Evolução Java (JVM, JDK) 1.4 -> 1.9
===================

A idéia desse post é apresentar um pouco dos recursos a cada nova release do JDK ao longo do tempo, partindo da versão 1.4 até a versão 9.
Posteriormente, pretendo abordar como a JVM evoluiu e suporta outras linguagens além do Java.

Irei apresentar os novos recursos a cada release para que possamos relembrar o que foi adicionado e ao mesmo tempo façamos uma reflexão. "***Com tantos novos recursos, por que uma parte de nós continuamos com códigos feitos com recursos da versão 1.4 e 1.5?***"

A plataforma Java é definida através de JSRs (Java Specification Request) que são aprovadas pelo JCP (Java Comunitty Process)

J2SE 1.4
-------------

**Características:**

- **Codename:** Merlin
- **Release date:** 06/02/2002
- **Public support and security updates:** Até outubro de 2008
- **Private support and security updates:** Até fevereiro de 2013
- **Mudanças na plataforma:**
* * *assert keyword (specified in JSR 41)*
* * Regular expressions modeled after Perl regular expressions
* * Exception chaining allows an exception to encapsulate original lower-level exception
* * Internet Protocol version 6 (IPv6) support
* * Non-blocking IO (named New Input/Output, NIO) (specified in JSR 51)
* * Logging API (specified in JSR 47)
* * Image I/O API for reading and writing images in formats like JPEG and PNG
* * Integrated XML parser and XSLT processor (JAXP) (specified in JSR 5 and JSR 63)
* * Integrated security and cryptography extensions (JCE, JSSE, JAAS)
* * Java Web Start included (Java Web Start was first released in March 2001 for J2SE 1.3) (specified in JSR 56)
* * Preferences API (java.util.prefs)

J2SE 5.0
-------------

Nessa release (inicialmente numerada com J2SE 1.5) foi definida uma mudança na nomenclatura do número da versão para melhor refletir o nível de maturidade, estabilidade, escalabilidade e segurança do J2SE.

Essa foi a última release que foi recebeu suporte oficial das versões 98 e ME do Windows. Essa release também foi a última a suportar o Windows 95 e NT 4.0. 

Ela foi disponibilizada no Apple Mac OS X 10.4 (Tiger) e foi a versão default do Apple Mac OS X 10.5 (Leopard).

Esta foi uma release onde o Java (linguagem) recebeu suporte a novos recursos, esses bastante importante e revolucionários, como podemos destacar: *Generics, Metadata (annotations), Enumerations, for each* e *static imports*.

> **Características:**

- **Codename:** Tiger
- **Release date:** 30/09/2004
- **Difference date from the latest release:** 2 years, 7 months, 24 days
- **Public support and security updates:** 03/11/2009
- **Private support and security updates:** 05/2015
- **Mudanças na plataforma:**
* * 	Generics: provides compile-time (static) type safety for collections and eliminates the need for most typecasts (type conversion) (specified by JSR 14)
* * 	Metadata: also called annotations; allows language constructs such as classes and methods to be tagged with additional data, which can then be processed by metadata-aware utilities (specified by JSR 175)
* * 	Autoboxing/unboxing: automatic conversions between primitive types (such as int) and primitive wrapper classes (such as Integer) (specified by JSR 201)
* * 	Enumerations: the enum keyword creates a typesafe, ordered list of values (such as Day.MONDAY, Day.TUESDAY, etc.); previously this could only be achieved by non-typesafe constant integers or manually constructed classes (typesafe enum pattern) (specified by JSR 201)
* * 	Varargs: the last parameter of a method can now be declared using a type name followed by three dots (e.g. void drawtext(String... lines)); in the calling code any number of parameters of that type can be used and they are then placed in an array to be passed to the method, or alternatively the calling code can pass an array of that type
* * 	Enhanced for each loop: the for loop syntax is extended with special syntax for iterating over each member of either an array or any Iterable, such as the standard Collection classes (specified by JSR 201)
* * 	Improved semantics of execution for multi-threaded Java programs; the new Java memory model addresses issues of complexity, effectiveness, and performance of previous specifications[17]
* * 	Static imports
There were also the following improvements to the standard libraries:
* * 	Automatic stub generation for RMI objects
* * 	Swing: New skinnable look and feel, called synth
* * 	The concurrency utilities in package java.util.concurrent[18]
* * 	Scanner class for parsing data from various input streams and buffers

Java SE 6
-------------

A partir dessa release a versão do Java mudou o padrão de nomenclatura definitivamente. A grande maioria das mudanças foram internas na JVM, não havendo tantas mudanças na linguagem Java, mas a partir dessa release foi adicionado o suporte a linguagens de scripts na JVM (JSR 223). Esse é o tema que pretendo abordar em outro post, mas é bem interessante saber que a JVM roda mais de 50 linguagens nos dias atuais.

> **Características:**

- **Codename:** Mustang
- **Release date:** 11/12/2006
- **Difference date from the latest release:** 2 years, 2 months, 11 days
- **Public support and security updates:** 02/2013
- **Private support and security updates:** 12/2018
- **Mudanças na plataforma:**
* * 	Support for older Win9x versions dropped; unofficially, Java 6 Update 7 was the last release of Java shown to work on these versions of Windows.[citation needed]This is believed[by whom?] to be due to the major changes in Update 10.
* * 	Scripting Language Support (JSR 223): Generic API for tight integration with scripting languages, and built-in Mozilla JavaScript Rhino integration.
* * 	Dramatic performance improvements for the core platform,[27][28] and Swing.
* * 	Improved Web Service support through JAX-WS (JSR 224).
* * 	JDBC 4.0 support (JSR 221).
* * 	Java Compiler API (JSR 199): an API allowing a Java program to select and invoke a Java Compiler programmatically.
* * 	Upgrade of JAXB to version 2.0: Including integration of a StAX parser.
* * 	Support for pluggable annotations (JSR 269).[29]
* * 	Many GUI improvements, such as integration of SwingWorker in the API, table sorting and filtering, and true Swing double-buffering (eliminating the gray-area effect).
* * 	JVM improvements include: synchronization and compiler performance optimizations, new algorithms and upgrades to existing garbage collection algorithms, and application start-up performance.

Java SE 7
-------------

Em 2010, a Oracle comprou a Sun Microsystems (empresa que era responsável pelo Java) por aproximadamente US$ 7.4 bilhões. A partir dessa data a JDK passou a ser desenvolvida sob o projeto [Open JDK](http://openjdk.java.net/faq/). 
Algumas evoluções na linguagem Java foram adicionadas e melhorias na API de IO e concorrência foram as principais novidades dessa versão. 

> **Características:**

- **Codename:** Dolphin
- **Release date:** 07/2011
- **Difference date from the latest release:** 4 years, 6 months, 20 days
- **Public support and security updates:** 03/2014
- **Private support and security updates:** 07/2022
- **Mudanças na plataforma:**
* * 	JVM support for dynamic languages, with the new invokedynamic bytecode under JSR-292,[115] following the prototyping work currently done on the Multi Language Virtual Machine
* * 	Compressed 64-bit pointers[116] (available in Java 6 with -XX:+UseCompressedOops)[117]
* *  JDBC 4.1
* * 	Concurrency utilities under JSR 166[126]
* * 	New file I/O library (defined by JSR 203) adding support for multiple file systems, file metadata and symbolic links. The new packages are java.nio.file, java.nio.file.attribute and java.nio.file.spi[127][128]
* * 	Timsort is used to sort collections and arrays of objects instead of merge sort
* * 	Library-level support for elliptic curve cryptography algorithms
* * 	An XRender pipeline for Java 2D, which improves handling of features specific to modern GPUs
* * 	New platform APIs for the graphics features originally implemented in version 6u10 as unsupported APIs[129]
* * 	Enhanced library-level support for new network protocols, including SCTP and Sockets Direct Protocol
* * 	Upstream updates to XML and Unicode
* * 	Java Deployment Rulesets[130]
* * 	These small language changes (grouped under a project named Coin):[118]
* * * 	Strings in switch[119]
* * * 	Automatic resource management in try-statement[120]
* * * 	Improved type inference for generic instance creation, aka the diamond operator <>[121]
* * * 	Simplified varargs method declaration[122]
* * * 	Binary integer literals[123]
* * * 	Allowing underscores in numeric literals[124]
* * * 	Catching multiple exception types and rethrowing exceptions with improved type checking[125]

Java SE 8
-------------

Evoluções revolucionárias na JVM desde a versão 5 vieram com essa release. Suporte a programação funcional com uso de expressões lambdas.

Essa release não é suportada no Windows XP (antes da relase update 25).

A partir dessa release a definição passou a ser realizada através de JEP (JDK Enhancement Proposal) e JSR (Java Specification Request)

> **Características:**

- **Codename:** Kenai
- **Release date:** 18/03/2014
- **Release atual:**: JDK 8 update 111
- **Difference date from the latest release:** 2 years, 8 months, 17 days
- **Public support and security updates:** 09/2017
- **Private support and security updates:** 03/2025
- **Mudanças na plataforma:**
* * JSR 335, JEP 126: Language-level support for lambda expressions (officially, lambda expressions; unofficially, closures) under Project Lambda[196] and default methods (virtual extension methods)[197][198][199] which allow the addition of methods to interfaces without breaking existing implementations. There was an ongoing debate in the Java community on whether to add support for lambda expressions.[200][201] Sun later declared that lambda expressions would be included in Java and asked for community input to refine the feature.[202] Supporting lambda expressions also allows the performance of functional-style operations on streams of elements, such as MapReduce-inspired transformations on collections. Default methods allow an author of an API to add new methods to an interface without breaking the old code using it. Although it was not their primary intent,[197] default methods also allow multiple inheritance of behavior (but not state).
* * JSR 223, JEP 174: Project Nashorn, a JavaScript runtime which allows developers to embed JavaScript code within applications
* * JSR 308, JEP 104: Annotation on Java Types[203]
* * Unsigned Integer Arithmetic[204]
* * JSR 337, JEP 120: Repeating annotations[205]
* * JSR 310, JEP 150: Date and Time API[206]
* * JEP 178: Statically-linked JNI libraries[207]
* * JEP 153: Launch JavaFX applications (direct launching of JavaFX application JARs)[208]
* * JEP 122: Remove the permanent generation[209]

Java SE 9
-------------

O lançamento estava previsto para 22/09/2016. A Oracle mudou para 23/03/2017 e depois anunciou que seria julho/2017. A principal complexidade que vem gerando o atraso tem relação com a modularização da JVM (projeto Jig Saw).

> **Características:**

- **Codename:** Não definido
- **Release date:** 07/2017 **(Previsão)**
- **Difference date from the latest release:**  3 years, 3 months, 13 days **(se concluído de fato em julho/2017).
- **Public support and security updates:** *TBD (to be defined)*
- **Private support and security updates:** *TBD (to be defined)*
- **Mudanças na plataforma:**
* * JSR 376: Modularization of the JDK under Project Jigsaw (Java Module System)[132][243][244]
* * JEP 222: jshell: The Java Shell (a Java REPL)[245][246]
* * JEP 295: Ahead-of-Time Compilation[247]
* * JEP 268: XML Catalogs[248]

**Encontrei essa figura que mostra a divisão por categorias dos recursos.**

![fonte: https://blogs.oracle.com/java/jdk-9-categories](https://cdn.app.compendium.com/uploads/user/e7c690e8-6ff9-102a-ac6d-e4aebca50425/9f78fc09-faec-4068-82bd-09e7cc8bbf34/Image/05d573b4e13da18bf6a372dce5bf175b/screen_shot_2016_09_08_at_7_30_30_am.png)

----------
Fontes (**Links:**)

* https://blogs.oracle.com/java/jdk-9-categories 
* https://en.wikipedia.org/wiki/Java_version_history 
* http://javapapers.com/core-java/java-features-and-history/ 
* http://www.theregister.co.uk/2016/09/14/jdk_9_release_delay/
* http://www.oracle.com/technetwork/java/eol-135779.html
* http://openjdk.java.net/projects/jdk7/features/
* http://openjdk.java.net/projects/jdk8/features
* http://openjdk.java.net/faq/
* http://openjdk.java.net/projects/jdk6/
* http://openjdk.java.net/projects/jdk7/
* http://openjdk.java.net/projects/jdk8/spec/
* http://openjdk.java.net/projects/jdk9/spec/
* http://openjdk.java.net/projects/jdk10/
