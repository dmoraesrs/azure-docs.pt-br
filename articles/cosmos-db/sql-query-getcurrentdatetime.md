---
title: GetCurrentDateTime na linguagem de consulta Azure Cosmos DB
description: Saiba mais sobre a função do sistema SQL GetCurrentDateTime no Azure Cosmos DB.
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 09/13/2019
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: d50b08ab85c7e299c465c3eb6f34e867d6634006
ms.sourcegitcommit: f915d8b43a3cefe532062ca7d7dbbf569d2583d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78303895"
---
# <a name="getcurrentdatetime-azure-cosmos-db"></a>GetCurrentDateTime (Azure Cosmos DB)
 Retorna a data e a hora UTC atuais (tempo Universal Coordenado) como uma cadeia de caracteres ISO 8601.
  
## <a name="syntax"></a>Sintaxe
  
```sql
GetCurrentDateTime ()
```
  
## <a name="return-types"></a>Tipos de retorno
  
  Retorna o valor da cadeia de caracteres UTC 8601 atual de data e hora no formato `YYYY-MM-DDThh:mm:ss.fffffffZ` em que:
  
  |||
  |-|-|
  |AAAA|ano de quatro dígitos|
  |MM|mês de dois dígitos (01 = Janeiro, etc.)|
  |DD|dia de dois dígitos do mês (01 a 31)|
  |T|signifier para o início dos elementos de hora|
  |hh|hora de dois dígitos (00 a 23)|
  |mm|minutos de dois dígitos (00 a 59)|
  |ss|segundos de dois dígitos (00 a 59)|
  |. fffffff|segundos fracionários de sete dígitos|
  |Z|Designador UTC (tempo Universal Coordenado)||
  
  Para obter mais informações sobre o formato ISO 8601, consulte [ISO_8601](https://en.wikipedia.org/wiki/ISO_8601)

## <a name="remarks"></a>Comentários

  GetCurrentDateTime () é uma função não determinística. 
  
  O resultado retornado é UTC.

  A precisão é de 7 dígitos, com uma precisão de 100 nanossegundos.

## <a name="examples"></a>Exemplos
  
  O exemplo a seguir mostra como obter a data e hora UTC atuais usando a função interna GetCurrentDateTime ().
  
```sql
SELECT GetCurrentDateTime() AS currentUtcDateTime
```  
  
 Veja um exemplo de conjunto de resultados.
  
```json
[{
  "currentUtcDateTime": "2019-05-03T20:36:17.1234567Z"
}]  
```  

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

- [Funções de data e hora Azure Cosmos DB](sql-query-date-time-functions.md)
- [Funções do sistema Azure Cosmos DB](sql-query-system-functions.md)
- [Introdução ao Azure Cosmos DB](introduction.md)
