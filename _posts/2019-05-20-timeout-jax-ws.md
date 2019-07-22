---
layout:     post
title:      Configurando timeout JAX-WS 
date:       20/05/2019
author:     Antonio Lazaro
summary:    Configurando timeout com JAX-WS
categories: [java,jax-ws,webservices]
thumbnail:  heart

---

## Introdução

**Atualizado em 22/07/2018**

O mundo Java tem duas especificações para trabalhar com a parte de Webservices. [Jax-WS](https://docs.oracle.com/javaee/6/tutorial/doc/bnayl.html){:target="_blank"} e [JAX-RS](https://docs.oracle.com/javaee/6/tutorial/doc/giepu.html){:target="_blank"}. JAX-WS foca na criação de serviços e clientes que seguem atendem a comunicação de serviços usando o [protocolo SOAP](https://searchmicroservices.techtarget.com/definition/SOAP-Simple-Object-Access-Protocol){:target="_blank"}.

## Um pouco sobre integração entre sistemas

Integração entre sistemas é um tema complexo e é bastante importante que o usuário da nossa aplicação, tenha visibilidade do que está acontecendo para que não pareça que nossa aplicação é lenta ou não responde, por algum problema em um sistema ao qual ela se integra, consumindo ou enviando dados.

Um ponto que nem sempre os desenvolvedores tratam, é a questão da configuração de um timeout. Timeout seria um tempo limite onde a comunicação é "encerrada" por ausência de alguma resposta.

Imagine que um serviço de um e-commerce consome a API dos correios para informar cálculo de frete e o sistema esteja fora. Não é admissível que o usuário fique aguardando 5-10 minutos para depois receber uma mensagem de erro informando que a API está fora. A experiência de uso vai embora e o cliente ficaria muito insatisfeito.

Por isso, é de extrema relevância que quando pensemos em comunicação entre serviços, tenhamos cuidado com a definição de timeout compatíveis com o contexto do projeto e do serviço em questão. Não adiante pensar em timeout de 5s se o serviço demora 20s para responder. Isso deve ser muito avaliado, testado e mensurado, antes de definir.

## Meu problema e como resolvi

Um dos projetos que trabalho tinha integração com um sistema X e esse sistema eventualmente ficava indisponível. Tinhamos feito uma implementação de timeout seguindo a estratégia abaixo:

```java
EmployeeRecordsManagementPort customerPort = service.getPort(EmployeeRecordsManagementPort.class);

		BindingProvider bindingProvider = (BindingProvider) customerPort;
		Map<String, Object> context = bindingProvider.getRequestContext();
		//context.put("com.sun.xml.internal.ws.connect.timeout", TIMEOUT_EM_MS);
		//context.put("com.sun.xml.internal.ws.request.timeout", TIMEOUT_EM_MS);
		context.put("weblogic.wsee.transport.connection.timeout", TIMEOUT_EM_MS);
        context.put("weblogic.wsee.transport.read.timeout", TIMEOUT_EM_MS);
```

Entretanto, ainda assim, quando o serviço estava fora, tinhamos problema porque não se tratava de tempo de resposta do serviço e sim uma indisponibilidade total. Eu acreditava que o parâmetro **com.sun.xml.internal.ws.connect.timeout** serviria para isso, porém no meu ambiente isso não funcionou. [Atualização]Ao encontrar as propriedades weblogic.wsee.transport.connection.timeout e weblogic.wsee.transport.read.timeout, a configuração do timeout funcionou, com o código acima.[/Atualização]

Eu estou trabalhando com Java 8 e Weblogic 12.2.3c e a única forma que encontrei do timeout funcionar foi definindo a URL, conforme código abaixo:

```java
		URL url = new URL(null,getEndpoint(),
				new URLStreamHandler() { // Anonymous (inline) class
		    @Override
		    protected URLConnection openConnection(URL url) throws IOException {
		    URL clone_url = new URL(url.toString());
		    HttpURLConnection clone_urlconnection = (HttpURLConnection) clone_url.openConnection();
		    // TimeOut settings
		    clone_urlconnection.setConnectTimeout(TIMEOUT_EM_MS);
		    clone_urlconnection.setReadTimeout(TIMEOUT_EM_MS);
		    return(clone_urlconnection);
		    }
		});
```

Embora eu tenha tentado as configurações indicadas nos posts abaixo, a única que resolveu efetivamente meu problema foi a codificação acima.

1. [Link 1](https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-client-timeout-example/){:target="_blank"}
1. [Link 2 - Mais completo](https://www.igorkromin.net/index.php/2018/12/06/setting-jax-ws-webservice-client-timeout-values-correctly-within-a-weblogic-12c-container/){:target="_blank"}

## Conclusão

Embora a documentação e o que encontrei na internet explicasse outra coisa, tive que buscar uma outra implementação que até hoje não encontro razão. Entretanto temos cronograma e entregas a fazer e nem sempre temos tempo para buscar o entendimento completo de tudo que resolvemos. Segundo meu amigo e consultor de assuntos avançados no Java, [Ivan Queiroz](http://twitter.com/ivanqueiroz/){:target="_blank"}, isso pode acontecer devido a implementação usada do JAX-WS. Ai entre variável do projeto, weblogic e ainda tem a influência do Java, qual versão tem.

Não tive tempo para investigar e vou compartilhar como eu resolvi. Se alguém tiver alguma idéia e quiser discutir essa abordagem ou uma visão de solução, deixa mensagem nos comentários do blog.

## Outras Fontes

N/A
   



