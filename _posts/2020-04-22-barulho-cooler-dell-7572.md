---
layout: post
title: Resolvendo barulho cooler Dell 15 7572 no Linux Mint 19
date: 22/04/2020
author: Antonio Lazaro
summary: Resolvendo barulho cooler Dell 15 7572 no Linux Mint 19
categories: [linux]
thumbnail: heart
---

## Introdução

Esse mês, vinha sofrendo com um barulho muito forte vindo do cooler no meu notebook. Mesmo em cenários onde apenas o browser estava aberto, e sem vídeos processando, ele fazia um barulho muito forte, como se o cooler estivesse sobrecarregado. Entrei no site da Dell e fui em busca de soluções pois na Internet não tinha encontrado nada que fizesse sentido para meu problema.

Diante disso, vi que poderiam ser duas coisas:

- Sujeira tapando ventilaçã do cooler: Para investigar, abri o Notebook (se o seu estiver na garantia, atenção porque isso pode comprometer sua garantia) e internamente estava extremamente limpo. De qualquer sorte, passei um pincel para limpar mais e testei. Barulho continuou.
- Falta de atualização de Bios/Chipset: Problema que vou descrever a solução logo abaixo.

## Resolução do problema: Atualizando BIOS do Notebook Linux sem instalação Windows

No site da Dell, nessa [página](https://www.dell.com/support/home/br/pt/brbsdt1/?app=products){:target="\_blank"}, é possível digitar a etiqueta do produto e ela vai te direcionar para uma página com a marca e modelo do seu equipamento. NO meu caso tenho um Dell Inspiron 15 7572. Na página ele mostra etique da produto, código de serviço expresso, garantia (no meu caso já expirada). Lá é possível também identificar a configuração do seu produto inteira (caso não saiba procurar em seu sistema operacional).

Existe uma aba de diagnósticos que para quem não utiliza Windows, não é aplicável. Então na seção Drivers e Download é possível ver todos Drivers que existem para seu equipamento. No meu caso vi que existia um Driver para BIOS, classificado como Urgente, conforme as figuras abaixo.

![](/static/img/linux/drivers-dell.png)
![](/static/img/linux/driver-bios.png)

Ai começa o problema, a BIOS para ser atualizada, ela precisa ser executada com um programa .exe que não é um executável Linux. Então, como fazer isso?

No caso do Linux Mint, é um distro baseada em Ubuntu/Debian, ela implementa UEFI, que vem de Universal Extensible Firmware Interface ([um pouco mais sobre o tema pode ser lido no link](http://www.rodsbooks.com/linux-uefi/){:target="\_blank"}), então é possível salvar o arquivo executável em um pendrive formatado como FAT para que através do Menu de inicialização do Boot (F12) ao iniciar, o Driver seja instalado. Após a instalação desse driver da BIOS, o barulho não aconteceu ainda e aparentemente o problema está resolvido. [Esse link do suporte da Dell, descreve detalhadamente como fazer esse procedimento](https://www.dell.com/support/article/pt-br/sln171755/atualizar-o-bios-de-dell-em-um-ambiente-de-linux-ou-ubuntu?lang=pt#updatebios2015){:target="\_blank"}.

Os demais Drivers que se encontram para Download (audio,placa de vídeo, etc), acredito eu que sejam atualizados pelos repositórios oficiais dos fabricantes no sistema operacional, e outros aplicativos da Dell que são feitos para Windows não rodam no Windows, porém, para BIOS, esse foi o único caminho que encontrei.

## Conclusão

Importante buscar informações de suporte junto ao fornecedor, porém, em um fórum, tinha lido que a o atendente do suporte da Dell basicamente mandou um usuário instalar Windows para fazer esse procedimento. Então, bastante importante certificar antes de tomar medidas mais drásticas. Qualquer dificuldade ou dúvida, coloquem nos comentários.

## Outras Fontes:

- https://www.dell.com/support/home/br/pt/brbsdt1/Products/?app=drivers
- https://www.dell.com/support/article/pt-br/sln171755/atualizar-o-bios-de-dell-em-um-ambiente-de-linux-ou-ubuntu?lang=pt#updatebios2015
