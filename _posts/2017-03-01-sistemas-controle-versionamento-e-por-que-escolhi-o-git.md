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
    * Exceto o pull inicial, eles são muito mais rápidos do que os sistemas centralizados como CVS e SVN.
	* Muitas operações não necessitam de acesso à rede, então o desenvolvedor pode trabalhar offline, sincronizando com o repositório remoto apenas quando necessário.
	* O desenvolvedor pode trabalhar em modo privado, gerando tags, branches e versões que serão simplesmente descartadas.
	* Exceto quando há conflitos, o merge é automático.
	* Cada cópia do repositório funciona como um backup do repositório "principal".
  - Desvantagens dessa abordagem:
    - Curva de aprendizado inicial para os desenvolvedores entenderem os conceitos da distribuição do file system.
    - Importante que um fluxo de trabalho seja definido para evitar caos. 
  - Principais ferramentas do mercado nessa abordagem:
  - 	GIT (Concurrent Versions System): Desenvolvido em 2005 por Linus Torvalds com objetivo de facilitar o gerenciamento do kernell do linux que tem milhares de colaboradores espalhados ao redor do mundo.
  - 	Mercurial (Subversion): Tem recursos semelhantes ao GIT. O Bit Bucket hospeda tanto projetos git quanto mercurial.

### Conclusão. Por que usa o Git?

Diante do apresentado, minha conclusão pessoal sobre ferramentas de versionamentos. Se tiver que usar o modelo centralizado, vá de SVN. Caso não seja obrigado, recomendo fortemente o uso do GIT, como opção, por diversos aspectos:

#### Aspectos funcionais:

1. Em quase tudo é executado mais rápido, em alguns casos muito mais rápido por ser otimizado para funcionar pela internet.
2. O repositório ocupa menos espaço.
3. É muito mais fácil administrar diversas fontes de atualizações.
4. É fácil trabalhar com cópias locais para fazer experimentos e desenvolvimentos paralelos. Branches são baratos e simples. São incentivados.
5. Incentiva o commit frequente.
6. Facilita muito fazer merge.
7. Permite trabalhar confortavelmente sem perder nenhuma funcionalidade e informação sem estar conectado ao servidor central (que pode e frequentemente é usado). Ele tem mais metadados locais.
8. Possui mais informações de auditoria e que permitem mais facilidades em toda a administração.
9. Manipula conversão de fim de linha mais facilmente.
10. As revisões são assinadas digitalmente.
12. Possui uma staging area que permite selecionar partes que deseja enviar para um repositório.
13. Permite uma gama maior de fluxos de trabalho.

#### Aspectos não funcionais:

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

## Fontes:
1. https://blog.pronus.io/posts/o-que-eh-gerencia-de-configuracao-de-software/
1. https://www.atlassian.com/git/tutorials/what-is-version-control
1. http://guides.beanstalkapp.com/version-control/intro-to-version-control.html
1. http://pt.stackoverflow.com/questions/8315/diferen%C3%A7as-entre-git-svn-e-cvs 
1. http://www.tecmint.com/best-gui-git-clients-git-repository-viewers-for-linux/
1. https://pt.wikiversity.org/wiki/CVS_x_SVN_x_Git
1. https://biz30.timedoctor.com/git-mecurial-and-cvs-comparison-of-svn-software/
1. https://blog.pronus.io/posts/vantagens-e-desvantagens-do-controle-de-versao-distribuido/


