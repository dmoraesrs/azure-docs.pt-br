---
title: Exemplo do PowerShell – listar informações estendidas para aplicativos de proxy de aplicativo
description: Exemplo do PowerShell que lista todos os aplicativos de proxy de aplicativo Azure Active Directory (Azure AD) junto com a ID do aplicativo (AppId), Name (DisplayName), URL externa (ExternalUrl), URL interna (InternalUrl) e tipo de autenticação ( ExternalAuthenticationType).
services: active-directory
author: msmimart
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 12/05/2019
ms.author: mimart
ms.reviewer: japere
ms.collection: M365-identity-device-management
ms.openlocfilehash: f58de8c081dbb0323a2d9638777e29d879172072
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75482134"
---
# <a name="get-all-application-proxy-apps-and-list-extended-information"></a>Obter todos os aplicativos de proxy de aplicativo e listar informações estendidas

Este exemplo de script do PowerShell lista informações sobre todos os aplicativos de proxy de aplicativo Azure Active Directory (Azure AD), incluindo a ID do aplicativo (AppId), Name (DisplayName), URL externa (ExternalUrl), URL interna (InternalUrl) e tipo de autenticação (ExternalAuthenticationType).

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az](../../../../includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Este exemplo requer o [módulo AzureAD v2 PowerShell for Graph](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0) (AzureAD) ou o [PowerShell do AzureAD v2 para a versão de visualização do módulo do Graph](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0-preview) (AzureADPreview).

## <a name="sample-script"></a>Exemplo de script

[!code-azurepowershell[main](~/powershell_scripts/application-proxy/get-all-appproxy-apps-extended.ps1 "Get all Application Proxy apps")]

## <a name="script-explanation"></a>Explicação sobre o script

| Comando | Observações |
|---|---|
|[Get-AzureADServicePrincipal](https://docs.microsoft.com/powershell/module/azuread/get-azureadserviceprincipal?view=azureadps-2.0) | Obtém uma entidade de serviço. |
|[Get-AzureADApplication](https://docs.microsoft.com/powershell/module/azuread/get-azureadapplication?view=azureadps-2.0) | Obtém um aplicativo do Azure AD. |
|[Get-AzureADApplicationProxyApplication](https://docs.microsoft.com/powershell/module/azuread/get-azureadapplicationproxyapplication?view=azureadps-2.0) | Recupera um aplicativo configurado para o proxy de aplicativo no Azure AD. |

## <a name="next-steps"></a>Próximos passos

Para obter mais informações sobre o módulo do PowerShell do Azure AD, consulte [visão geral do módulo do PowerShell do Azure ad](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

Para obter outros exemplos do PowerShell para o proxy de aplicativo, consulte [exemplos do PowerShell do Azure ad para azure proxy de aplicativo do AD](../application-proxy-powershell-samples.md).