---
title: Autorizar o acesso com o Azure Active Directory
description: Este artigo fornece informações sobre como autorizar o acesso aos recursos de hubs de eventos usando Azure Active Directory.
services: event-hubs
ms.service: event-hubs
documentationcenter: ''
author: spelluru
ms.topic: conceptual
ms.date: 02/12/2020
ms.author: spelluru
ms.openlocfilehash: 16d8faa1f20227241d1a582dd4d80e0123f7a31e
ms.sourcegitcommit: f97f086936f2c53f439e12ccace066fca53e8dc3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2020
ms.locfileid: "77368500"
---
# <a name="authorize-access-to-event-hubs-resources-using-azure-active-directory"></a>Autorizar o acesso aos recursos de hubs de eventos usando Azure Active Directory
Os hubs de eventos do Azure dão suporte ao uso de Azure Active Directory (AD do Azure) para autorizar solicitações para recursos de hubs de eventos. Com o Azure AD, você pode usar o RBAC (controle de acesso baseado em função) para conceder permissões a uma entidade de segurança, que pode ser um usuário ou uma entidade de serviço de aplicativo. Para saber mais sobre funções e atribuições de função, confira [noções básicas sobre as diferentes funções](../role-based-access-control/overview.md).

## <a name="overview"></a>Visão geral
Quando uma entidade de segurança (um usuário ou um aplicativo) tenta acessar um recurso de hubs de eventos, a solicitação deve ser autorizada. Com o Azure AD, o acesso a um recurso é um processo de duas etapas. 

 1. Primeiro, a identidade da entidade de segurança é autenticada e um token OAuth 2,0 é retornado. O nome do recurso para solicitar um token é `https://eventhubs.azure.net/`.
 1. Em seguida, o token é passado como parte de uma solicitação para o serviço de hubs de eventos para autorizar o acesso ao recurso especificado.

A etapa de autenticação requer que uma solicitação de aplicativo contenha um token de acesso OAuth 2,0 em tempo de execução. Se um aplicativo estiver em execução em uma entidade do Azure, como uma VM do Azure, um conjunto de dimensionamento de máquinas virtuais ou um aplicativo de funções do Azure, ele poderá usar uma identidade gerenciada para acessar os recursos. Para saber como autenticar solicitações feitas por uma identidade gerenciada para o serviço de hubs de eventos, consulte [autenticar o acesso aos recursos dos hubs de eventos do Azure com Azure Active Directory e identidades gerenciadas para recursos do Azure](authenticate-managed-identity.md). 

