---
title: Histórico de implantações
description: Descreve como exibir as operações de implantação do Azure Resource Manager com o portal, o PowerShell, a CLI do Azure e a API REST.
tags: top-support-issue
ms.topic: conceptual
ms.date: 11/26/2019
ms.openlocfilehash: 753071a3edca62690b772f7b8d34fec43641466f
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75477857"
---
# <a name="view-deployment-history-with-azure-resource-manager"></a>Exibir histórico de implantação com Azure Resource Manager

Azure Resource Manager permite que você exiba seu histórico de implantação e examine operações específicas em implantações anteriores. Você pode ver os recursos que foram implantados e obter informações sobre quaisquer erros.

Para obter ajuda com a resolução de erros de implantação específicos, veja [Resolver erros comuns ao implantar recursos no Azure com o Azure Resource Manager](common-deployment-errors.md).

## <a name="get-deployments-and-correlation-id"></a>Obter as implantações e a ID de correlação

Você pode exibir detalhes sobre uma implantação por meio do portal do Azure, do PowerShell, do CLI do Azure ou da API REST. Cada implantação tem uma ID de correlação, que é usada para rastrear eventos relacionados. Pode ser útil ao trabalhar com o suporte técnico para solucionar problemas de implantação.

# <a name="portaltabazure-portal"></a>[Portal](#tab/azure-portal)

1. Selecione o grupo de recursos que você deseja examinar.

1. Selecione o link em **implantações**.

   ![Selecionar histórico de implantação](./media/deployment-history/select-deployment-history.png)

1. Selecione uma das implantações do histórico de implantação.

   ![Selecionar a implantação](./media/deployment-history/select-details.png)

1. Um resumo da implantação é exibido, incluindo a ID de correlação. 

    ![Resumo da implantação](./media/deployment-history/show-correlation-id.png)

# <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

Para listar todas as implantações de um grupo de recursos, use o comando [Get-AzResourceGroupDeployment](/powershell/module/az.resources/Get-AzResourceGroupDeployment) .

```azurepowershell-interactive
Get-AzResourceGroupDeployment -ResourceGroupName ExampleGroup
```

Para obter uma implantação específica de um grupo de recursos, adicione o parâmetro **deploymentname** .

```azurepowershell-interactive
Get-AzResourceGroupDeployment -ResourceGroupName ExampleGroup -DeploymentName ExampleDeployment
```

Para obter a ID de correlação, use:

```azurepowershell-interactive
(Get-AzResourceGroupDeployment -ResourceGroupName ExampleGroup -DeploymentName ExampleDeployment).CorrelationId
```

# <a name="azure-clitabazure-cli"></a>[CLI do Azure](#tab/azure-cli)

Para listar a implantação de um grupo de recursos, use [AZ Group Deployment List](/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-list).

```azurecli-interactive
az group deployment list --resource-group ExampleGroup
```

Para obter uma implantação específica, use o [grupo de implantação AZ Group show](/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-show).

```azurecli-interactive
az group deployment show --resource-group ExampleGroup --name ExampleDeployment
```
  
Para obter a ID de correlação, use:

```azurecli-interactive
az group deployment show --resource-group ExampleGroup --name ExampleDeployment --query properties.correlationId
```

# <a name="httptabhttp"></a>[HTTP](#tab/http)

Para listar as implantações de um grupo de recursos, use a operação a seguir. Para obter o número de versão da API mais recente a ser usado na solicitação, consulte [implantações-listar por grupo de recursos](/rest/api/resources/deployments/listbyresourcegroup). 

```
GET https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/?api-version={api-version}
```

