---
title: Usar uma identidade gerenciada atribuída pelo sistema para acessar Azure Key Vault
description: Saiba como criar uma identidade gerenciada para aplicativos do serviço de aplicativo e como usá-lo para acessar o Azure Key Vault
services: key-vault
author: msmbaldwin
manager: rkarlin
tags: azure-resource-manager
ms.service: key-vault
ms.subservice: general
ms.topic: conceptual
ms.date: 09/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 36a4871339401629300eedd77b6441aed10aabf3
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79270947"
---
# <a name="provide-key-vault-authentication-with-a-managed-identity"></a>Fornecer autenticação de Key Vault com uma identidade gerenciada

Uma identidade gerenciada do Azure Active Directory permite que seu aplicativo acesse facilmente outros recursos protegidos pelo Azure AD. A identidade é gerenciada pela plataforma do Azure e não exige provisionamento ou giro de nenhum segredo. Para saber mais, confira [Gerenciar identidades para recursos do Azure](../active-directory/managed-identities-azure-resources/overview.md). 

Este artigo mostra como criar uma identidade gerenciada para um aplicativo do serviço de aplicativo e usá-lo para acessar o Azure Key Vault. Para aplicativos hospedados em VMs do Azure, consulte [usar uma identidade gerenciada atribuída pelo sistema de VM do Windows para acessar Azure Key Vault](../active-directory/managed-identities-azure-resources/tutorial-windows-vm-access-nonaad.md).


[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="prerequisites"></a>Prerequisites 

Para concluir este guia, você deve ter os seguintes recursos. 

- Um cofre de chaves. Você pode usar um cofre de chaves existente ou criar um seguindo as etapas em um destes inícios rápidos:
   - [Criar um cofre de chaves com a CLI do Azure](quick-create-cli.md)
   - [Criar um cofre de chaves com o Azure PowerShell](quick-create-powershell.md)
   - [Criar um cofre de chaves com o portal do Azure](quick-create-portal.md).
- Um aplicativo do serviço de aplicativo existente ao qual conceder acesso ao cofre de chaves. Você pode criar um rapidamente seguindo as etapas na documentação do [serviço de aplicativo](../app-service/overview.md).
- [CLI do Azure](/cli/azure/install-azure-cli?view=azure-cli-latest) ou [Azure PowerShell](/powershell/azure/overview). Como alternativa, você pode usar o [portal do Azure](https://portal.azure.com).


## <a name="adding-a-system-assigned-identity"></a>Adicionando uma identidade designada pelo sistema 

Primeiro, você deve adicionar uma identidade atribuída pelo sistema a um aplicativo. 
 
### <a name="azure-portal"></a>Portal do Azure 

Para configurar uma identidade gerenciada no portal, primeiro, crie um aplicativo como normal e, em seguida, habilite o recurso. 

1. Se você estiver usando um aplicativo de funções, navegue até os **recursos da Plataforma**. Para outros tipos de aplicativo, role para baixo até o grupo **Configurações** no painel de navegação à esquerda. 

1. Selecione **Identidade gerenciada**. 

1. Na guia **Sistema atribuído**, alterne o **Status** para **Ligado**. Clique em **Save** (Salvar). 

    ![](./media/managed-identity-system-assigned.png)

### <a name="azure-cli"></a>CLI do Azure

Este guia de início rápido requer o CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para localizar a versão atual. Se você precisar instalar ou atualizar, confira [Instalar a CLI do Azure](/cli/azure/install-azure-cli?view=azure-cli-latest). 

Para entrar com CLI do Azure, use o comando [AZ login](/cli/azure/reference-index?view=azure-cli-latest#az-login) :

```azurecli-interactive
az login
```

Para obter mais informações sobre as opções de logon com o CLI do Azure, consulte [entrar com CLI do Azure](/cli/azure/authenticate-azure-cli?view=azure-cli-latest). 

Para criar a identidade para este aplicativo, use o comando CLI do Azure [AZ webapp Identity Assign](/cli/azure/webapp/identity?view=azure-cli-latest#az-webapp-identity-assign) ou o comando [AZ functionapp Identity Assign](/cli/azure/functionapp/identity?view=azure-cli-latest#az-functionapp-identity-assign) :


```azurecli-interactive
az webapp identity assign --name myApp --resource-group myResourceGroup
```

```azurecli-interactive
az functionapp identity assign --name myApp --resource-group myResourceGroup
```

Anote o `PrincipalId`, que será necessário na próxima seção.

```json
{
  "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "type": "SystemAssigned"
}
```
## <a name="grant-your-app-access-to-key-vault"></a>Conceder acesso ao aplicativo para Key Vault 

### <a name="azure-portal"></a>Portal do Azure

1.  Navegue até Key Vault recurso. 

1.  Selecione **políticas de acesso** e clique em **Adicionar política de acesso**. 

1.  Em **permissões de segredo**, selecione **obter, listar**. 

1.  Escolha **selecionar entidade de segurança**e, no campo de pesquisa, insira o nome do aplicativo.  Selecione o aplicativo na lista de resultados e clique em **selecionar**. 

1.  Clique em **Adicionar** para concluir a adição da nova política de acesso.

    ![](./media/managed-identity-access-policy.png)

### <a name="azure-cli"></a>CLI do Azure

Para conceder a seu aplicativo acesso ao cofre de chaves, use o comando CLI do Azure [AZ keyvault Set-Policy](/cli/azure/keyvault?view=azure-cli-latest#az-keyvault-set-policy) , fornecendo o parâmetro **ObjectID** com o **PrincipalId** anotado acima.

```azurecli-interactive
az keyvault set-policy --name myKeyVault --object-id <PrincipalId> --secret-permissions get list 
```

## <a name="next-steps"></a>Próximas etapas

- [Segurança de Azure Key Vault: gerenciamento de acesso e identidade](overview-security.md#identity-and-access-management)
- [Fornecer Key Vault autenticação com uma política de controle de acesso](key-vault-group-permissions-for-apps.md)
- [Sobre chaves, segredos e certificados](about-keys-secrets-and-certificates.md)
- [Proteger o cofre de chaves](key-vault-secure-your-key-vault.md).
- [Guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md)
- Examine as [Melhores práticas do Azure Key Vault](key-vault-best-practices.md)