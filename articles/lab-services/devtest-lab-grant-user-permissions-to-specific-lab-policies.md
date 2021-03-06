---
title: Conceder permissões de usuário para políticas específicas do laboratório | Microsoft Docs
description: Saiba como conceder permissões de usuário para políticas específicas dos Laboratórios de Desenvolvimento/Teste com base nas necessidades de cada usuário
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2019
ms.author: spelluru
ms.openlocfilehash: 9b31f3e68fbabc32f301fdcd8066a3bfbf1c2dbd
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79284207"
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a>Conceder permissões de usuário para políticas específicas do laboratório
## <a name="overview"></a>Visão geral
Este artigo ilustra como usar o PowerShell para conceder aos usuários permissões para uma determinada política de laboratório. Dessa forma, as permissões podem ser aplicadas com base nas necessidades de cada usuário. Por exemplo, talvez você queira conceder a um usuário específico a capacidade de alterar as configurações de política de VM, mas não as políticas de custo.

## <a name="policies-as-resources"></a>Políticas como recursos
Como discutido no artigo [Controle de acesso baseado em função do Azure](../role-based-access-control/role-assignments-portal.md) , o RBAC permite o gerenciamento de acesso refinado de recursos do Azure. Com o RBAC, você pode separar as tarefas dentro de sua equipe de operação de desenvolvimento e conceder somente a quantidade de acesso que os usuários precisam para realizar seus trabalhos.

Nos Laboratórios de Desenvolvimento/Teste, uma política é um tipo de recurso que habilita a ação de RBAC **Microsoft.DevTestLab/labs/policySets/policies/** . Cada política do laboratório é um recurso do tipo de recurso Política e pode ser atribuída como um escopo a uma função RBAC.

Por exemplo, para conceder aos usuários permissão de leitura/gravação para a política de **tamanhos de VM permitidos** , você deve criar uma função personalizada que funcione com a ação **Microsoft. DevTestLab/Labs/policySets/Policies/** e, em seguida, atribuir os usuários apropriados a essa função personalizada no escopo de **Microsoft. DevTestLab/Labs/PolicySets/Policies/AllowedVmSizesInLab**.

Para saber mais sobre as funções personalizadas no RBAC, consulte o [Controle de acesso das funções personalizadas](../role-based-access-control/custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Criar uma função personalizada do laboratório usando o PowerShell
Para começar, você precisará [instalar o Azure PowerShell](/powershell/azure/install-az-ps). 

Depois de configurar os cmdlets do Azure PowerShell, você pode executar as seguintes tarefas:

* Listar todas as operações/ações para um provedor de recursos
* Listar ações em uma função específica:
* Criar uma função personalizada

O seguinte script do PowerShell apresenta exemplos de como executar essas tarefas:

    # List all the operations/actions for a resource provider.
    Get-AzProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    # List actions in a particular role.
    (Get-AzRoleDefinition "DevTest Labs User").Actions

    # Create custom role.
    $policyRoleDef = (Get-AzRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a>Atribuir permissões a um usuário para uma política específica usando funções personalizadas
Depois de definir suas funções personalizadas, você pode atribuí-las aos usuários. Para atribuir uma função personalizada a um usuário, você deve primeiro obter o **ObjectId** que representa esse usuário. Para fazer isso, use o cmdlet **Get-AzADUser** .

No exemplo a seguir, o **ObjectId** do usuário *SomeUser* é 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.

    PS C:\>Get-AzADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Depois de obter o **ObjectID** para o usuário e um nome de função personalizado, você pode atribuir essa função ao usuário com o cmdlet **New-AzRoleAssignment** :

    PS C:\>New-AzRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/default/policies/AllowedVmSizesInLab

No exemplo anterior, a política **AllowedVmSizesInLab** é usada. Você pode usar qualquer uma das políticas a seguir:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Após você tiver concedido permissões de usuário para políticas específicas do laboratório, estas são algumas das próximas etapas a serem consideradas:

* [Proteger o acesso a um laboratório](devtest-lab-add-devtest-user.md)
* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md)
* [Criar um modelo de laboratório](devtest-lab-create-template.md)
* [Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md)
* [Adicionar uma VM a um laboratório](devtest-lab-add-vm.md)

