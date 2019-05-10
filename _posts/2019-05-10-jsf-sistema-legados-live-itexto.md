---
layout:     post
title:      Live Itexto sobre JSF.
date:       16/04/2019
author:     Antonio Lazaro
summary:    C
categories: [jsf,web,carreira,java]
thumbnail:  heart

---

## Introdução

Ontem, 09/05/2019, gravamos para o [PodCast da Itexto](https://itexto.com.br/podcast/index.php/2019/05/10/4-resgatando-o-jsf/){:target="_blank"} com [Kico Lobo](https://twitter.com/loboweissmann){:target="_blank"},[Rafael Ponte](https://twitter.com/rponte){:target="_blank"}, [Ivan Queiroz](https://twitter.com/ivanqueiroz){:target="_blank"}, Thiago Jalis, [Cleison Ferreira](https://twitter.com/@mestresilfer){:target="_blank"},
[Miguelângelo Rocha](https://twitter.com/miguelangelodev){:target="_blank"} e [Ricardo Viana](https://twitter.com/richardluizv){:target="_blank"}sobre JSF (Java Server Faces) e seu uso atual. O bate papo durou por volta de 02:30 (duas horas e meia) mas foi muito bacana porque compartilhamos experiência e conhecimento. 

Kico e Rafael, eu já conhecia (Kico pessoalmente, Rafael apenas do mundo virtual). Ivan é meu amigo pessoal aqui de Salvador e os outros membros da live, conheci online.

Kico além de membro ativo da comunidade Java a muitos anos (e uma referência técnica para mim), é diretor técnico da [Itexto](http://www.itexto.com.br/site/){:target="_blank"}, empresa mineira com sede em BH que trabalha com desenvolvimento de projetos, treinamento e consultorias. Thiago, Miguelângelo, Ricardo trabalham com Kico na Itexto. Os conheci ontem na Live.

Rafael Ponte, bem, quando Kico me convidou para falar sobre JSF, não tinha como fazer uma live sobre isso, sem "o cara" do JSF. Rafael provavelmente tem os posts mais clássicos sobre JSF e atemporais, por sinal. Cara entende muito, tanto de JSF, quanto hibernate e sempre que possível, trocamos algumas idéias. O [site dele ainda está no ar](http://www.rponte.com.br/){:target="_blank"}, porém hoje ele posta mais no site da empresa atual dele, [Triad Works](http://cursos.triadworks.com.br/){:target="_blank"}

Ivan, além de amigo pessoal aqui de Salvador, é arquiteto na Indra e conhece muito de vários assuntos (técnicos ou não). Ele escreve também no [blog dele](https://ivanqueiroz.dev/){:target="_blank"}.

Feito as devidas apresentações, tentarei sintetizar um pouco do que discutimos ontem.

## Meu histórico com JSF

No meu caso, trabalho com JSF desde sua versão 1.1. Tinha expectativa de poder colocar o JSF 1.2 no primeiro projeto, mas isso ficou apenas no sonho. Esse projeto, em 2018, recebeu um aporte de modernização e por diversos fatores (técnicos e não técnicos), a decisão arquitetural foi que seria refeito usando JSF 2. Manunteção da base de código e expertise do time, foram fatores primordiais para a decisão. A expertise do time em JSF, significaria para o projeto redução de custos.

Hoje, atuo nesse projeto como arquiteto (apesar da arquitetura dele não ter sido definida/criada por mim) e sigo trabalhando. Em breve, Ivan se juntará a mim nessa saga também.

Trabalhamos em um projeto que atende todo jurídico da Telefônica, então não se trata de um sistema pouco utilizado. Ele é usado em ambiente corporativo, e não tem requisitos de uso de tela que demandem algo que o JSF não cubra. Pelo menos, até o momento...Sabemos como funciona escopo de projetos...rs

## Uso corrente do JSF

Minha constatação, é que hoje, JSF se fechará e ficará restrito aos devs do mundo Java no sentido que dificilmente pessoas de outras tecnologias virão para o mundo Java para aprender JSF, como acontece com Ruby On Rails, por exemplo. Existe a confiabilidade do mundo corporativo tradicional na suíte Oracle, mas acredito que com a maturação do ambiente JavaScript ([já estão caminhando para definir mudanças a partir de specs](https://www.ecma-international.org/publications/standards/Ecma-262.htm){:target="_blank"}), e a preferência dos desenvolvedores por trabalhar com os chamados "frameworks Javascripts modernos", o JSF deve se transformar em uma tecnologia de legado e poucos projetos novos sejam começados com essa stack em um ambiente "fora" do mundo Java.

Percebo que muitas empresas grandes utilizam JEE (JSF, EJB, JPA) e isso deve manter JSF como ferramenta de legado.

## Como devemos aprender JSF?

Como todo framework, JSF trabalha para abstrair a complexidade para o desenvolvedor. Entretanto, ele roda na Web, e na web, não tem mágica. Necessário conhecer protocolo HTTP, o que é um request, o que é um response. Acho que esse [post](http://gabsferreira.com/o-que-e-o-http-como-funciona-request-respose/){:target="_blank"} de [Gabs Ferreira](https://twitter.com/o_gabsferreira){:target="_blank"} da [Caelum](http://caelum.com.br/){:target="_blank"}/[Alura](https://www.alura.com.br/){:target="_blank"}, um bom início. A [Casa do Código](https://www.casadocodigo.com.br/){:target="_blank"}., tem um [livro muito interessante sobre o tema](https://www.casadocodigo.com.br/products/livro-desconstruindo-web){:target="_blank"}.

Um caminho para quem vem do mundo Java, recomendo que antes de estudar JSF, entenda o que são Servlets e o que foram os JSPs. Essa [apostila](https://www.caelum.com.br/apostila-java-web/){:target="_blank"} da Caelum também é muito bom sobre o tema.

A [apostila da Caelum sobre JSF](https://www.caelum.com.br/apostila-java-testes-jsf-web-services-design-patterns/introducao-ao-jsf-e-primefaces/){:target="_blank"} é um bom ponto de partida. Entretanto, antes de tudo, é importante entender conceitos básicos do JSF, e o principal dele é o ciclo de vida do mesmo.

Achei esse [tutorial](https://www.tutorialspoint.com/jsf/jsf_life_cycle.htm){:target="_blank"} que é bem prático na explicação sobre o ciclo de vida.

JSF trabalha com binding como Angular ou React, mas de uma maneira diferente, então é importante entender esse conceito.

Outros tópicos interessante para aprender em JSF:
* Validators (Beans Validation)
* Converters
* Navigation Rules
* Integração com CDI

Encontrei [esse site](https://www.vogella.com/tutorials/JavaServerFaces/article.html){:target="_blank"} que fala um pouco sobre esses pontos.

Kico Lobo e o pessoal da Itexto, estão trabalhando na escrita de um livro JSF, e conhecendo a qualidade da escrita de Kico, acredito que teremos algo fundamentado e bem usual em breve. Fiquem atentos (cobrem ele no Twitter a publicação do livro!).

Após aprender JSF, sugiro que usem o [Primefaces](https://www.primefaces.org/){:target="_blank"}. A melhor biblioteca de componentes JSF disponível no mercado, na minha opnião.
Atualmente está na versão 7.0 e evolui até mais rápido que o próprio JSF.

A galera da PrimeTech trabalha tao bem a parte de componentes que eles criaram o [PrimeNG (angular)](https://www.primefaces.org/#primeng){:target="_blank"} e o [PrimeReact](https://www.primefaces.org/#primereact){:target="_blank"}. E eles estão trabalhando no [PrimeVue](https://www.primefaces.org/introducing-primevue/){:target="_blank"} também!

## Quando usaríamos JSF?

Diante do contexto, percebi que JSF será uma tecnologia focada no mundo Java e onde entrada de dados é o foco. Com primefaces é possível ir um pouco além desse contexto pois existem muitos componentes ricos e complexos disponíveis. Data grid com filtro, carrocel, gráfico e outras coi9sas complexas. Organograma, tree table, schedule. No [showcase](https://www.primefaces.org/showcase/){:target="_blank"} é possível conhecer a suíte disponível

## Futuro JSF?

Estive em SP, entre 29/04 e 03/05 e lá, tive a oportunidade de ir a um evento onde [Ed Burns](https://twitter.com/edburns?lang=en)
{:target="_blank"}, líder das especificações de Servlet e JSF, questionado sobre o futuro do JSF, não deixou muito claro se existe um futuro na especificação principal.

Na minha visão, como existe a espec para criação do MVC 1.0 que deve ser baseada em algo como o Spring trabalha, acredito que JSF não terá muita evolução. Exceto se algum grupo, empresa ou conjunto de invididuos assuma o projeto e trabalhe nele.

## Conclusão

Uma tecnologia com um bom potencial, principalmente para times que não tem expertise em front end. Produtiva, porém com suas particularidades. Acredito que deve reduzir substancialmente, até no meio Java seu uso, principalmente pelo crescimento do Spring Boot que é "orientado a REST", essencialmente. Pelo modelo altamente acoplado, JSF não permite reuso do Controller por outros dispositivos, como acontece em projetos com APIs.

Com a dica de Rafael, conheci o projeto BootFaces que é um framework que traz Spring Boot + JSF integrados. Não conheço ainda, mas ficou a curisoidade para testar.

## Alguns links interessantes interessante que separei durante a conversa
1. [http://prevayler.org/](http://prevayler.org/){:target="_blank"}
1. [https://rubyonrails.org/](https://rubyonrails.org/){:target="_blank"}
1. [https://grails.org/](https://grails.org/){:target="_blank"}
1. [https://www.djangoproject.com/](https://www.djangoproject.com/){:target="_blank"}

### Site de Balusc, um dos maiores contribuidores do StackOverflow sobre JSF. Criador do Omie Faces.
1. [http://balusc.omnifaces.org/](http://balusc.omnifaces.org/){:target="_blank"}

### Textos clássicos de Rafael Ponte
1. [http://www.rponte.com.br/2008/07/12/repitam-comigo-redirect-nao-e-forward/](http://www.rponte.com.br/2008/07/12/repitam-comigo-redirect-nao-e-forward/){:target="_blank"}
1. [http://blog.triadworks.com.br/quando-usar-action-ou-actionlistener-com-jsf](http://blog.triadworks.com.br/quando-usar-action-ou-actionlistener-com-jsf){:target="_blank"}
1. [http://www.handersonfrota.com.br/os-10-maus-habitos-do-desenvolvedor-jsf-rafael-ponte/](http://www.handersonfrota.com.br/os-10-maus-habitos-do-desenvolvedor-jsf-rafael-ponte/){:target="_blank"}
1. [http://blog.triadworks.com.br/jsf-nao-coloque-processamento-caro-em-metodos-getters](http://blog.triadworks.com.br/jsf-nao-coloque-processamento-caro-em-metodos-getters){:target="_blank"}
1. [http://blog.triadworks.com.br/quando-usar-action-ou-actionlistener-com-jsf](http://blog.triadworks.com.br/quando-usar-action-ou-actionlistener-com-jsf){:target="_blank"}

### Novidades JSF 2.3
1. [https://arjan-tijms.omnifaces.org/p/jsf-23.html](https://arjan-tijms.omnifaces.org/p/jsf-23.html){:target="_blank"}

### Bootfaces - 
1. [https://www.bootsfaces.net/](https://www.bootsfaces.net/){:target="_blank"}
   