Para obter uma implantação específica. Use a operação a seguir. Para obter o número de versão da API mais recente a ser usado na solicitação, consulte [implantações-obter](/rest/api/resources/deployments/get).

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
```

A resposta inclui a ID de correlação.

```json
{
 ...
 "properties": {
   "mode": "Incremental",
   "provisioningState": "Failed",
   "timestamp": "2019-11-26T14:18:36.4518358Z",
   "duration": "PT26.2091817S",
   "correlationId": "47ff4228-bf2e-4ee5-a008-0b07da681230",
   ...
 }
}
```

---

## <a name="get-deployment-operations-and-error-message"></a>Obter mensagens de erro e operações de implantação

Cada implantação pode incluir várias operações. Para ver mais detalhes sobre uma implantação, exiba as operações de implantação. Quando uma implantação falha, as operações de implantação incluem uma mensagem de erro.

# <a name="portaltabazure-portal"></a>[Portal](#tab/azure-portal)

1. No Resumo de uma implantação, selecione **detalhes da operação**.

    ![Selecionar operações de implantação](./media/deployment-history/get-operation-details.png)

1. Você verá os detalhes dessa etapa da implantação. Quando ocorre um erro, os detalhes incluem a mensagem de erro.

    ![Mostrar detalhes da operação](./media/deployment-history/see-operation-details.png)

# <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

Para exibir as operações de implantação para implantação em um grupo de recursos, use o comando [Get-AzResourceGroupDeploymentOperation](/powershell/module/az.resources/get-azdeploymentoperation) .

```azurepowershell-interactive
Get-AzResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName ExampleDeploy
```

Para exibir as operações com falha, filtre operações com estado de **falha** .

```azurepowershell-interactive
(Get-AzResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName ExampleDeploy).Properties | Where-Object ProvisioningState -eq Failed
```

Para obter a mensagem de status das operações com falha, use o seguinte comando:

```azurepowershell-interactive
((Get-AzResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName ExampleDeploy ).Properties | Where-Object ProvisioningState -eq Failed).StatusMessage.error
```

# <a name="azure-clitabazure-cli"></a>[CLI do Azure](#tab/azure-cli)

Para exibir as operações de implantação para implantação em um grupo de recursos, use o comando [AZ Group Deployment Operation List](/cli/azure/group/deployment/operation?view=azure-cli-latest#az-group-deployment-operation-list) .

```azurecli-interactive
az group deployment operation list --resource-group ExampleGroup --name ExampleDeployment
```

Para exibir as operações com falha, filtre operações com estado de **falha** .

```azurecli-interactive
az group deployment operation list --resource-group ExampleGroup --name ExampleDeploy --query "[?properties.provisioningState=='Failed']"
```

Para obter a mensagem de status das operações com falha, use o seguinte comando:

```azurecli-interactive
az group deployment operation list --resource-group ExampleGroup --name ExampleDeploy --query "[?properties.provisioningState=='Failed'].properties.statusMessage.error"
```

# <a name="httptabhttp"></a>[HTTP](#tab/http)

Para obter operações de implantação, use a seguinte operação. Para obter o número de versão da API mais recente a ser usado na solicitação, consulte [Deployment Operations-List](/rest/api/resources/deploymentoperations/list).

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
```

A resposta inclui uma mensagem de erro.

```json
{
  "value": [
    {
      "id": "/subscriptions/xxxx/resourceGroups/examplegroup/providers/Microsoft.Resources/deployments/exampledeploy/operations/13EFD9907103D640",
      "operationId": "13EFD9907103D640",
      "properties": {
        "provisioningOperation": "Create",
        "provisioningState": "Failed",
        "timestamp": "2019-11-26T14:18:36.3177613Z",
        "duration": "PT21.0580179S",
        "trackingId": "9d3cdac4-54f8-486c-94bd-10c20867b8bc",
        "serviceRequestId": "01a9d0fe-896b-4c94-a30f-60b70a8f1ad9",
        "statusCode": "BadRequest",
        "statusMessage": {
          "error": {
            "code": "InvalidAccountType",
            "message": "The AccountType Standard_LRS1 is invalid. For more information, see - https://aka.ms/storageaccountskus"
          }
        },
        "targetResource": {
          "id": "/subscriptions/xxxx/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/storageq2czadzfgizc2",
          "resourceType": "Microsoft.Storage/storageAccounts",
          "resourceName": "storageq2czadzfgizc2"
        }
      }
    },
    ...
  ]
}
```

---

## <a name="next-steps"></a>Próximos passos

* Para obter ajuda com a resolução de erros de implantação específicos, veja [Resolver erros comuns ao implantar recursos no Azure com o Azure Resource Manager](common-deployment-errors.md).
* Para saber mais sobre como usar os logs de atividades para monitorar outros tipos de ação, confira [View activity logs to manage Azure resources](../management/view-activity-logs.md) (Exibir logs de atividades para gerenciar recursos do Azure).
* Para validar sua implantação antes de executá-la, consulte [Implantar um grupo de recursos com um modelo do Azure Resource Manager](deploy-powershell.md).

