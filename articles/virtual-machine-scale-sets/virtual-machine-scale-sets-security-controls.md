---
title: Controles de segurança para conjuntos de dimensionamento de máquinas virtuais do Azure
description: Uma lista de verificação de controles de segurança para avaliar os conjuntos de dimensionamento de máquinas virtuais do Azure
ms.service: virtual-machine-scale-sets
author: msmbaldwin
ms.topic: conceptual
ms.date: 09/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 4007f4adeee065fe32492d3bd16f3a06d24e7d96
ms.sourcegitcommit: b07964632879a077b10f988aa33fa3907cbaaf0e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2020
ms.locfileid: "77190601"
---
# <a name="security-controls-for-azure-virtual-machine-scale-sets"></a>Controles de segurança para conjuntos de dimensionamento de máquinas virtuais do Azure

Este artigo documenta os controles de segurança criados nos conjuntos de dimensionamento de máquinas virtuais do Azure.

[!INCLUDE [Security controls header](../../includes/security-controls-header.md)]

## <a name="network"></a>Rede

| Controle de segurança | Sim/Não | Observações |
|---|---|--|
| Suporte ao ponto de extremidade de serviço| Sim | |
| Suporte à injeção de VNet| Sim | |
| Isolamento de rede e suporte de firewall| Sim |  |
| Suporte a túnel forçado| Sim | Consulte [Configurar o túnel forçado usando o modelo de implantação Azure Resource Manager](/azure/vpn-gateway/vpn-gateway-forced-tunneling-rm). |

## <a name="monitoring--logging"></a>Monitorando & log

| Controle de segurança | Sim/Não | Observações|
|---|---|--|
| Suporte ao monitoramento do Azure (log Analytics, app insights, etc.)| Sim | Consulte [monitorar e atualizar uma máquina virtual Linux no Azure](/azure/virtual-machines/linux/tutorial-monitoring) e [monitorar e atualizar uma máquina virtual do Windows no Azure](/azure/virtual-machines/windows/tutorial-monitoring). |
| Registro e auditoria do plano de gerenciamento e controle| Sim |  |
| Log e auditoria do plano de dados | Não |  |

## <a name="identity"></a>Identidade

| Controle de segurança | Sim/Não | Observações|
|---|---|--|
| Autenticação| Sim |  |
| Autorização| Sim |  |

## <a name="data-protection"></a>Proteção de dados

| Controle de segurança | Sim/Não | Observações |
|---|---|--|
| Criptografia no lado do servidor em repouso: chaves gerenciadas pela Microsoft | Sim | Consulte [Azure Disk Encryption para conjuntos de dimensionamento de máquinas virtuais](disk-encryption-overview.md). |
| Criptografia em trânsito (como criptografia de ExpressRoute, criptografia de vnet e criptografia vnet)| Sim | As máquinas virtuais do Azure dão suporte à criptografia de [ExpressRoute](/azure/expressroute) e VNet. Consulte [criptografia em trânsito em VMs](/azure/security/security-azure-encryption-overview#in-transit-encryption-in-vms). |
| Criptografia no lado do servidor em repouso: chaves gerenciadas pelo cliente (BYOK) | Sim | As chaves gerenciadas pelo cliente são um cenário de criptografia do Azure com suporte; consulte Confira [Azure Disk Encryption para conjuntos de dimensionamento de máquinas virtuais](disk-encryption-overview.md)|
| Criptografia em nível de coluna (serviços de dados do Azure)| N/D | |
| Chamadas criptografadas à API| Sim | Via HTTPS e TLS. |

## <a name="configuration-management"></a>Gerenciamento de configuração

| Controle de segurança | Sim/Não | Observações|
|---|---|--|
| Suporte ao gerenciamento de configuração (controle de versão de configuração, etc.)| Sim |  | 

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre os [controles de segurança internos nos serviços do Azure](../security/fundamentals/security-controls.md).
