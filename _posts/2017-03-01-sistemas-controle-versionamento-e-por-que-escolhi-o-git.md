---
published: false
---
## Sistemas de controle de versionamento e por quê escolhi o GIT

O objetivo desse post é explicar o que é um SCM, exemplificar os tipos e apresentar algumas opções com a recomendação de uma que, acredito que seja o atual padrão de mercado.

Quando trabalhamos em um projeto de software, é bastante comum, compartilharmos o códifo-fonte deste com outros desenvolvedores do time. Quando estamos na faculdade, a primeira ferramenta de backup que usamos são HDs, pendrive, e-mails, mas a medida que o projeto cresce e o número de participantes também. Precisamos ter mais controle sobre as modificações. Em alguns momentos precisamos ter diferentes versões do código e gerenciar isso dentro de arquivos ZIP ou diretórios de computador/HD/Pendrive não é uma tarefa sustentável.

Diante desse cenário, temos dentro da Engenharia de Software, a gestão de configuração, é responsável por controlar e acompanhar mudanças (Controle de Mudança), registrar a evolução do projeto (Controle de Versão) e estabelecer a integridade do sistema (Integração Contínua). Normalmente, um software precisa evoluir com mudanças ou incrementos de features e para termos um controle sobre isso, é necessário usarmos uma ferramenta de controle de versionamento. Um Version Control System (VCS) é um software que ajuda a equipe a gerenciar/documentar as mudanças realizadas no código-fonte em um sistema de arquivos específico. Com o uso dessas ferramentas é possível acompanhar o que cada desenvolvedor modificiou, quando ele o fez, gerando um fluxo de trabalho sustentável. Os VCS também são conhecidos como SCM (Source Code Management) tools ou RCS (Revision Control System). Independente da nomenclatura utilizada, vocês podem perceber que tudo gira em torno de gerenciar mudanças no código-fonte do projeto que é o coração do software. Dentre os benefícios do uso de um SCM, é possível esclarecer os seguintes aspectos:

1. Uma documentação histórica de cada versão de arquivo do projeto. Desde a criação, até a exclusão, passando por toda e qualquer modificação. Tudo pode ser registrado na ferramenta.
2. Possibilidade de tornar mais automático criação de bifurcações para os projetos. Quantas vezes você está trabalhando na feature X, quando é necessário modificar ou implementar uma feature Y, mais urgente. Então? O que fazer? O processo de branching é uma seguimentação do ramo principal do projeto. Para unificar o código do projeto, com os diversos branching, existe uma operação chamada merge, que também é provida pela ferramenta. O merge basicamente serve para unificar as mudanças realizadas dentro de um ou mais arquivos, permitindo mudanças concorrentes em estruturas.
3. Rastreabilidade, é possível descobrir quem modificou, e quando. Do ponto de vista de governança, isso é bastante importante, descobrir quem modificou, quando e de que forma. É como se fosse a digital de cada desenvolvedor.

Quando falamos em SCM, podemos dividi-los basicamente em dois grandes tipos. Centralizados e distribuídos. 

### Tipos de ferramentas

1. Modelo centralizado: Nesse modelo, existe um servidor central que serve como repositório das mudanças e todos desenvolvedores consomem e enviam seus arquivos para esse servidor. Podemos fazer a analogia com um servidor FTP.
  - Vantagens dessa abordagem:
    - Modelo mais simples de ser compreendido
    - Permite mais controle dos usuários e acesso ao repositório
    - Simples de iniciar o uso
  - Desvantagens dessa abordagem:
    - O acesso ao servidor é a única forma de compartilhar código.
    - Todo comando precisa de conexão com servidor
    - Branching e merge são mais custosos do ponto de vista de consumo de recurso computacional (exige mais disco, exige mais processamento).  
  - Principais ferramentas do mercado nessa abordagem:
    - CVS (Concurrent Versions System): Um dos primeiros sistemas de controle de versão. Segue fluxo de desenvolvimento baseado em um tronco (trunk) de onde podem surgir desenvolvimentos alternativos (branches ou ramos) e as tags servem para sinalizar versões estáveis. Teve sua importância ao longo do tempo, porém atualmente, **se vai iniciar um projeto não deve avaliar o CVS mesmo que sua opção seja um sistema centralizado.** Naturalmente, o CVS é muito mais lento que o SVN.
    - SVN (Subversion): Aparece no mercado como evolução do CVS e vem com objetivo de resolver varias limitações da ferramenta anterior. Algumas das evoluções que podem ser citadas em relação ao CVS é permitir renomear e mover arquivos, bem como o suporte de commit atômico, suportando rollback em caso de falhas.

