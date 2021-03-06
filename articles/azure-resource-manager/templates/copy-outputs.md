---
title: Definir várias instâncias de um valor de saída
description: Use a operação de cópia em um modelo de Azure Resource Manager para iterar várias vezes ao retornar um valor de uma implantação.
ms.topic: conceptual
ms.date: 02/25/2020
ms.openlocfilehash: db5c548c7bd4c60357d3656b1273b0192c497459
ms.sourcegitcommit: 5a71ec1a28da2d6ede03b3128126e0531ce4387d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77624768"
---
# <a name="output-iteration-in-azure-resource-manager-templates"></a>Iteração de saída em modelos de Azure Resource Manager

Este artigo mostra como criar mais de um valor para uma saída em seu modelo de Azure Resource Manager. Ao adicionar o elemento **copiar** à seção de saídas do modelo, você pode retornar dinamicamente vários itens durante a implantação.

Você também pode usar copiar com [recursos](copy-resources.md), [Propriedades em um recurso](copy-properties.md)e [variáveis](copy-variables.md).

## <a name="outputs-iteration"></a>Iteração de saída

O elemento Copy tem o seguinte formato geral:

```json
"copy": [
  {
    "count": <number-of-iterations>,
    "input": <values-for-the-variable>
  }
]
```

A propriedade **Count** especifica o número de iterações que você deseja para o valor de saída.

A propriedade de **entrada** especifica as propriedades que você deseja repetir. Você cria uma matriz de elementos construídos com base no valor na propriedade de **entrada** . Pode ser uma única propriedade (como uma cadeia de caracteres) ou um objeto com várias propriedades.

O exemplo a seguir cria um número variável de contas de armazenamento e retorna um ponto de extremidade para cada conta de armazenamento:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageCount": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "variables": {
        "baseName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2019-04-01",
            "name": "[concat(copyIndex(), variables('baseName'))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": "[parameters('storageCount')]"
            }
        }
    ],
    "outputs": {
        "storageEndpoints": {
            "type": "array",
            "copy": {
                "count": "[parameters('storageCount')]",
                "input": "[reference(concat(copyIndex(), variables('baseName'))).primaryEndpoints.blob]"
            }
        }
    }
}
```

O modelo anterior retorna uma matriz com os seguintes valores:

```json
[
    "https://0storagecfrbqnnmpeudi.blob.core.windows.net/",
    "https://1storagecfrbqnnmpeudi.blob.core.windows.net/"
]
```

O próximo exemplo retorna três propriedades das novas contas de armazenamento.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageCount": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "variables": {
        "baseName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2019-04-01",
            "name": "[concat(copyIndex(), variables('baseName'))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": "[parameters('storageCount')]"
            }
        }
    ],
    "outputs": {
        "storageInfo": {
            "type": "array",
            "copy": {
                "count": "[parameters('storageCount')]",
                "input": {
                    "id": "[reference(concat(copyIndex(), variables('baseName')), '2019-04-01', 'Full').resourceId]",
                    "blobEndpoint": "[reference(concat(copyIndex(), variables('baseName'))).primaryEndpoints.blob]",
                    "status": "[reference(concat(copyIndex(), variables('baseName'))).statusOfPrimary]"
                }
            }
        }
    }
}
```

O exemplo anterior retorna uma matriz com os seguintes valores:

```json
[
    {
        "id": "Microsoft.Storage/storageAccounts/0storagecfrbqnnmpeudi",
        "blobEndpoint": "https://0storagecfrbqnnmpeudi.blob.core.windows.net/",
        "status": "available"
    },
    {
        "id": "Microsoft.Storage/storageAccounts/1storagecfrbqnnmpeudi",
        "blobEndpoint": "https://1storagecfrbqnnmpeudi.blob.core.windows.net/",
        "status": "available"
    }
]
```

## <a name="next-steps"></a>Próximas etapas

* Para passar por um tutorial, consulte [Tutorial: crie várias instâncias de recursos usando os modelos do Resource Manager](template-tutorial-create-multiple-instances.md).
* Para outros usos do elemento copiar, consulte:
  * [Iteração de recurso em modelos de Azure Resource Manager](copy-resources.md)
  * [Iteração de propriedade em modelos de Azure Resource Manager](copy-properties.md)
  * [Iteração variável em modelos de Azure Resource Manager](copy-variables.md)
* Para saber mais sobre as seções de um modelo, veja [Criando modelos do Azure Resource Manager](template-syntax.md).
* Para saber mais sobre como implantar o modelo, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](deploy-powershell.md).

