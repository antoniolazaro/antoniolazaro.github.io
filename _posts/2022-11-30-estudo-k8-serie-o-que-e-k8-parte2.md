---
layout: post
title: Aprendizado K8s - O que é Kubernetes?
date: 30/11/2022
author: Antonio Lazaro
summary: Aprendizado K8s - O que é Kubernetes?
categories: [k8, devops]
thumbnail: heart
---

## Nota de aprendizado

O objetivo dessa série é ser uma nota pessoal de conceitos e aprendizados um exercicio de escrita baseado em pesquisas. Com isso, não considero como verdade absoluta nenhuma das anotações, e uma parte significativa são informações extraídas da documentação oficial da ferramenta ou de outros links com as devidas referências.

![](/static/img/k8/k8-icon.png)
## Introdução

De maneira muito direta e objetiva a definição conceitual de Kubernetes, e segundo a definição da sua própria documentação é "__uma plataforma portátil, extensível e de código aberto para gerenciamento de cargas de trabalho e serviços em contêineres, que facilita a configuração declarativa e a automação. Possui um ecossistema grande e em rápido crescimento. Os serviços, suporte e ferramentas do Kubernetes estão amplamente disponíveis.__".

O nome Kubernetes tem origem grega e significa timoneiro ou piloto, devido a isso, podemos entender o simbolo da plataforma. K8s é um short name para tecnologia que vem da contagem de 8 letras entre o "K" e o "s". 

O Google foi responsável por construir essa tecnologia e abriu o código-fonte da mesma em 2014. Ele combina mais de 154 anos de experiência do Google usando cargas de trabalho em larga escala com as melhores ideias e práticas da comunidade.

