---
layout: post
title: Aprendizado K8s - Componentes do Kubernetes
date: 06/12/2022
author: Antonio Lazaro
summary: Aprendizado K8s - Componentes do Kubernetes
categories: [k8, devops]
thumbnail: heart
---

## Nota de aprendizado

O objetivo dessa série é ser uma nota pessoal de conceitos e aprendizados um exercicio de escrita baseado em pesquisas. Com isso, não considero como verdade absoluta nenhuma das anotações, e uma parte significativa são informações extraídas da documentação oficial da ferramenta ou de outros links com as devidas referências.

![](/static/img/k8/k8-icon.png)

## Componentes do Kubernetes

A primeira estrutura existente no Kubernetes (K8s) é o cluster. Por definição, o cluster é __um conjunto de servidores de processamento (chamados nós), que executam aplicações containerizadas. Todos cluster, possui pelo menos um servidor de processamento (worker node).__

O servidor de processamento hospedas os Pods que são componentes de uma aplicação. Os Pods, é o menor e mais simples objeto K8s. Um Pod representa um conjunto de container em execução no cluster. 

O ambiente de gerenciamento, gerencia os nós de processamento e os Pods de um cluster. Em ambientes de produção, o ambiente de gerenciamento geralmente executa em múltiplos computadores e um cluster geralmente executa em múltiplos nós (nodes), provendo tolerância a falhas e alta disponibilidade.

O diagrama abaixo apresenta um cluster K8s com todos seus componentes interligados.

![](/static/img/k8/components-of-kubernetes.svg)

## Componentes da camada de gerenciamento

Os componentes da camada de gerenciamento tomam decisões globais sobre o cluster (exemplo: agendamento de pods), bem como detectam e respondem aos eventos do cluster. Esses componentes podem ser executados em qualquer máquina do cluster, contudo, os scripts, com objetivo de simplificar, normalmente iniciam os componentes dessa camada na mesma máquina e não executa containeres de usuários nesta máquina.

Nas próximas seções serão descritos os componentes existentes.

### kube-apiserver

O servidor de API expõe a API do K8s. Esse componente foi projetado para ser escalonado horizontalmente, com isso é possível executar várias instâncias do kube-apiserver e balancer o tráfego entre essas instâncias através de um load balancer.

A documentação traz uma [seção que aborda especificamente a API do K8s.](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){:target="\_blank"}

#### Escalabilidade horizontal x vertical

A figura abaixo explica a diferença entre escalabilidade vertical e horizontal.

![](/static/img/k8/escalabilidade-Vertical-x-Escalabilidade-Horizontal.-Adaptado-de-MARQUESONE-2017.png)

### etcd

Repositório consistente e de alta-disponibilidade que armazena dados no formato chave-valor (Map) como apoio para o K8s.
As aplicações leem dados do etcd e gravam dados nele. Por sua vez, ele distribui os dados de configuração, fornecendo redundância e resiliência para os nós de configuração.

Importante definir uma política de backups para os dados armazenados nessa estrutra.

### kube-scheduler

Componente que observa os Pods recém-cridos sem nenhum nó atribuído e seleciona um nó (máquina de trabalho dentro de um cluster) para executa-los.
O agendador determina quais nós são posicionamentos válidos para cada Pod na fila de agendamento de acordo 
com as restrições e recursos disponíveis. O agendador então classifica cada nós válido e vincula o Pod a um nó adequado. Vários agendadores diferentes podem ser usados em um cluster; kube-scheduler é a implementação de referência.

### kube-controller-manager

Componente da camada de gerenciamento que executa os processos de controlador.

Logicamente, cada controlador está em um processo separado, mas para reduzir a complexidade, eles todos são compilados num único binário e executam em um processo único.

Alguns tipos desses controladores são:

- *Controlador de nó:* responsável por perceber e responder quando os nós caem.
- *Controlador de Job:* Observa os objetos Job que representam tarefas únicas e, em seguida, cria pods para executar essas tarefas até a conclusão.
- *Controlador de endpoints:* preenche o objeto Endpoints (ou seja, junta os Serviços e os pods).
- *Controladores de conta de serviço e de token:* crie contas padrão e tokens de acesso de API para novos namespaces.

### cloud-controller-manager

