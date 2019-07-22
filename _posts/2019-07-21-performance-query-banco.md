---
layout:     post
title:      Como analisar performance de consultas nos bancos de dados.
date:       21/07/2019
author:     Antonio Lazaro
summary:    Como analisar performance de consultas nos bancos de dados.
categories: [banco-relacional,banco-oracle]
thumbnail:  heart

---

## Introdução

Esse post fala sobre como podemos utilizar ferramentas para analisar performance de queries em bancos de dados relacionais. Toda consulta feita no banco de dados gera um plano de execução da query. O plano de execução é a sequência de operações que o banco realiza para recuperar o dado. Essa definição pode ser melhor entendida no [post do blog de Fabio Prado](https://www.fabioprado.net/2011/03/analisando-o-plano-de-execucao-para.html){:target="_blank"}.
O objetivo do plano de execução é mostrar como o banco de dados processa a consulta. Importante sempre comparar consultas que foram otimizadas para avaliar o real ganho. Sempre que escrever uma consulta, é interessante que se analise o plano de execução das mesma, pois consultas com plano de execução alto, normalmente com o crescimento natural do banco de dados a tendência é que a performance seja degradada.
Cada SGBD ou até mesmo ferramenta possui uma forma de visualização do plano de execução. A ferramenta que atualmente eu utilizo para banco de dados é o [Dbeaver](https://dbeaver.io/){:target="_blank"}.

## Analisando consultas

Algumas "dicas" que você deve ficar atento no plano de execução da query.
- Queries cujo plano aparece Table Acess (Full), são queries que estão fazendo a leitura da tabela inteira para buscar os dados.
- Usar order by apenas onde é necessário
- Evitar uso de disctinct refinando melhor os dados
- Criação de íncides para colunas que são muito lidas
- Colunas que tem muita escrita/atualização deve ser evitada como índice
- Colunas que são referenciadas em condições de busca são candidatas a índice

No exemplo que me inspirou a construir esse post tive uma redução de ordem de mais de 10x na performance. AQ query tinha custo 323 para 172. Esse número eu não sei informar qual a grandeza dele, porém, um amigo, me sinalizou que quanto mais próximo de 1000, mais cara sua query está para o banco, então hoje me guio por isso.

Query antes da otimização:
![](/static/img/otimizacao/otimizacao1.png)

Query após a otimização
![](/static/img/otimizacao/otimizacao2.png)

## Conclusão

Otimização é sempre um tema que só pensamos quando temos problemas. Podemos pensar de maneira preventiva com um esforço inicial mais elaborado, muitas vezes não valorizamos os recursos que temos e geramos problemas sem necessidade.

## Fontes usadas

- [Post 1](https://medium.com/alexandre-malavasi/25-dicas-e-boas-pr%C3%A1ticas-de-banco-de-dados-para-desenvolvedores-7a60bfc28f1f){:target="_blank"}
- [Post 2](https://www.devmedia.com.br/entendendo-e-usando-indices-parte-1/6567){:target="_blank"}
- [Post 3](https://imasters.com.br/banco-de-dados/8-dicas-para-criar-indices-mais-eficientes){:target="_blank"}