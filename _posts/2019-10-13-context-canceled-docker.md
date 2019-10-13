---
layout:     post
title:      Docker ERRO[0000] - Context canceled
date:       13/10/2019
author:     Antonio Lazaro
summary:    Docker ERRO[0000] - Context canceled
categories: [docker,container,devops]
thumbnail:  heart

---

## Problema

Passei por um erro ao tentar subir um container e não sabia como resolver. Ao rodar o comando {% highlight shell %} docker run -p *"5432:5432" consilium-db:1.0{% endhighlight %} no diretório que tinha o DockerFile, acontecia o erro: {% highlight shell %}docker: Error response from daemon: no status provided on response: unknown.
ERRO[0000] error waiting for container: context canceled*{% endhighlight %}

## Solução

No meu caso, não sei por qual motivo, o docker daemon, não estava rodando. E tive que reiniciar processo. O docker daemon é o processo docker que roda em background que espera os comandos docker para executar. No Linux Mint é possível reiniciar o daemon com o comando: {% highlight shell %}service docker restart {% endhighlight %}.

Após isso, o daemon está ativo e no meu caso o erro não aconteceu mais. Caso reiniciar pela linha de comando, talvez, reiniciar o sistema operacional recarregue o daemon corretamente. Em alguns casos, alguma atualização do SO ou do docker pode ter comprometido o funcionamento correto.

### Outras Fontes:

1. https://docs.docker.com/config/daemon/
1. https://docs.docker.com/engine/docker-overview/