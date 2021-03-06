---
title: Políticas de acesso condicional comum-Azure Active Directory
description: Políticas de acesso condicional comumente usadas para organizações
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 02/11/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb, rogoya
ms.collection: M365-identity-device-management
ms.openlocfilehash: cfb5fb17abd5a433c177d3efc5a4f0a2cec3d4d7
ms.sourcegitcommit: b07964632879a077b10f988aa33fa3907cbaaf0e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2020
ms.locfileid: "77186135"
---
# <a name="common-conditional-access-policies"></a>Políticas de Acesso Condicional Comum

[Os padrões de segurança](../fundamentals/concept-fundamentals-security-defaults.md) são ótimos para algumas, mas muitas organizações precisam de mais flexibilidade do que oferecem. Por exemplo, muitas precisam da capacidade de excluir contas específicas como suas contas de acesso de emergência ou de administração de interrupções de políticas de acesso condicional que exigem autenticação multifator. Para essas organizações, as políticas comuns referenciadas neste artigo podem ser usadas.

![Políticas de acesso condicional no portal do Azure](./media/concept-conditional-access-policy-common/conditional-access-policies-azure-ad-listing.png)

## <a name="emergency-access-accounts"></a>Contas de acesso de emergência

Mais informações sobre contas de acesso de emergência e por que elas são importantes podem ser encontradas nos seguintes artigos: 

* [Gerenciar contas de acesso de emergência no Azure AD](../users-groups-roles/directory-emergency-access.md)
* [Crie uma estratégia de gerenciamento de controle de acesso resiliente com Azure Active Directory](../authentication/concept-resilient-controls.md)

## <a name="typical-policies-deployed-by-organizations"></a>Políticas típicas implantadas por organizações

* [Exigir MFA para administradores](howto-conditional-access-policy-admin-mfa.md)\*
* [Exigir MFA para\* de gerenciamento do Azure](howto-conditional-access-policy-azure-management.md)
* [Exigir MFA para todos os usuários](howto-conditional-access-policy-all-users-mfa.md)\*
* [Bloquear\* de autenticação herdadas](howto-conditional-access-policy-block-legacy.md)
* [Acesso condicional com base em risco (requer Azure AD Premium P2)](howto-conditional-access-policy-risk.md)
* [Exigir local confiável para o registro de MFA](howto-conditional-access-policy-registration.md)
* [Bloquear o acesso por local](howto-conditional-access-policy-location.md)
* [Exigir dispositivo em conformidade](howto-conditional-access-policy-compliant-device.md)

\* essas quatro políticas quando configuradas juntas, imitariam a funcionalidade habilitada por [padrões de segurança](../fundamentals/concept-fundamentals-security-defaults.md).

## <a name="next-steps"></a>Próximas etapas

- [Simule o comportamento de entrada usando a ferramenta de What If de acesso condicional.](troubleshoot-conditional-access-what-if.md)
- [Use o modo somente de relatório para acesso condicional para determinar o impacto das novas decisões de política.](concept-conditional-access-report-only.md)
