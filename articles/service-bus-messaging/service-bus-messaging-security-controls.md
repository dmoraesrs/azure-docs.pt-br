---
title: Controles de segurança para mensagens do barramento de serviço do Azure
description: Uma lista de verificação de controles de segurança para avaliar as mensagens do barramento de serviço do Azure
services: service-bus-messaging
ms.service: service-bus-messaging
author: spelluru
ms.topic: conceptual
ms.date: 09/23/2019
ms.author: spelluru
ms.openlocfilehash: af119ef026b70fcb4a56b4f823d20c0e9eddddc8
ms.sourcegitcommit: 3eb0cc8091c8e4ae4d537051c3265b92427537fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75903259"
---
# <a name="security-controls-for-azure-service-bus-messaging"></a>Controles de segurança para mensagens do barramento de serviço do Azure

Este artigo documenta os controles de segurança incorporados ao sistema de mensagens do barramento de serviço do Azure.

[!INCLUDE [Security controls Header](../../includes/security-controls-header.md)]

## <a name="network"></a>Rede

| Controle de segurança | Sim/Não | Observações | Documentação |
|---|---|--|--|
| Suporte ao ponto de extremidade de serviço| Sim (somente camada Premium) | Os pontos de extremidade do serviço VNet têm suporte somente para a [camada Premium do barramento de serviço](service-bus-premium-messaging.md) . |  |
| Suporte à injeção de VNet| Não | |  |
| Isolamento de rede e suporte de firewall| Sim (somente camada Premium) |  |  |
| Suporte a túnel forçado| Não |  |  |

## <a name="monitoring--logging"></a>Monitorando & log

| Controle de segurança | Sim/Não | Observações| Documentação |
|---|---|--|--|
| Suporte ao monitoramento do Azure (log Analytics, app insights, etc.)| Sim | Com suporte via [Azure monitor e alertas](service-bus-metrics-azure-monitor.md). |  |
| Registro e auditoria do plano de gerenciamento e controle| Sim | Os logs de operações estão disponíveis.  | [Logs de diagnóstico do barramento de serviço](service-bus-diagnostic-logs.md) |
| Log e auditoria do plano de dados| Não |  |

## <a name="identity"></a>Identidade

| Controle de segurança | Sim/Não | Observações| Documentação |
|---|---|--|--|
| Autenticação| Sim | Gerenciado por meio de [Azure Active Directory identidade de serviço gerenciada](service-bus-managed-service-identity.md).| [Autenticação e autorização do barramento de serviço](service-bus-authentication-and-authorization.md). |
| Autorização| Sim | Dá suporte à autorização por meio do [RBAC](authenticate-application.md) e do token SAS. | [Autenticação e autorização do barramento de serviço](service-bus-authentication-and-authorization.md). |

## <a name="data-protection"></a>Proteção de dados

| Controle de segurança | Sim/Não | Observações | Documentação |
|---|---|--|--|
| Criptografia no lado do servidor em repouso: chaves gerenciadas pela Microsoft |  Sim, para criptografia do lado do servidor, em repouso, por padrão. |  |  |
| Criptografia no lado do servidor em repouso: chaves gerenciadas pelo cliente (BYOK) | Sim. | Uma chave gerenciada pelo cliente no Azure keyvault pode ser usada para criptografar os dados no namespace do barramento de serviço em repouso. | [Configurar chaves gerenciadas pelo cliente para criptografar dados do barramento de serviço do Azure em repouso usando o portal do Azure](configure-customer-managed-key.md)  |
| Criptografia em nível de coluna (serviços de dados do Azure)| N/D | |   |
| Criptografia em trânsito (como criptografia de ExpressRoute, criptografia de vnet e criptografia vnet)| Sim | Dá suporte ao mecanismo HTTPS/TLS padrão. |   |
| Chamadas criptografadas à API| Sim | As chamadas à API são feitas por meio de [Azure Resource Manager](../azure-resource-manager/index.yml) e HTTPS. |   |

## <a name="configuration-management"></a>Gerenciamento de configuração

| Controle de segurança | Sim/Não | Observações| Documentação |
|---|---|--|--|
| Suporte ao gerenciamento de configuração (controle de versão de configuração, etc.)| Sim | Dá suporte ao controle de versão do provedor de recursos por meio da [API Azure Resource Manager](/rest/api/resources/).|   |

## <a name="next-steps"></a>Próximos passos

- Saiba mais sobre os [controles de segurança internos nos serviços do Azure](../security/fundamentals/security-controls.md).
