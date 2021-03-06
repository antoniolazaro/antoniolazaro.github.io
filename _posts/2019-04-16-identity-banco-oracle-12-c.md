---
layout:     post
title:      Identity banco Oracle 12C
date:       16/04/2019
author:     Antonio Lazaro
summary:    C
categories: [banco-relacional,banco-oracle,docker]
thumbnail:  heart

---

## Introdução

O objetivo desse post é apresentar o recurso Identity do banco Oracle. 

Esse recurso foi implementado a partir da release 12C entretanto já existia nos bancos <a href="https://dev.mysql.com/doc/refman/8.0/en/example-auto-increment.html">Mysql</a>, <a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-transact-sql-identity-property?view=sql-server-2017">SQL Server e </a> <a href="http://www.postgresqltutorial.com/postgresql-serial/">Postgres.</a>

Com bancos Oracle sempre foi padrão a utilização de sequences ao invés de recursos auto-incremento. 



## Tipos de Identity no Oracle

```sql
GENERATED [ ALWAYS | BY DEFAULT [ ON NULL ] ] AS IDENTITY [ ( identity_options ) ]
```

### Tipos suportados


![](/static/img/oracle-post/identity/identity-clause-oracle.png)

1. ALWAYS: O banco de dados sempre gerará um valor para essa coluna. Inserir um valor manualmente nessa coluna causará um erro.

1. BY DEFAULT: O banco de dados gerará um valor para essa coluna, caso o valor não seja informado. Se o valor for informado, este será aplicado a coluna. Caso tente inserir um valor NULL nessa coluna causará um erro.

1. BY DEFAULT ON NULL: Suporta a sintaxe informando valor, omitindo ou passando NULL.

Para as configurações BY DEFAULT ou BY DEFAULT ON NULL, você deve ter atenção ao valor inserido manualmente porque o incremento não leva em consideração valores inseridos manualmente e estourará erro de constraint unique. Por isso, o recomendado é criar ranges distantes para valores inseridos manualmente. 

### Recursos suportados como identity options

![](/static/img/oracle-post/identity/identity-option-oracle.png)

1. START WITH: Valor inicial do contador. Valor padrão = 1.
1. INCREMENT BY: Valor interno que o contador será incrementado. Valor padrão é = 1.
1. CACHE: Define um número de registros que será usado para fazer cache. Recomendado para volumes altos de inserção.


### Algumas informações complementares

1. Apenas uma coluna IDENTITY pode ser usada por tabela. Se sua tabela precisa de duas colunas, as N próximas devem usar sequences.
1. Somente novas colunas podem ter atributo IDENTITY. Não é possível alterar uma coluna existente para suportar esse recurso. Para essa necessidade, sequences são recomendadas.
1. Em caso de TRUCANTE Table aplicado, o campo retorna para valor definido pela option START WITH.
1. Não há opção de uso de NEXTVAL, como na sequence.
1. É possível usar CURRVAL.
1. O tipo de dado deve ser numérico.
1. Não pode ser definido valor default para esse tipo de coluna.
1. Para esse tipo de coluna, implicitamente já é NOT NULL.
1. ```CREATE TABLE AS SELECT``` não gerará para a tabela filha o comportamento de identity

### Script para teste do recurso

```sql
DROP TABLE accounts;
CREATE TABLE accounts (
    id NUMBER GENERATED ALWAYS AS IDENTITY,
    text NUMBER NOT null,
    PRIMARY KEY(id)
);

INSERT INTO ACCOUNTS(id,text) VALUES (1,1);
--SQL Error [32795] [99999]: ORA-32795: cannot insert into a generated always identity COLUMN

COMMIT;

INSERT INTO ACCOUNTS(text) VALUES (2);
--Updated Rows	1
COMMIT;


INSERT INTO ACCOUNTS(id,text) VALUES (NULL,2);
--SQL Error [32795] [99999]: ORA-32795: cannot insert into a generated always identity COLUMN
COMMIT;

ALTER TABLE ACCOUNTS 
MODIFY ID NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY;

INSERT INTO ACCOUNTS(id,text) VALUES (100,3);
--Updated Rows	1
COMMIT;

INSERT INTO ACCOUNTS(text) VALUES (10);
--Updated Rows	1
COMMIT;

INSERT INTO ACCOUNTS(id,text) VALUES (NULL,5);
--Updated Rows	1
COMMIT;

SELECT * FROM ACCOUNTS;

ALTER TABLE ACCOUNTS 
MODIFY ID NUMBER GENERATED BY DEFAULT AS IDENTITY;

INSERT INTO ACCOUNTS(id,text) VALUES (101,6);
--Updated Rows	1
COMMIT;

INSERT INTO ACCOUNTS(text) VALUES (8);
--Updated Rows	1
COMMIT;

INSERT INTO ACCOUNTS(id,text) VALUES (NULL,9);
--SQL Error [1400] [23000]: ORA-01400: cannot insert NULL into ("PROCESSUM"."ACCOUNTS"."ID")
COMMIT;
```

### Performance

No [site](https://oracle-base.com/articles/12c/identity-columns-in-oracle-12cr1){:target="_blank"}, foi feita uma comparação entre a estratégia de usar Sequence, Trigger e Identity. Nos testes feitos a sequence teve uma performance mais rápida. Porém, *tudo isso, na minha visão, é bem relativo, uma vez que depende de variáveis como concorrência, estratégia/necessidade de cache, dentre outras coisas.*

Resultado benchmark:
1. SEQUENCE_IDENTITY: Time=26 hsecs CPU Time=22 hsecs
2. REAL_IDENTITY    : Time=28 hsecs CPU Time=26 hsecs
3. TRIGGER_IDENTITY : Time=217 hsecs CPU Time=204 hsecs

## Conclusão

Acredito que a Oracle criou o recurso por uma demanda de mercado. Frameworks de persistência demandam por esse tipo de flexibilidade e o esforço de configuração de sequences em alguns contextos demandava mais tempo. É aquela velha máxima, o produto quem demanda é o cliente e o mercado. A Oracle com isso, fornece mais opção para seu produto, agregando valor.

Para quem não tem banco Oracle configurado, existe esse artigo de [como instalar um banco Oracle 12C no docker](https://www.oracle.com/technetwork/pt/articles/database-performance/oracle-db12-2-no-docker-4427706-ptb.html){:target="_blank"}.

## Outras Fontes
1. [Documentação Oracle](https://docs.oracle.com/database/121/SQLRF/statements_7002.htm){:target="_blank"}
1. [http://www.oracletutorial.com/oracle-basics/oracle-identity-column/](http://www.oracletutorial.com/oracle-basics/oracle-identity-column/){:target="_blank"}
1. [https://oracle-base.com/articles/12c/identity-columns-in-oracle-12cr1](https://oracle-base.com/articles/12c/identity-columns-in-oracle-12cr1){:target="_blank"}
   



