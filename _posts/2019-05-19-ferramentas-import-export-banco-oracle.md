---
layout:     post
title:      Ferramentas de import e export banco Oracle
date:       19/05/2019
author:     Antonio Lazaro
summary:    C
categories: [banco-relacional,banco-oracle,docker]
thumbnail:  heart

---

## Introdução

O objetivo desse post é apresentar as opções de import e export em um banco de dados Oracle.

A Oracle disponibiliza algumas opções para download da ferramenta Oracle Client que além do SqlPlus (cliente oficial para acessar o banco), traz as ferramentasde backup.

Esses links ajudam a instalar o Oracle client no Windows (no ambiente do trabalhok foi o SO, que precisei usar, mas deve ter equivalência para outros sistemas suportados pelo banco).

* [Link 1](https://o7planning.org/en/11475/installing-oracle-client-on-windows)
* [Link 2](http://www.catgovind.com/oracle/{:target="_blank"}oracle-how-to-install-oracle-11g-database-client-in-windows-10/){:target="_blank"}
* [Link para download Oracle 11.2](https://www.oracle.com/technetwork/database/enterprise-edition/downloads/112010-win32soft-098987.html){:target="_blank"}
* [Link para download Oracle 12C](https://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-win64-download-2297732.html){:target="_blank"}
* [Link para download Oracle 18c](https://www.oracle.com/technetwork/database/enterprise-edition/downloads/oracle18c-windows-180000-5066774.html){:target="_blank"}
* [Link para download Oracle client com orientações](https://www.oracle.com/technetwork/topics/winx64soft-089540.html){:target="_blank"}

## Opções de backup imp/exp x impdb/expdp

Uma vez que o client esteja instalado e configurado corretamente, existem dois caminhos para fazer import/export de dados no Oracle. As ferramentas imp/exp e impdp e expdp. As segundas, são mais recentes e só constam desde a versão 10G. 
Dados exportados/importados com imp/exp não funcionam com impdp e expdp. 

Para usar o banco Oracle via terminal, é necessário na instalação do client definir um arquivo de configuração chamado TNSNAMEs. Através dele, que o banco conhecerá os dados de conexão.

Exemplo:
```bash
DATABASE_1 =
  (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = 10.10.0.1)(PORT = 1521))
    (CONNECT_DATA = (SERVICE_NAME = SERVICE_NAME_DB_1)))

DATABASE_2 =
  (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = 10.10.0.2)(PORT = 1521))
    (CONNECT_DATA = (SERVICE_NAME = SERVICE_NAME_DB_2)))
```

Os comandos impdp/expdp são mais avançados e tem recursos interessantes, como por exemplo, buscar exportar os dados para uma tabela e importar para uma tabela com nome diferente. No imp/exp isso não acontece e é necessário renomear tabela para "driblar esse recurso".

Nesse processo de descoberta, achei [esse post](https://oracle-base.com/articles/10g/oracle-data-pump-10g#TableExpImp){:target="_blank"} que explicava muito bem sobre expdp e impdp.

Como não tive a oportunidade de testar impdb/expdb por limitação de acesso no banco que estava trabalhando, tive que resolver usando imp/exp.

No meu contexto, não podia sobrescrever os dados importados, eu precisava manter os dados do banco de origem em uma estrutura separada dos dados do banco destino. Com a opção impdb e expdb, existem o recurso de mapping, porém na opção imp/exp não encontrei mecanismo similar.

## Rotina usando imp/exp

O processo de export de dados se mostrou um tanto lento, mas no meu caso acessava o ambiente via VPN, via internet, o que influenciou bastante na performance. Abaixo, explico o comando de export.

1) Exportação do dado do banco de origem
```
exp NOME_BANCO_ORIGEM/SENHA_BANCO_ORIGEM@ENTRADA_TNSNAME_BANCO_ORIGEM TABLES=(MUNICIPIO,USUARIO) GRANTS=N ROWS=Y file=nome_arquivo_gerado.dmp log=nome_arquivo_log.log
```
Essa rotina gerará o arquivo nome_arquivo_gerado.dmp com log nome_arquivo_log.log na pasta onde o client está instalado. 

2) Uma vez que o arquivo de dump está disponível, conecto no banco destino e renomeio as tabelas para preservar os dados. 

```sql
ALTER TABLE NOME_BANCO_DESTINO.MUNICIPIO RENAME TO NOME_BANCO_DESTINO.TMP_MUNICIPIO;
ALTER TABLE NOME_BANCO_DESTINO.USUARIO RENAME TO NOME_BANCO_DESTINO.TMP_USUARIO;
```

3) No banco destino executo o comando de import.

```bash
imp NOME_BANCO_DESTINO/SENHA_BANCO_DESTINO@ENTRADA_TNSNAME_BANCO_DESTINO TABLES=(MUNICIPIO,USUARIO)  file=nome_arquivo_gerado.dmp log=nome_arquivo_log_input_dados.log
```

4) Com o processo anterior, os dados foram importados. Entretanto, eu preciso ainda acessar as informações originais e manter os dados convivendo.

```sql
ALTER TABLE NOME_BANCO_DESTINO.MUNICIPIO RENAME TO NOME_BANCO_DESTINO.T2_MUNICIPIO;
ALTER TABLE NOME_BANCO_DESTINO.USUARIO RENAME TO NOME_BANCO_DESTINO.T2_USUARIO;
ALTER TABLE NOME_BANCO_DESTINO.TMP_MUNICIPIO RENAME TO NOME_BANCO_DESTINO.MUNICIPIO;
ALTER TABLE NOME_BANCO_DESTINO.TMP_USUARIO RENAME TO NOME_BANCO_DESTINO.USUARIO;
```

## Conclusão

Interessante a forma como cada banco trabalha com mecanismo de importação de dados. Essa opção se mostrou muito mais rápida do que exportar os dados da tabela em inserts e realizar outros inserts, por se tratar da criação de um arquivo binário. 

No meu caso isso foi aplicado a um contexto de migração, com algumas transformações de dados.

Vocês já tiveram experiência similares com banco de dados? Compartilhe um pouco como foi nos comentários e vamos tentar compartilhar formas melhor de trabalho.

Para quem não tem banco Oracle configurado, existe esse artigo de [como instalar um banco Oracle 12C no docker](https://www.oracle.com/technetwork/pt/articles/database-performance/oracle-db12-2-no-docker-4427706-ptb.html){:target="_blank"}.

## Outras Fontes
1. [Documentação Oracle sobre transporte de dados](https://docs.oracle.com/database/121/ADMIN/transport.htm#ADMIN11397){:target="_blank"}
1. [Tabela de erros](https://docs.oracle.com/database/121/ERRMG/UDI-00001.htm#ERRMG-GUID-1D460B47-3D90-4FE9-A9B8-7C8FF74E2B4B){:target="_blank"}
1. [Artigo que apresenta recursos](https://oracle-base.com/articles/10g/oracle-data-pump-10g#TableExpImp){:target="_blank"}
   