2. Modelo distribuído:
  - Vantagens dessa abordagem:
    - Modelo mais simples de ser compreendido
    - Permite mais controle dos usuários e acesso ao repositório
    - Simples de iniciar o uso
  - Desvantagens dessa abordagem:
    - O acesso ao servidor é a única forma de compartilhar código.
    - Todo comando precisa de conexão com servidor
    - Branching e merge são mais custosos do ponto de vista de consumo de recurso computacional (exige mais disco, exige mais processamento).  
  - Principais ferramentas do mercado nessa abordagem:
  - 	GIT (Concurrent Versions System): Um dos primeiros sistemas de controle de versão. Segue fluxo de desenvolvimento baseado em um tronco (trunk) de onde podem surgir desenvolvimentos alternativos (branches ou ramos) e as tags servem para sinalizar versões estáveis. Teve sua importância ao longo do tempo, porém atualmente, **se vai iniciar um projeto não deve avaliar o CVS mesmo que sua opção seja um sistema centralizado.** Naturalmente, o CVS é muito mais lento que o SVN.
  - 	Mercurial (Subversion): Aparece no mercado como evolução do CVS e vem com objetivo de resolver varias limitações da ferramenta anterior. Algumas das evoluções que podem ser citadas em relação ao CVS é permitir renomear e mover arquivos, bem como o suporte de commit atômico, suportando rollback em caso de falhas.

### Conclusão
Diante do apresentado, minha conclusão pessoal sobre ferramentas de versionamentos. Se tiver que usar o modelo centralizado, vá de SVN. Caso não seja obrigado, recomendo fortemente o uso do GIT, como opção, por diversos aspectos:
1. Padrão de mercado
2. Permite que você use poderosos serviços de hosting como o Github (https://github.com/) e o Bitbucket (https://bitbucket.org/) gratuitamente (cada um tem suas limitações e termos para a gratuidade) e baixo custo (repositórios particulares custam abaixo de 10 dólares mês). Isso tudo com backup, sob responsabilidade dessas empresas!
3. Muitos projetos opensource usam o git, e são hospedados no github, isso facilita a imersão.
4. O Google Code, um dos maiores repositórios de projetos open source [migraram para o GIT, hospedando seus projetos no GitHub](https://opensource.googleblog.com/2015/03/farewell-to-google-code.html).
5. Grandes empresas estão usando, como Oracle, Apple, Microsoft:
1. https://github.com/oracle
2. https://github.com/apple
3. https://github.com/Microsoft
4. https://github.com/twitter
5. https://github.com/Netflix
6. https://github.com/facebook
7. https://github.com/Instagram

6. Grandes projetos são gerenciados através dessa ferramenta:
1. https://github.com/torvalds/linux
2. https://github.com/twbs/bootstrap
3. https://github.com/jquery/jquery
4. https://github.com/rails/rails
5. https://github.com/spring-projects


### Materiais auxiliares para aprender a usar o GIT:

#### Tutoriais sobre como iniciar com o GIT:
1. https://try.github.io/levels/1/challenges/1
2. https://www.atlassian.com/git/tutorials
3. https://www.codecademy.com/learn/learn-git
4. https://www.youtube.com/watch?v=HVsySz-h9r4

#### Material mais abrangente com mais recursos:
1. https://git-scm.com/book/en/v2
2. https://www.tutorialspoint.com/git/
3. https://git-scm.com/docs/gittutorial
4. http://www.vogella.com/tutorials/Git/article.html

#### Clientes visuais para o GIT (para quem não quer ficar na linha de comando)
1. https://www.gitkraken.com/ (Linux, Windows e Mac)
2. https://www.sourcetreeapp.com/ (Windows e Mac)
3. https://www.syntevo.com/smartgit/ (Linux, Windows e Mac)

