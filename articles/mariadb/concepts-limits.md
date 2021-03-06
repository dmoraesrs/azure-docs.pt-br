---
title: Limitações-banco de dados do Azure para MariaDB
description: Este artigo descreve as limitações no Banco de Dados do Azure para o MariaDB, como o número de opções de mecanismo de conexão e armazenamento.
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.topic: conceptual
ms.date: 3/9/2020
ms.openlocfilehash: c982181dee34a7eb0715d5e1271ef5ed794f3809
ms.sourcegitcommit: c29b7870f1d478cec6ada67afa0233d483db1181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79296737"
---
# <a name="limitations-in-azure-database-for-mariadb"></a>Limitações no Banco de Dados do Azure para o MariaDB
As seções a seguir descrevem a capacidade, suporte do mecanismo de armazenamento, suporte de privilégio, suporte à instrução de manipulação de dados e limites funcionais no serviço do banco de dados.

## <a name="server-parameters"></a>Parâmetros do Servidor

Os valores mínimo e máximo de vários parâmetros de servidor populares são determinados pelo tipo de preço e vCores. Consulte as tabelas abaixo para obter limites.

### <a name="max_connections"></a>max_connections

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|50|10|50|
|Basic|2|100|10|100|
|Uso Geral|2|300|10|600|
|Uso Geral|4|625|10|1250|
|Uso Geral|8|1250|10|2500|
|Uso Geral|16|2500|10|5\.000|
|Uso Geral|32|5\.000|10|10000|
|Uso Geral|64|10000|10|20000|
|Otimizado para memória|2|600|10|800|
|Otimizado para memória|4|1250|10|2500|
|Otimizado para memória|8|2500|10|5\.000|
|Otimizado para memória|16|5\.000|10|10000|
|Otimizado para memória|32|10000|10|20000|

Quando as conexões excederem o limite, você poderá receber o seguinte erro:
> ERRO 1040 (08004): número excessivo de conexões

> [!IMPORTANT]
> Para obter a melhor experiência, recomendamos que você use um pool de conexões como o ProxySQL para gerenciar conexões com eficiência.

