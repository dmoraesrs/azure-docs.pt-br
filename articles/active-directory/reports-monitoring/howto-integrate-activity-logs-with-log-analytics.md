---
title: Transmitir logs de Azure Active Directory para Azure Monitor logs | Microsoft Docs
description: Saiba como integrar logs de Azure Active Directory com logs de Azure Monitor
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 2c3db9a8-50fa-475a-97d8-f31082af6593
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 04/18/2019
ms.author: markvi
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: 213fb6e73ae2fc4314320d0e3e593632d8eb7f85
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79266436"
---
# <a name="integrate-azure-ad-logs-with-azure-monitor-logs"></a>Integrar logs do Azure AD com logs de Azure Monitor

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-log-analytics-rebrand.md)]

Os logs do Azure Monitor permitem consultar os dados para localizar eventos em particular, analisar tendências e executar a correlação entre várias fontes de dados. Com a integração do logs de atividade do Azure AD nos logs do Azure Monitor, agora você pode executar tarefas como:

 * Comparar os logs de entrada do dos logs de assinatura do Azure Active Directory mediante os logs de segurança pela Central de Segurança do Azure

 * Solucionar problemas de gargalos de desempenho na página de entrada do seu aplicativo, correlacionando os dados de desempenho de aplicativo do Aplicativo Azure Insights.  

O vídeo de uma sessão do Ignite a seguir demonstra os benefícios do uso de logs do Azure Monitor para logs do Azure AD em cenários práticos de usuários.

> [!VIDEO https://www.youtube.com/embed/MP5IaCTwkQg?start=1894]

Neste artigo, você aprenderá a integrar os logs do Azure Active Directory (Azure AD) ao Azure Monitor.

## <a name="supported-reports"></a>Relatórios com suporte

Você pode rotear os logs de atividade de auditoria e logs de atividade de entrada para logs do Azure Monitor para análise posterior. 

* **Logs de auditoria**: o [relatório de atividade dos logs de auditoria](concept-audit-logs.md) dá acesso ao histórico de todas as tarefas executadas em seu locatário.
* **Logs de entrada**: com o [relatório de atividades de entrada](concept-sign-ins.md), você pode determinar quem realizou as tarefas indicadas pelo relatório das trilhas de auditoria.

> [!NOTE]
> Não há suporte para logs de atividades de auditoria e entradas relacionados ao B2C no momento.
>

## <a name="prerequisites"></a>Prerequisites 

Para usar esse recurso, você precisa de:

* Uma assinatura do Azure. Se não tiver uma assinatura do Azure, você poderá [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/free/).
* Um locatário do Azure AD.
* Um usuário que seja *administrador global* ou *administrador de segurança* do locatário do Azure AD.
* Um espaço de trabalho do Log Analytics em sua assinatura do Azure. Saiba como [criar um espaço de trabalho do Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

## <a name="send-logs-to-azure-monitor"></a>Enviar logs para Azure Monitor

1. Entre no [portal do Azure](https://portal.azure.com). 

2. Selecione as configurações do **Azure Active Directory** > **Diagnostic** -> **Adicionar configuração de diagnóstico**. Você também pode selecionar a página**Exportar Configurações** dos **Logs de Auditoria** ou **Assinaturas** para obter a página de configuração de configurações de diagnóstico.  
    
3. No menu **Configurações de Diagnóstico**, marque a caixa de seleção **Enviar para o espaço de trabalho do Log Analytics** e, em seguida, selecione **Configurar**.

4. Selecione o espaço de trabalho do Log Analytics para enviar os logs ou criar um novo espaço de trabalho na caixa de diálogo fornecida.  

5. Siga um destes procedimentos, ou ambos:
    * Para enviar os logs de auditoria para o espaço de trabalho do Log Analytics, selecione a caixa de seleção **AuditLogs**. 
    * Para enviar logs de entrada para o espaço de trabalho do Log Analytics, selecione a caixa de seleção **SignInLogs**.

6. Clique em **Salvar** para salvar a configuração.

    ![Configurações de diagnóstico](./media/howto-integrate-activity-logs-with-log-analytics/Configure.png)

7. Após cerca de 15 minutos, verifique se que os eventos são transmitidos para seu espaço de trabalho do Log Analytics.

## <a name="next-steps"></a>Próximas etapas

* [Analisar logs de atividade do Azure AD com os logs do Azure Monitor](howto-analyze-activity-logs-log-analytics.md)
* [Instalar e usar os modos de exibição do Log Analytics do Azure Active Directory](howto-install-use-log-analytics-views.md)