Para conhecer mais sobre o projeto é possível conhecer [sua extensa documentação](https://kubernetes.io/docs/concepts/overview/){:target="\_blank"}, bem como ter acesso ao seu [código-fonte](https://github.com/kubernetes/kubernetes){:target="\_blank"}.

Tecnicamente não há como falar de Kubernetes sem explicar o conceito de containers e prioritariamente precisamos falar de Docker para conversamos sobre containers, embora hoje o Kubernetes tenha suporte a outras ferramentas de containers, por isso motivos o [post anterior abordou esses temas requisitos para entendimento.]({% link _posts/2022-11-27-estudo-k8-serie-o-que-e-k8-parte1.md %}){:target="\_blank"}

Para falarmos de K8s, precisamos entender como processo de deploy na infraestrutura foi mudando ao longo do tempo.

![](/static/img/k8/container_evolution.svg)

Podemos dividir em 3 grandes eras o processo de deploy:

- __Deploy tradicional:__ Aplicações executadas em servidores físicos.
    - __Problemas:__ 
        - Para não gerar ociosidade de recursos mais de uma aplicação compartilhava o ambiente, com isso, quando uma aplicação era sobrecarregada, outras sofriam por algo que era fora de seu escopo.
        - Cada servidor tinha um custo, e isso inviabiliza projetos que não tinha uma importância grande, sistemas menores, que otimizavam processos internos as vezes não eram viáveis devido a custo de infraestrutura, mesmo trazendo benefícios operacionais.
    - __Dores principais:__ Custo, escalabilidade, segregação de ambientes de aplicações diferentes.

- __Deploy virtualizado:__ Várias máquinas virtuais em um mesmo servidor físico, porém com esse recurso é possível isolar aplicações criando VMs distintas. Aumenta nível de segurança, pois não há compartilhamento de informações entre as VMs. Também é possível otimizar a utilização  de recursos, gerando redução de custos. Possibilidade de customizações especificas por VM, sem interferência em outros ambientes. Flexibilidade (possibilidade de cada VM ter seu próprio SO e dependências e componentes instalados e configurados).

- __Deploy em containeres:__ Nível atual. Tem uma melhor capacidade de isolamento que as VMs. São mais leves, pois compartilham sistema operacional. São portáveis entre provedores cloud e SOs distintos.
    - Benefícios adicionais:
        - __Criação e implantação ágil de aplicações:__ Aumento da facilidade e eficiência na criação de imagem de contêiner comparado ao uso de imagem de VM.
        - __Desenvolvimento, integração e implantação contínuos:__ Fornece capacidade de criação e de implantação de imagens de contêiner de forma confiável e frequente, com a funcionalidade de efetuar reversões rápidas e eficientes (devido à imutabilidade da imagem).
        - __Separação de interesses entre Desenvolvimento e Operações:__ Crie imagens de contêineres de aplicações no momento de construção/liberação em vez de no momento de implantação, desacoplando as aplicações da infraestrutura.
        - __Capacidade de observação (Observabilidade)__: Não apenas apresenta informações e métricas no nível do sistema operacional, mas também a integridade da aplicação e outros sinais.
        - __Consistência ambiental entre desenvolvimento, teste e produção:__ funciona da mesma forma em um laptop e na nuvem.
        - __Portabilidade de distribuição de nuvem e sistema operacional:__ Executa no Ubuntu, RHEL, CoreOS, localmente, nas principais nuvens públicas e em qualquer outro lugar.
        - __Gerenciamento centrado em aplicações:__ Eleva o nível de abstração da execução em um sistema operacional em hardware virtualizado à execução de uma aplicação em um sistema operacional usando recursos lógicos.
        - __Microserviços fracamente acoplados, distribuídos, elásticos e livres:__ As aplicações são divididas em partes menores e independentes e podem ser implantados e gerenciados dinamicamente - não uma pilha monolítica em execução em uma grande máquina de propósito único.
        - __Isolamento de recursos:__ Desempenho previsível de aplicações.
        - __Utilização de recursos:__ Alta eficiência e densidade.
    
Diante disso, precisamos entender onde o K8s entra na era dos deploy em containeres. Imagine um ambiente de produção, onde um containeres esteja inativo ou teve alguma queda. É necessário que alguém reative ou suba esse servidor. Então, esse alguém é o que o K8s se propõe a resolver.

Características do K8s no gerenciamento de containeres:

- __Descoberta de serviço e balanceamento de carga:__ O Kubernetes pode expor um contêiner usando o nome DNS ou seu próprio endereço IP. Se o tráfego para um contêiner for alto, o Kubernetes pode balancear a carga e distribuir o tráfego de rede para que a implantação seja estável.
- __Orquestração de armazenamento:__ O Kubernetes permite que você monte automaticamente um sistema de armazenamento de sua escolha, como armazenamentos locais, provedores de nuvem pública e muito mais.
- __Lançamentos e reversões automatizadas:__ Você pode descrever o estado desejado para seus contêineres implantados usando o Kubernetes, e ele pode alterar o estado real para o estado desejado em um ritmo controlada. Por exemplo, você pode automatizar o - Kubernetes para criar novos contêineres para sua implantação, remover os contêineres existentes e adotar todos os seus recursos para o novo contêiner.
- __Empacotamento binário automático:__ Você fornece ao Kubernetes um cluster de nós que pode ser usado para executar tarefas nos contêineres. Você informa ao Kubernetes de quanta CPU e memória (RAM) cada contêiner precisa. O Kubernetes pode encaixar contêineres em seus nós para fazer o melhor uso de seus recursos.
- __Autocorreção:__ O Kubernetes reinicia os contêineres que falham, substitui os contêineres, elimina os contêineres que não respondem à verificação de integridade definida pelo usuário e não os anuncia aos clientes até que estejam prontos para servir.
- __Gerenciamento de configuração e de segredos:__ O Kubernetes permite armazenar e gerenciar informações confidenciais, como senhas, tokens OAuth e chaves SSH. Você pode implantar e atualizar segredos e configuração de aplicações sem reconstruir suas imagens de contêiner e sem expor segredos em sua pilha de configuração.

Entretanto, é importante termos claro qual missão do K8s e existe uma restrição de escopo de atuação na ferramenta. Com isso, é importante explicar que o K8 é não é um PAAS (Platform as a service). O K8s fornece recursos de PAAS, porém, ele não é monolítico, e outras soluções podem ser conectadas para se construir uma plataforma de desenvolvimento.

Dito isso, temos como características do K8s:

- Se uma aplicação puder ser executada em um container, deve ser executada perfeitamente no K8s. Não é função do K8s, limitar os tipos de aplicações suportadas.
- Não suporta implantação de código-fonte, e nem constroi aplicação. Isso deve ser feito dentro do processo ou pipeline de cada projeto, gerando imagens de containers como artefato final.
- Não funciona como middleware de aplicação (barramento de msg, banco de dados, cache,etc). Esses componentes podem ser executados no K8s.
- Não define soluções de logging, monitoramento e alerta. Varias ferramentas podem ser acopladas.
- Não fornece nem adota sistemas de configuração de máquinas como vagrant ou chef;
- Adicionalmente, o Kubernetes não é um mero sistema de orquestração. Na verdade, ele elimina a necessidade de orquestração. A definição técnica de orquestração é a execução de um fluxo de trabalho definido: primeiro faça A, depois B e depois C. Em contraste, o Kubernetes compreende um conjunto de processos de controle independentes e combináveis que conduzem continuamente o estado atual em direção ao estado desejado fornecido. Não importa como você vai de A para C. O controle centralizado também não é necessário. Isso resulta em um sistema que é mais fácil de usar e mais poderoso, robusto, resiliente e extensível.

No próximo [post]({% link _posts/2022-11-30-estudo-k8-serie-o-que-e-k8-parte3.md %}), entraremos mais na apresentação da estrutura de componentes do K8s.

## Fontes

- https://kubernetes.io/pt-br/docs/concepts/overview/what-is-kubernetes/ 
- https://www.alura.com.br/artigos/o-que-e-kubernetes
- 