A criação de novas conexões de cliente com o MariaDB leva tempo e, uma vez estabelecida, essas conexões ocupam recursos do banco de dados, mesmo quando ociosas. A maioria dos aplicativos solicita muitas conexões de curta duração, o que aumenta essa situação. O resultado é um número menor de recursos disponíveis para sua carga de trabalho real, levando a um desempenho reduzido. Um pool de conexões que diminui as conexões ociosas e reutiliza as conexões existentes ajudará a evitar isso. Para saber mais sobre como configurar o ProxySQL, visite nossa [postagem no blog](https://techcommunity.microsoft.com/t5/azure-database-for-mysql/load-balance-read-replicas-using-proxysql-in-azure-database-for/ba-p/880042).

## <a name="query_cache_size"></a>query_cache_size

O cache de consulta é desativado por padrão. Para habilitar o cache de consulta, configure o parâmetro `query_cache_type`. 

Examine a [documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#query_cache_size) para saber mais sobre esse parâmetro.

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|Não configurável na camada básica|N/D|N/D|
|Basic|2|Não configurável na camada básica|N/D|N/D|
|Uso Geral|2|0|0|16777216|
|Uso Geral|4|0|0|33554432|
|Uso Geral|8|0|0|67108864|
|Uso Geral|16|0|0|134217728|
|Uso Geral|32|0|0|134217728|
|Uso Geral|64|0|0|134217728|
|Otimizado para memória|2|0|0|33554432|
|Otimizado para memória|4|0|0|67108864|
|Otimizado para memória|8|0|0|134217728|
|Otimizado para memória|16|0|0|134217728|
|Otimizado para memória|32|0|0|134217728|

## <a name="sort_buffer_size"></a>sort_buffer_size

Examine a [documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#sort_buffer_size) para saber mais sobre esse parâmetro.

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|Não configurável na camada básica|N/D|N/D|
|Basic|2|Não configurável na camada básica|N/D|N/D|
|Uso Geral|2|524288|32768|4194304|
|Uso Geral|4|524288|32768|8388608|
|Uso Geral|8|524288|32768|16777216|
|Uso Geral|16|524288|32768|33554432|
|Uso Geral|32|524288|32768|33554432|
|Uso Geral|64|524288|32768|33554432|
|Otimizado para memória|2|524288|32768|8388608|
|Otimizado para memória|4|524288|32768|16777216|
|Otimizado para memória|8|524288|32768|33554432|
|Otimizado para memória|16|524288|32768|33554432|
|Otimizado para memória|32|524288|32768|33554432|

## <a name="join_buffer_size"></a>join_buffer_size

Examine a [documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#join_buffer_size) para saber mais sobre esse parâmetro.

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|Não configurável na camada básica|N/D|N/D|
|Basic|2|Não configurável na camada básica|N/D|N/D|
|Uso Geral|2|262144|128|268435455|
|Uso Geral|4|262144|128|536870912|
|Uso Geral|8|262144|128|1073741824|
|Uso Geral|16|262144|128|2147483648|
|Uso Geral|32|262144|128|4294967295|
|Uso Geral|64|262144|128|4294967295|
|Otimizado para memória|2|262144|128|536870912|
|Otimizado para memória|4|262144|128|1073741824|
|Otimizado para memória|8|262144|128|2147483648|
|Otimizado para memória|16|262144|128|4294967295|
|Otimizado para memória|32|262144|128|4294967295|

## <a name="max_heap_table_size"></a>max_heap_table_size

Examine a [documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#max_heap_table_size) para saber mais sobre esse parâmetro.

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|Não configurável na camada básica|N/D|N/D|
|Basic|2|Não configurável na camada básica|N/D|N/D|
|Uso Geral|2|16777216|16384|268435455|
|Uso Geral|4|16777216|16384|536870912|
|Uso Geral|8|16777216|16384|1073741824|
|Uso Geral|16|16777216|16384|2147483648|
|Uso Geral|32|16777216|16384|4294967295|
|Uso Geral|64|16777216|16384|4294967295|
|Otimizado para memória|2|16777216|16384|536870912|
|Otimizado para memória|4|16777216|16384|1073741824|
|Otimizado para memória|8|16777216|16384|2147483648|
|Otimizado para memória|16|16777216|16384|4294967295|
|Otimizado para memória|32|16777216|16384|4294967295|

## <a name="tmp_table_size"></a>tmp_table_size

Examine a [documentação do MariaDB](https://mariadb.com/kb/en/server-system-variables/#tmp_table_size) para saber mais sobre esse parâmetro.

|**Tipo de preço**|**vCore(s)**|**Valor padrão**|**Valor mínimo**|**Valor máximo**|
|---|---|---|---|---|
|Basic|1|Não configurável na camada básica|N/D|N/D|
|Basic|2|Não configurável na camada básica|N/D|N/D|
|Uso Geral|2|16777216|1024|67108864|
|Uso Geral|4|16777216|1024|134217728|
|Uso Geral|8|16777216|1024|268435456|
|Uso Geral|16|16777216|1024|536870912|
|Uso Geral|32|16777216|1024|1073741824|
|Uso Geral|64|16777216|1024|1073741824|
|Otimizado para memória|2|16777216|1024|134217728|
|Otimizado para memória|4|16777216|1024|268435456|
|Otimizado para memória|8|16777216|1024|536870912|
|Otimizado para memória|16|16777216|1024|1073741824|
|Otimizado para memória|32|16777216|1024|1073741824|

## <a name="storage-engine-support"></a>Suporte do mecanismo de armazenamento

### <a name="supported"></a>Suportado
- [InnoDB](https://mariadb.com/kb/en/library/xtradb-and-innodb/)
- [MEMORY](https://mariadb.com/kb/en/library/memory-storage-engine/)

### <a name="unsupported"></a>Sem suporte
- [MyISAM](https://mariadb.com/kb/en/library/myisam-storage-engine/)
- [BLACKHOLE](https://mariadb.com/kb/en/library/blackhole/)
- [ARCHIVE](https://mariadb.com/kb/en/library/archive/)

## <a name="privilege-support"></a>Suporte de privilégio

### <a name="unsupported"></a>Sem suporte
- Função DBA: muitas configurações e parâmetros do servidor podem inadvertidamente prejudicar o desempenho do servidor ou negar as propriedades ACID do DBMS. Desa forma, para manter a SLA e integridade do serviço em um nível de produto, esse serviço não expõe a função DBA. A conta de usuário padrão, que é construída quando uma nova instância do banco de dados é criada, permite que o usuário execute a maioria das instruções DDL e DML na instância do banco de dados gerenciado.
- Privilégio SUPER: semelhante a privilégio [SUPER](https://mariadb.com/kb/en/library/grant/#global-privileges) também é restrito.
- O desfinamento: requer a criação de privilégios e é restrito. Se estiver importando dados usando um backup, remova os comandos `CREATE DEFINER`manualmente ou usando o comando `--skip-definer` ao executar um mysqldump.

## <a name="data-manipulation-statement-support"></a>Suporte à instrução de manipulação de dados

### <a name="supported"></a>Suportado
- `LOAD DATA INFILE` tem suporte, mas o parâmetro `[LOCAL]` deve ser especificado e direcionado para um caminho UNC (armazenamento do Azure montado por meio do SMB).

### <a name="unsupported"></a>Sem suporte
- `SELECT ... INTO OUTFILE`

## <a name="functional-limitations"></a>Limitações funcionais

### <a name="scale-operations"></a>Operações de dimensionamento
- O dimensionamento dinâmico de e para as camadas de preços básicas não tem suporte no momento.
- Não há suporte para diminuir o tamanho de armazenamento do servidor.

### <a name="server-version-upgrades"></a>Upgrade da versão do servidor
- Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.

### <a name="point-in-time-restore"></a>Restauração pontual
- Ao usar o recurso PITR, o novo servidor é criado com as mesmas configurações nas quais o servidor está baseado.
- Não há suporte para restaurar um servidor eliminado.

### <a name="subscription-management"></a>Gerenciamento de assinaturas
- Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.

### <a name="vnet-service-endpoints"></a>Ponto de extremidade de serviço VNet
- O suporte para ponto de extremidade de serviço de VNet é apenas para servidores de Uso Geral e Otimizados para Memória.

### <a name="storage-size"></a>Tamanho de armazenamento
- Veja os [tipos de preço](concepts-pricing-tiers.md) para os limites de tamanho de armazenamento por tipo de preço.

## <a name="current-known-issues"></a>Problemas frequentes conhecidos
- Instância de servidor MariaDB exibe a versão de servidor incorreto após o estabelecimento de conexão. Para obter a versão correta do mecanismo de instância de servidor, use o comando `select version();`.

## <a name="next-steps"></a>Próximas etapas
- [O que está disponível em cada camada de serviço](concepts-pricing-tiers.md)
- [Versões com suporte de banco de dados MariaDB](concepts-supported-versions.md)
