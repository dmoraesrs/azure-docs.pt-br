---
title: Acesso condicional-informações de segurança combinadas-Azure Active Directory
description: Criar uma política de acesso condicional personalizada para exigir um local confiável para o registro de informações de segurança
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 12/12/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb, rogoya
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c9b01cc06b3d0ef8f47b34e9ef86bec9adac03f
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75424845"
---
# <a name="conditional-access-require-trusted-location-for-mfa-registration"></a>Acesso condicional: exigir local confiável para o registro de MFA

A proteção de quando e como os usuários se registram para a autenticação multifator do Azure e a redefinição de senha de autoatendimento agora são possíveis com as ações do usuário na política de acesso condicional. Esse recurso de visualização está disponível para organizações que habilitaram a [visualização de registro combinado](../authentication/concept-registration-mfa-sspr-combined.md). Essa funcionalidade pode ser habilitada em organizações em que desejam usar condições como local de rede confiável para restringir o acesso ao registro para a autenticação multifator do Azure e o SSPR. Para obter mais informações sobre como criar locais confiáveis no acesso condicional, consulte o artigo [qual é a condição de local em Azure Active Directory acesso condicional?](../conditional-access/location-condition.md#named-locations)

## <a name="create-a-policy-to-require-registration-from-a-trusted-location"></a>Criar uma política para exigir o registro de um local confiável

A política a seguir se aplica a todos os usuários selecionados, que tentam se registrar usando a experiência de registro combinada e bloqueia o acesso, a menos que eles estejam se conectando de um local marcado como rede confiável.

1. Na **portal do Azure**, navegue até **Azure Active Directory** > **segurança** > **acesso condicional**.
1. Selecione **Nova política**.
1. Em nome, insira um nome para essa política. Por exemplo, o **registro de informações de segurança combinadas em redes confiáveis**.
1. Em **atribuições**, clique em **usuários e grupos**e selecione os usuários e grupos aos quais você deseja que essa política se aplique.

   > [!WARNING]
   > Os usuários devem estar habilitados para a [visualização de registro combinado](../authentication/howto-registration-mfa-sspr-combined.md).

1. Em **aplicativos de nuvem ou ações**, selecione **ações do usuário**, marque **registrar informações de segurança (versão prévia)** .
1. Em **condições** > **locais**.
   1. Configurar **Sim**.
   1. Inclua **qualquer local**.
   1. Exclua **todos os locais confiáveis**.
   1. Clique em **concluído** na folha locais.
   1. Clique em **concluído** na folha condições.
1. Em **controles de acesso** > **concessão**.
   1. Clique em **bloquear acesso**.
   1. Em seguida, clique em **Selecionar**.
1. Defina **Habilitar política** como **Ativado**.
1. Em seguida, clique em **Salvar**.

## <a name="next-steps"></a>Próximos passos

[Políticas comuns de acesso condicional](concept-conditional-access-policy-common.md)

[Determinar o impacto usando o modo somente relatório de acesso condicional](howto-conditional-access-report-only.md)

[Simular comportamento de entrada usando a ferramenta de What If de acesso condicional](troubleshoot-conditional-access-what-if.md)
