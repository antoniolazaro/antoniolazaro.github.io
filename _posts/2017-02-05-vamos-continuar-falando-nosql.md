## Vamos continuar falando de Nosql

Para quem ainda não sabe nós (Comunidades [Java Bahia](https://twitter.com/javabahia?lang=en) + [Python Bahia](https://groups.google.com/forum/#!forum/grupy-ba) + [Universidade Católica do Salvador - UCSAL](www.ucsal.br)) estamos organizando uma conferência sobre Nosql que acontecerá entre 30/03 e 01/04. Virão nomes de peso sobre o assunto e contamos com apoio de grandes empresas, como [Amazon](https://twitter.com/awscloud?lang=en) e [Microsoft](https://twitter.com/Microsoft?lang=en), além claro, da [UCSAL](https://twitter.com/ucsaloficial?lang=en).

[As incrições para o evento foram abertas oficialmente na última sexta-feira](http://javabahia.blogspot.com.br/2017/02/abertas-as-inscricoes-para-nosqlba-2017.html) e podem ser feitas nesse [link](http://inscricao.nosqlba.org/).

Mais informações do evento podem ser obtidas no [site oficial](http://nosqlba.org/).

Para ajudar a trazer mais informações sobre o tema, estamos divulgando informações sobre NoSQL. O nosso amigo [Ivan Queiroz](https://twitter.com/ivanqueiroz) iniciou o movimento de posts para trazer conhecimento sobre o assunto e também para ajudar na divulgação do evento e eu decidi dar continuidade. Se ainda não leu o [post de Ivan](http://blog.ivanqueiroz.com/2017/01/o-que-devo-saber-sobre-nosql.html), recomendo que leia, pois ele apresenta conceitos iniciais e fala da classificação desses bancos.

### Introdução

Os bancos de dados não relacionais, ou também conhecidos como NoSQL (not only SQL) surgem com objetivo de trazer novas opções de armazenamento de dados diferentes dos nossos modelos relacionais que são baseados em schemas. Sabemos que em computação não existe bala de prata, então não vamos dizer que é a melhor solução para tudo e que deve ser usada sempre, mas deve ser uma opção que deve ser considerada antes de dar uma solução em um projeto. Estamos apresentando um conceito que é conhecido como [persistência poliglota](http://christiano.me/persistencia-poliglota-e-nosql-palestra-fisl/).

### Definindo tipos

Os bancos NoSQL estão classificados em 4 grande tipos. São eles:

- Chave-valor - Os registros são armazenados como uma coleção de elementos indexados que são recuperados por uma chave. Funciona muito bem para informações no formato de listas;
- Colunar(column family) - Registro são armazenados em uma tabela, mas cada registro pode possuir várias colunas;
- Documento - Cada registro é um documento que pode ou não fazer parte de uma coleção;
- Grafo - Os registros são nós em um grafo interligados por arestas que representam o tipo de relacionamento entre eles;
- Multimodelo - Suporta mais de um paradigma.

### Quando usar?

Fica ai uma questão, em qual contexto é sugerido o uso de cada tipo de banco desse? Vou trazer alguns cenários com exemplos para ajudar nesse entendimento (**lembrando que não pretendo definir, apenas apresentar alguns cenários**)

### Chave-valor:
  * Exemplos de contexto onde pode ser usado:
    * Armazenar dados de sessão, preferência e perfil de usuário
    * Dados do carrinho de compras
    * Não é recomendado o uso quando a data de persistência é algo importante 
    * Usualmente utilizado como mecanismo de cache  
  * Exemplos de empresas que usam:
    * Twitter
    * Github
    * Stackoverflow
  * Exemplos de bancos desse tipo:
    * [DynamoDB](https://aws.amazon.com/dynamodb/) - **Teremos mini-curso e palestra sobre esse banco**
    * [Redis](https://redis.io/) - **Teremos palestra sobre esse banco.**
    * [Riak](http://basho.com/products/#riak)
    * [Memcache](http://memcachedb.org/)

### Colunar (column family):
  * Exemplos de contexto onde pode ser usado:
    * Tratamento de largo volume de dados (a partir de Terabytes) com demanda de alta performance em leitura e escrita e alta disponibilidade
    * Aplicações distribuídas entre diversos datacenters
    * Aplicações que podem tolerar uma curta inconsistência entre os dados da replica
    * Aplicações com campos dinâmicos 
  * Exemplos de empresas que usam:
    * IBM
    * Apple
    * Netflix
  * Exemplos de bancos desse tipo:
	* [Cassandra](http://cassandra.apache.org/) 
    * [Hadoop](http://hadoop.apache.org/)
    * [Elassandra](https://github.com/strapdata/elassandra)
  
### Documento:
  * Exemplos de contexto onde pode ser usado: ([fonte](http://tech.leroymerlin.com.br/devemos-usar-nosql-e-mongodb)):
    * Os dados não se encaixam no modelo relacional
    * Quando seus dados são na verdade objetos
    * Quando sua aplicação valida a consistência dos dados, não o banco
    * Quando o projeto da aplicação é orientado ao domínio
    * Quando seu projeto precisa se adaptar a mudanças
    * Quando a escalabilidade é importante
    * Quando você **não** precisa de transações e ACID ([atomicity, consistency, isolation, and durability](http://searchsqlserver.techtarget.com/definition/ACID))
  * Exemplos de empresas que usam:  
    * Cisco
    * Google 
    * Ebay
  * Exemplos de bancos desse tipo:
    * [CouchDB](http://couchdb.apache.org/)
    * [MongoDB](https://www.mongodb.com/) **Teremos mini-curso e palestra sobre esse banco**
    * [Elastic](https://www.elastic.co/)

### Grafo:
  * Exemplos de contexto onde pode ser usado:
    * Toda vez que for necessário persistir um grafo. Um grafo é um elemento composto de um nó e uma relação.
    * Cada nó representa uma entidade e uma relação, é uma ligação entre essas entidades.
    * Exemplo mais comum: rede social.
    * Dados espaciais, sistemas de recomendação também usam esse tipo de banco de dados.
  * Exemplos de empresas que usam:
    * Nasa
    * Walmart
    * Linkedin
  * Exemplos de bancos desse tipo:
    * [HyperGraphDB](http://www.kobrix.com/hgdb.jsp)
    * [OrientDB](http://orientdb.com/)
    * [Neo4j](https://neo4j.com/) **Teremos mini-curso e palestra sobre esse banco**
    
### Multimodelo
  * Exemplos de empresas que usam:
    * Fox Sports
    * Dell
    * Ericsson
  * Exemplos de bancos desse tipo:
    * [OrientDB](http://orientdb.com/)
   
Fontes:
<br /> - [Post introdutório no blog de Ivan Queiroz](http://blog.ivanqueiroz.com/2017/01/o-que-devo-saber-sobre-nosql.html)
<br /> - [Livro da Casa do Código - NoSQL Como armazenar os dados de uma aplicação moderna](https://www.casadocodigo.com.br/products/livro-nosql)
<br /> - [http://tech.leroymerlin.com.br/devemos-usar-nosql-e-mongodb](http://tech.leroymerlin.com.br/devemos-usar-nosql-e-mongodb)
<br /> - [Nosql Database (reune todos bancos Nosql disponíveis)](http://nosql-database.org/)
<br /> - [http://www.slideshare.net/steppat/nosql-por-que-e-quando-usar](http://www.slideshare.net/steppat/nosql-por-que-e-quando-usar)
<br /> - [http://christiano.me/persistencia-poliglota-e-nosql-palestra-fisl/](http://christiano.me/persistencia-poliglota-e-nosql-palestra-fisl/)
<br /> - [https://neo4j.com/why-graph-databases/](https://neo4j.com/why-graph-databases/)
<br /> - [https://www.thoughtworks.com/insights/blog/nosql-databases-overview](https://www.thoughtworks.com/insights/blog/nosql-databases-overview)
<br /> - [http://www.3pillarglobal.com/insights/exploring-the-different-types-of-nosql-databases](http://www.3pillarglobal.com/insights/exploring-the-different-types-of-nosql-databases)
