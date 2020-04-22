---
layout: post
title: Como ordernar categorias no Jekyll
date: 22/04/2020
author: Antonio Lazaro
summary: Como ordernar categorias no Jekyll
categories: [jekyll, blog]
thumbnail: heart
---

## Introdução

Esse blog é feito com [Jekyll](https://jekyllrb.com/){:target="\_blank"} e esta é uma ferramenta para quem blogs extremamente simples. A proposta dele é ser simples, estático e construido para ser uma ferramenta de blog, um site que tem estrutura composta por páginas, categorias e posts.

Jekkyl é construído em Ruby com [Liquid](https://shopify.github.io/liquid/){:target="\_blank"} como template engine.

Uma vantagem de ter um site em Jekyll é que ele pode ser hospedado gratuitamente no [github pages](https://pages.github.com/){:target="\_blank"}.

Tinha escrito um pouco sobre Jekyll no [post]({% link _posts/2019-10-13-jekyll-highlight-code.md %}){:target="\_blank"}. Nesse mesmo post, falo um pouco sobre criar um site usando Jekyll e como configurar um domínio do Google Domains para o Github Pages, que foi descrito pelo meu amigo
[Mateus Malaquias](https://twitter.com/malaquiasdev){:target="\_blank"}. [Link para o post dele:
post](https://medium.com/trainingcenter/como-configurar-um-dominio-do-google-domains-no-github-pages-87324885bf11){:target="\_blank"}.

## Como ordenar uma categoria usando Jekyll

No blog, existe a seção de categorias que é uma estrutura fornecida pelo Jekyll.
É necessário definir uma variável e definir a ordenação.
Logo em seguida se utiliza essa variável ordenada. Meu código ficou da seguinte forma:

{% highlight liquid %}
assign sortedCategories = site.categories | sort
for category in sortedCategories
{% endhighlight %}

Respeitando a sintaxe do liquid, coloquei apenas o trecho que trata da ordenação.

## Conclusão

Jekyll é uma ferramenta simples e oferece uma forma de trabalho bacana para escrita de blogs. Escolhendo um template e manter um blog é simples e o fato de ser hospedado no Github pages, zera o custo de hospedagem. Se a pessoa quiser, configura um domínio, mas sem um domínio pode usar o próprio fornecedor pelo github = nomeusuario.github.io.

E vocês? Fazem seus sites e blogs com que tecnologia?

## Outras Fontes:

- [Importando blogs de outras ferramentas para Jekyll](https://import.jekyllrb.com/){:target="\_blank"}
- [Temas, plugins e outros recursos Jekyll](https://jekyllrb.com/resources/){:target="\_blank"}
