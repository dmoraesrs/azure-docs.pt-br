---
title: CLI do Azure Service Fabric-aplicativo de malha sfctl
description: Saiba mais sobre o sfctl, a interface de linha de comando Service Fabric do Azure. Inclui uma lista de comandos para gerenciar Service Fabric recursos de aplicativo de malha.
author: jeffj6123
ms.topic: reference
ms.date: 1/16/2020
ms.author: jejarry
ms.openlocfilehash: 7c571136e6bef64c2024c81db85ef736f64a4e01
ms.sourcegitcommit: 67e9f4cc16f2cc6d8de99239b56cb87f3e9bff41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76906065"
---
# <a name="sfctl-mesh-app"></a>sfctl mesh app
Obter e excluir os recursos do aplicativo.

## <a name="commands"></a>Comandos

|Comando|Description|
| --- | --- |
| excluir | Exclui o recurso de aplicativo. |
| list | Lista todos os recursos do aplicativo. |
| mostrar | Obtém o recurso do aplicativo com o nome fornecido. |

## <a name="sfctl-mesh-app-delete"></a>sfctl mesh app delete
Exclui o recurso de aplicativo.

Exclui o recurso do aplicativo identificado pelo nome.

### <a name="arguments"></a>Argumentos

|Argumento|Description|
| --- | --- |
| --name -n [Obrigatório] | O nome do aplicativo. |

### <a name="global-arguments"></a>Argumentos globais

|Argumento|Description|
| --- | --- |
| --debug | Aumente o detalhamento do log para mostrar todos os logs de depuração. |
| --help -h | Mostrar esta mensagem de ajuda e sair. |
| --output -o | Formato de saída.  Valores permitidos\: json, jsonc, tabela, tsv.  Padrão\: json. |
| --query | Cadeia de caracteres de consulta JMESPath. Veja http\://jmespath.org/ para saber mais e obter exemplos. |
| --verbose | Aumentar o detalhamento do log. Use --debug para logs de depuração completos. |

## <a name="sfctl-mesh-app-list"></a>sfctl mesh app list
Lista todos os recursos do aplicativo.

Obtém as informações sobre todos os recursos do aplicativo em um determinado grupo de recursos. As informações incluem a descrição e outras propriedades do aplicativo.

### <a name="global-arguments"></a>Argumentos globais

|Argumento|Description|
| --- | --- |
| --debug | Aumente o detalhamento do log para mostrar todos os logs de depuração. |
| --help -h | Mostrar esta mensagem de ajuda e sair. |
| --output -o | Formato de saída.  Valores permitidos\: json, jsonc, tabela, tsv.  Padrão\: json. |
| --query | Cadeia de caracteres de consulta JMESPath. Veja http\://jmespath.org/ para saber mais e obter exemplos. |
| --verbose | Aumentar o detalhamento do log. Use --debug para logs de depuração completos. |

## <a name="sfctl-mesh-app-show"></a>sfctl mesh app show
Obtém o recurso do aplicativo com o nome fornecido.

Obtém as informações sobre o recurso do aplicativo com o nome fornecido. As informações incluem a descrição e outras propriedades do aplicativo.

### <a name="arguments"></a>Argumentos

|Argumento|Description|
| --- | --- |
| --name -n [Obrigatório] | O nome do aplicativo. |

### <a name="global-arguments"></a>Argumentos globais

|Argumento|Description|
| --- | --- |
| --debug | Aumente o detalhamento do log para mostrar todos os logs de depuração. |
| --help -h | Mostrar esta mensagem de ajuda e sair. |
| --output -o | Formato de saída.  Valores permitidos\: json, jsonc, tabela, tsv.  Padrão\: json. |
| --query | Cadeia de caracteres de consulta JMESPath. Veja http\://jmespath.org/ para saber mais e obter exemplos. |
| --verbose | Aumentar o detalhamento do log. Use --debug para logs de depuração completos. |


## <a name="next-steps"></a>Próximos passos
- [Configurar](service-fabric-cli.md) a CLI do Service Fabric.
- Saiba como usar a CLI do Service Fabric usando os [scripts de exemplo](/azure/service-fabric/scripts/sfctl-upgrade-application).