Um componente da camada de gerenciamento do Kubernetes que incorpora a lógica de controle específica da nuvem. 
O gerenciador de controle de nuvem permite que você vincule seu cluster na API do seu provedor de nuvem, e separar os componentes que interagem com essa plataforma de nuvem a partir de componentes que apenas interagem com seu cluster.
O cloud-controller-manager executa apenas controladores que são específicos para seu provedor de nuvem. Se você estiver executando o Kubernetes em suas próprias instalações ou em um ambiente de aprendizagem dentro de seu próprio PC, o cluster não possui um gerenciador de controlador de nuvem.

Tal como acontece com o kube-controller-manager, o cloud-controller-manager combina vários ciclos de controle logicamente independentes em um binário único que você executa como um processo único. Você pode escalar horizontalmente (executar mais de uma cópia) para melhorar o desempenho ou para auxiliar na tolerância a falhas.

Os seguintes controladores podem ter dependências de provedor de nuvem:

- *Controlador de nó:* para verificar junto ao provedor de nuvem para determinar se um nó foi excluído da nuvem após parar de responder.
- *Controlador de rota:* para configurar rotas na infraestrutura de nuvem subjacente.
- *Controlador de serviço:* Para criar, atualizar e excluir balanceadores de carga do provedor de nuvem.

## Componentes de Nós

Os componentes de nó são executados em todos os nós, mantendo os pods em execução e fornecendo o ambiente de execução do Kubernetes.

### kubelet
Um agente que é executado em cada node no cluster. Ele garante que os contêineres estejam sendo executados em um Pod.

O kubelet utiliza um conjunto de PodSpecs que são fornecidos por vários mecanismos e garante que os contêineres descritos nesses PodSpecs estejam funcionando corretamente. O kubelet não gerencia contêineres que não foram criados pelo Kubernetes.

### kube-proxy
kube-proxy é um proxy de rede executado em cada nó no seu cluster, implementando parte do conceito de serviço do Kubernetes.

kube-proxy mantém regras de rede nos nós. Estas regras de rede permitem a comunicação de rede com seus pods a partir de sessões de rede dentro ou fora de seu cluster.

kube-proxy usa a camada de filtragem de pacotes do sistema operacional se houver uma e estiver disponível. Caso contrário, o kube-proxy encaminha o tráfego ele mesmo.

### Container runtime
O agente de execução (runtime) de contêiner é o software responsável por executar os contêineres.

O Kubernetes suporta diversos agentes de execução de contêineres: Docker, containerd, CRI-O, e qualquer implementação do Kubernetes CRI (Container Runtime Interface).

#### CRI (Container Runtime Interface)

[Doc](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md){:target="\_blank"}

## Addons

São complementos que usam recursos do K8s para implementar funcionalidades do cluster. Precisam ser criados dentro de um namespace que pertencem ao namespace kube-system.

Alguns exemplos:

Mais sobre addons pode ser visto nesse [link.](https://kubernetes.io/docs/concepts/cluster-administration/addons/){:target="\_blank"}

### DNS
Embora os outros complementos não sejam estritamente necessários, todos os clusters do Kubernetes devem ter um DNS do cluster, já que muitos exemplos dependem disso.

O DNS do cluster é um servidor DNS, além de outros servidores DNS em seu ambiente, que fornece registros DNS para serviços do Kubernetes.

Os contêineres iniciados pelo Kubernetes incluem automaticamente esse servidor DNS em suas pesquisas DNS.

### Web UI (Dashboard)
Interface de usuário Web, de uso geral, para clusters do Kubernetes. Ele permite que os usuários gerenciem e solucionem problemas de aplicações em execução no cluster, bem como o próprio cluster.

### Monitoramento de recursos do contêiner
Esse registra métricas de série temporal genéricas sobre os contêineres em um banco de dados central e fornece uma interface de usuário para navegar por esses dados.

### Logging a nivel do cluster 
Um mecanismo de logging a nível do cluster é responsável por guardar os logs dos contêineres em um armazenamento central de logs com um interface para navegação/pesquisa.

## Conclusão

Próximo post a idéia é estudar um pouco mais sobre a arquitetura do K8s, seguindo o fluxo sugerido pela documentação oficial.

## Fontes

- https://kubernetes.io/pt-br/docs/concepts/overview/components/
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/
- https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/
- https://www.redhat.com/pt-br/topics/containers/what-is-etcd
- https://etcd.io/docs/
- https://kubernetes.io/docs/concepts/cluster-administration/addons/