A etapa de autorização requer que uma ou mais funções RBAC sejam atribuídas à entidade de segurança. Os hubs de eventos do Azure fornecem funções RBAC que abrangem conjuntos de permissões para recursos de hubs de eventos. As funções atribuídas a uma entidade de segurança determinam as permissões que o principal terá. Para obter mais informações sobre as funções RBAC, consulte [funções RBAC internas para hubs de eventos do Azure](#built-in-rbac-roles-for-azure-event-hubs). 

Aplicativos nativos e aplicativos Web que fazem solicitações para hubs de eventos também podem autorizar com o Azure AD. Para saber como solicitar um token de acesso e usá-lo para autorizar solicitações para recursos de hubs de eventos, consulte [autenticar o acesso aos hubs de eventos do Azure com o Azure AD de um aplicativo](authenticate-application.md). 

## <a name="assign-rbac-roles-for-access-rights"></a>Atribuir funções RBAC para direitos de acesso
Azure Active Directory (Azure AD) autoriza os direitos de acesso aos recursos protegidos por meio do [controle de acesso baseado em função (RBAC)](../role-based-access-control/overview.md). Os hubs de eventos do Azure definem um conjunto de funções RBAC internas que abrangem conjuntos comuns de permissões usadas para acessar dados do hub de eventos e você também pode definir funções personalizadas para acessar os dados.

Quando uma função RBAC é atribuída a uma entidade de segurança do Azure AD, o Azure concede acesso a esses recursos para essa entidade de segurança. O acesso pode ser definido para o nível de assinatura, o grupo de recursos, o namespace de hubs de eventos ou qualquer recurso sob ele. Uma entidade de segurança do Azure AD pode ser um usuário ou uma entidade de serviço de aplicativo ou uma [identidade gerenciada para recursos do Azure](../active-directory/managed-identities-azure-resources/overview.md).

## <a name="built-in-rbac-roles-for-azure-event-hubs"></a>Funções RBAC internas para hubs de eventos do Azure
O Azure fornece as seguintes funções RBAC internas para autorizar o acesso aos dados dos hubs de eventos usando o Azure AD e o OAuth:

- [Proprietário de dados dos hubs de eventos do Azure](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-owner): Use essa função para fornecer acesso completo aos recursos dos hubs de eventos.
- [Remetente de dados dos hubs de eventos do Azure](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-receiver): Use essa função para fornecer acesso de envio aos recursos dos hubs de eventos.
- [Receptor de dados dos hubs de eventos do Azure](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-sender): Use essa função para fornecer o acesso de consumo/recebimento aos recursos dos hubs de eventos.

## <a name="resource-scope"></a>Escopo de recurso 
Antes de atribuir uma função de RBAC a uma entidade de segurança, determine o escopo de acesso que a entidade de segurança deve ter. As práticas recomendadas ditam que é sempre melhor conceder apenas o escopo mais estreito possível.

A lista a seguir descreve os níveis nos quais você pode fazer o escopo de acesso a recursos de hubs de eventos, começando com o escopo mais estreito:

- **Grupo de consumidores**: nesse escopo, a atribuição de função se aplica somente a essa entidade. Atualmente, o portal do Azure não dá suporte à atribuição de uma função RBAC a uma entidade de segurança nesse nível. 
- **Hub de eventos**: a atribuição de função se aplica à entidade do hub de eventos e ao grupo de consumidores sob ela.
- **Namespace**: a atribuição de função abrange toda a topologia de hubs de eventos no namespace e no grupo de consumidores associado a ela.
- **Grupo de recursos**: a atribuição de função se aplica a todos os recursos de hubs de eventos no grupo de recursos.
- **Assinatura**: a atribuição de função se aplica a todos os recursos de hubs de eventos em todos os grupos de recursos na assinatura.

> [!NOTE]
> - Tenha em mente que as atribuições de função do RBAC podem levar até cinco minutos para serem propagadas. 
> - Esse conteúdo se aplica a hubs de eventos e hubs de eventos para Apache Kafka. Para obter mais informações sobre os hubs de eventos para suporte a Kafka, consulte [hubs de eventos para Kafka-segurança e autenticação](event-hubs-for-kafka-ecosystem-overview.md#security-and-authentication).


Para obter mais informações sobre como as funções internas são definidas, consulte [entender as definições de função](../role-based-access-control/role-definitions.md#management-and-data-operations). Para obter informações sobre como criar funções RBAC personalizadas, consulte [criar funções personalizadas para o controle de acesso baseado em função do Azure](../role-based-access-control/custom-roles.md).



## <a name="samples"></a>Exemplos
- [Exemplos de Microsoft. Azure. EventHubs](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac). 
    
    Esses exemplos usam a antiga biblioteca **Microsoft. Azure. EventHubs** , mas você pode atualizá-lo facilmente para usar a biblioteca **Azure. Messaging. EventHubs** mais recente. Para mover o exemplo do usando a biblioteca antiga para uma nova, consulte o [guia para migrar de Microsoft. Azure. EventHubs para Azure. Messaging. EventHubs](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs/migration-guide-from-v4.md).
- [Exemplos do Azure. Messaging. EventHubs](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp)

    Este exemplo foi atualizado para usar a biblioteca **Azure. Messaging. EventHubs** mais recente.
- [Hubs de eventos para exemplos de Kafka-OAuth](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth). 


## <a name="next-steps"></a>Próximas etapas
- Saiba como atribuir uma função interna de RBAC a uma entidade de segurança, consulte [autenticar o acesso aos recursos dos hubs de eventos usando Azure Active Directory](authenticate-application.md).
- Saiba [como criar funções personalizadas com o RBAC](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac/CustomRole).
- Saiba [como usar Azure Active Directory com eh](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac/AzureEventHubsSDK)

Consulte os seguintes artigos relacionados:

- [Autenticar solicitações para hubs de eventos do Azure por meio de um aplicativo usando Azure Active Directory](authenticate-application.md)
- [Autenticar uma identidade gerenciada com Azure Active Directory para acessar recursos de hubs de eventos](authenticate-managed-identity.md)
- [Autenticar solicitações para hubs de eventos do Azure usando assinaturas de acesso compartilhado](authenticate-shared-access-signature.md)
- [Autorizar o acesso a recursos de hubs de eventos usando assinaturas de acesso compartilhado](authorize-access-shared-access-signature.md)