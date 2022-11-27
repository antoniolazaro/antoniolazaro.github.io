---
layout: post
title: Aprendizado K8s - Containeres e Docker?
date: 27/11/2022
author: Antonio Lazaro
summary: Aprendizado K8s - Containeres e Docker?
categories: [k8, devops]
thumbnail: heart
---

![](/static/img/k8/docker.webp)


## Introdução

De maneira muito direta e objetiva a definição conceitual de Kubernetes, e segundo a definição da sua própria documentação é "__uma plataforma portátil, extensível e de código aberto para gerenciamento de cargas de trabalho e serviços em contêineres, que facilita a configuração declarativa e a automação. Possui um ecossistema grande e em rápido crescimento. Os serviços, suporte e ferramentas do Kubernetes estão amplamente disponíveis.__".

O nome Kubernetes tem origem grega e significa timoneiro ou piloto, devido a isso, podemos entender o simbolo da plataforma. K8s é um short name para tecnologia que vem da contagem de 8 letras entre o "K" e o "s". 

O Google foi responsável por construir essa tecnologia e abriu o código-fonte da mesma em 2014. Ele combina mais de 154 anos de experiência do Google usando cargas de trabalho em larga escala com as melhores ideias e práticas da comunidade.

Para conhecer mais sobre o projeto é possível conhecer [sua extensa documentação](https://kubernetes.io/docs/concepts/overview/){:target="\_blank"}, bem como ter acesso ao seu [código-fonte](https://github.com/kubernetes/kubernetes){:target="\_blank"}.

Tecnicamente não há como falar de Kubernetes sem explicar o conceito de containers e prioritariamente precisamos falar de Docker para conversamos sobre containers, embora hoje o Kubernetes tenha suporte a outras ferramentas de containers.

### Containers e Docker

#### Containers

Para a Red Hat, um Conteiner Linux é um conjunto de 1 ou mais processos isolados do restante do sistema. Os arquivos necessários para execução de um container são providos a partir de uma imagem, o que significa que eles são portáteis e consistentes. Devido a natureza da atividade de construção de software, bem como necessidade de equalização entre ambientes segregados (desenvolvimento, homologação, produção) foi necessário a utilização de tecnologia e uso de ferramentas que conseguissem prover portabilidade, consistência e velocidade, com o advento da computação em nuvens e também impulsionado pela larga utilização das arquiteturas distribuídas, bem comum atualmente.

#### Por que precisamos de containeres?

Resposta extraída da documentação da Red Hat: "_Imagine que você está desenvolvendo um aplicativo. Você faz seu trabalho em um laptop e seu ambiente tem uma configuração específica. Outros desenvolvedores podem ter configurações ligeiramente diferentes. O aplicativo que você está desenvolvendo depende dessa configuração e depende de bibliotecas, dependências e arquivos específicos. Enquanto isso, sua empresa possui ambientes de desenvolvimento e produção padronizados com suas próprias configurações e seus próprios conjuntos de arquivos de suporte. Você deseja emular esses ambientes tanto quanto possível localmente, mas sem toda a sobrecarga de recriar os ambientes de servidor. Então, como você faz seu aplicativo funcionar nesses ambientes, passa na garantia de qualidade e implementa seu aplicativo sem grandes dores de cabeça, reescrevendo e corrigindo falhas? A resposta: contêineres_"

A imagem abaixo, ilustra o funcionamento de um container. Nesse container, já existem as bibliotecas, dependências e arquivos necessários para que a aplicação seja executada sem necessidade novas intervenções. De maneira resumida, ela possui uma versão do microkernel do linux.

![](/static/img/k8/what-is-a-container.png)

#### Qual diferença entre container e virtualização?

Mas containers então seriam máquinas virtuais? Não, tecnicamente. Inclusive, você pode criar containers dentro de máquinas virtuais que rodam em um sistema operacional hospedeiro. Mas, trazendo a definição da Red Hat sobre a diferença, segue abaixo:

- A virtualização permite que seus sistemas operacionais (Windows ou Linux) sejam executados simultaneamente em um único sistema de hardware.
- Os contêineres compartilham o mesmo kernel do sistema operacional e isolam os processos de aplicativos do resto do sistema. Por exemplo: sistemas ARM Linux executam contêineres ARM Linux, sistemas x86 Linux executam contêineres x86 Linux, sistemas x86 Windows executam contêineres x86 Windows. Os contêineres do Linux são extremamente portáteis, mas devem ser compatíveis com o sistema subjacente.

![](/static/img/k8/virtualization-vs-containers.png)

Como o objetivo é introduzir K8, essa explicação é suficiente para definirmos Docker e consequentmente K8s.

### Docker

Em 2008, Docker entrou em cena. A tecnologia Docker adicionou conceitos e ferramentas e uma interface de linha de comando simples para execução e criação de novas imagens em camada, associados a um daemon servidor, uma biblioteca de imagens de containers pré-construídas, e o conceito de um servidor de registros. Através da combinação dessas tecnologias, foi permitido que os usuários construissem rapidamente novos containeres em camadas e os compartilhassem com outras pessoas de maneira fácil e padronizada.

Existem 3 padrões principais para garantir a interoperabilidade das tecnologias de contêiner - as especificações OCI Image, Distribution e Runtime. Combinadas, essas especificações permitem que projetos comunitários, produtos comerciais e provedores de nuvem criem tecnologias de contêiner interoperáveis ​​(pense em enviar suas imagens personalizadas construídas para o servidor de registro de um provedor de nuvem - você precisa disso para funcionar). Hoje, a Red Hat e a Docker, entre muitas outras, são membros da Open Container Initiative (OCI) — estão permitindo uma padronização aberta e industrial de tecnologias de contêiner.

A palavra "Docker" refere-se a várias coisas:
    - Projeto comunitário de código aberto; 
    - Ferramentas do projeto open source; 
    - Docker Inc., a empresa que apóia principalmente esse projeto; 
    - Ferramentas que a empresa suporta formalmente. 
    
O fato de as tecnologias e a empresa compartilharem o mesmo nome pode ser confuso.

Aqui as explicações:
- O software de TI “Docker” é uma tecnologia de conteinerização que permite a criação e uso de containers Linux.
- A comunidade Docker de código aberto trabalha para melhorar essas tecnologias para beneficiar todos os usuários.
- A empresa, Docker Inc., se baseia no trabalho da comunidade Docker, torna-a mais segura e compartilha esses avanços com a comunidade em geral. 
- A Docker Inc. oferece suporte às tecnologias aprimoradas e reforçadas para clientes corporativos.

Com o Docker, você pode tratar contêineres como máquinas virtuais modulares extremamente leves. E você obtém flexibilidade com esses contêineres para criar, implantar, copiar e movêr containeres entre ambientes.

#### Como Docker Funciona?

- A tecnologia Docker usa o kernel Linux e recursos do kernel, como Cgroups e namespaces, para segregar processos para que possam ser executados de forma independente. Essa independência é a intenção dos contêineres - a capacidade de executar vários processos e aplicativos separadamente uns dos outros para fazer melhor uso de sua infraestrutura, mantendo a segurança que você teria com sistemas separados.
- As ferramentas de contêiner, incluindo o Docker, fornecem um modelo de implantação baseado em imagem. Isso facilita o compartilhamento de um aplicativo ou conjunto de serviços com todas as suas dependências em vários ambientes. O Docker também automatiza a implantação do aplicativo (ou conjuntos combinados de processos que compõem um aplicativo) dentro desse ambiente de contêiner.
- Essas ferramentas construídas sobre contêineres do Linux - o que torna o Docker amigável e exclusivo - oferece aos usuários acesso sem precedentes a aplicativos, a capacidade de implantar rapidamente e controlar as versões e a distribuição de versões.

A figura abaixo mostra como funciona a infrestrutura com Docker.

![](/static/img/k8/docker-containerized-appliction-blue-border_2.webp)

#### Arquitetura docker

![](/static/img/k8/Docker-Architecture.png)

#### Docker e containers linux são a mesma coisa?

Embora às vezes confuso, o Docker não é o mesmo que um container Linux tradicional. 
- A tecnologia Docker foi inicialmente construída sobre a tecnologia LXC - que a maioria das pessoas associa aos contêineres "tradicionais" do Linux - embora tenha se afastado dessa dependência. 
- O LXC era útil como virtualização leve, mas não oferecia uma ótima experiência de desenvolvedor ou usuário. 
- A tecnologia Docker oferece mais do que a capacidade de executar contêineres - ela também facilita o processo de criação e construção de contêineres, remessa de imagens e versão de imagens, entre outras coisas.
- Os contêineres Linux tradicionais usam um sistema init que pode gerenciar vários processos. Isso significa que aplicativos inteiros podem ser executados como um só. 
A tecnologia Docker incentiva os aplicativos a serem divididos em seus processos separados e fornece as ferramentas para fazer isso. Essa abordagem granular tem suas vantagens.

#### Quais as vantagens de containeres Docker?

- *Modularidade:* A abordagem do Docker para conteinerização se concentra na capacidade de desativar uma parte de um aplicativo para atualização ou reparo, sem a necessidade de desativar o aplicativo inteiro. Além dessa abordagem baseada em microsserviços, você pode compartilhar processos entre vários aplicativos da mesma forma que a arquitetura orientada a serviços (SOA).

- *Camadas e controle de versão de imagem:* Cada arquivo de imagem do Docker é composto por uma série de camadas que são combinadas em uma única imagem. Uma camada é criada quando a imagem muda. Sempre que um usuário especifica um comando, como executar ou copiar, uma nova camada é criada. 
O Docker reutiliza essas camadas para criar novos contêineres, o que acelera o processo de construção. Alterações intermediárias são compartilhadas entre as imagens, melhorando ainda mais a velocidade, tamanho e eficiência. Também inerente à camada é o controle de versão: toda vez que há uma nova alteração, você basicamente tem um changelog integrado, fornecendo a você controle total sobre suas imagens de contêiner.

- *Suporte a rollback:*: Talvez a melhor parte das camadas seja a capacidade de reverter. Toda imagem tem camadas. Não gosta da iteração atual de uma imagem? Role de volta para a versão anterior. Isso dá suporte a uma abordagem de desenvolvimento ágil e ajuda a tornar a integração e implantação contínuas (CI/CD) uma realidade do ponto de vista das ferramentas.

- *Desenvolvimento rápido*: Colocar um novo hardware em funcionamento, provisionado e disponível costumava levar dias, e o nível de esforço e sobrecarga era oneroso. Os contêineres baseados em Docker podem reduzir a implantação para segundos. Ao criar um contêiner para cada processo, você pode compartilhar rapidamente esses processos com novos aplicativos. E, como um sistema operacional não precisa inicializar para adicionar ou mover um contêiner, os tempos de implantação são substancialmente mais curtos. Em conjunto com tempos de implantação mais curtos, você pode criar e destruir dados criados por seus contêineres de maneira fácil e econômica sem preocupação.

Portanto, a tecnologia Docker é uma abordagem mais granular, controlável e baseada em microsserviços que valoriza mais a eficiência.

#### Quais limitações do docker?

O Docker, por si só, pode gerenciar contêineres individuais. Quando você começa a usar mais e mais contêineres e aplicativos em contêineres, divididos em centenas de partes, o gerenciamento e a orquestração podem ficar difíceis. Eventualmente, você precisa dar um passo para trás e agrupar contêineres para fornecer serviços – rede, segurança, telemetria e muito mais – em todos os seus contêineres. É aí que entra o Kubernetes. Assunto do [próximo post.]({% link _posts/2022-11-27-estudo-k8-serie-o-que-e-k8-parte2.md %}){:target="\_blank"}

#### Onde aprendo mais sobre Docker?

- [Doc oficial do projeto](https://docs.docker.com/){:target="\_blank"}
- https://github.com/gomex/docker-para-desenvolvedores  __Autor BR (Baiano! Soteropolitano!) e atuante na comunidade:__ [Gomex](https://twitter.com/gomex){:target="\_blank"}
- https://livro.descomplicandodocker.com.br/   __Autor BR e atuante na comunidade:__ [Jefferson Fernando - From Linux Tips](https://twitter.com/badtux_){:target="\_blank"}
- [Canal no Youtube Linux Tips](https://www.youtube.com/linuxtips){:target="\_blank"}
- https://www.amazon.com.br/Docker-Running-2nd-Sean-Kane/dp/1492036730{:target="\_blank"}
- https://www.amazon.com/Using-Docker-Developing-Deploying-Containers/dp/1491915765
- https://learn.microsoft.com/pt-br/dotnet/architecture/microservices/container-docker-introduction/docker-defined


## Fontes
- https://www.redhat.com/en/topics/containers/whats-a-linux-container
- https://www.redhat.com/en/topics/containers/what-is-docker