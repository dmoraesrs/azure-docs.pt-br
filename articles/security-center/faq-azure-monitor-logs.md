---
title: Perguntas frequentes sobre a central de segurança do Azure-perguntas sobre o MMAs existente
description: Essas perguntas FREQUENTEs respondem a perguntas para clientes que já usam o Microsoft Monitoring Agent e considerando a central de segurança do Azure, um produto que ajuda você a prevenir, detectar e responder a ameaças.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/25/2020
ms.author: memildin
ms.openlocfilehash: 5c433140c3982813e372fd3f63243a96197d220c
ms.sourcegitcommit: 747a20b40b12755faa0a69f0c373bd79349f39e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77661882"
---
# Perguntas frequentes para clientes que já estão usando logs de Azure Monitor<a name="existingloganalyticscust"></a>

## <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>A Central de Segurança substitui todas as conexões existentes entre as VMs e os workspaces?

Se uma VM já tiver o Microsoft Monitoring Agent instalado como uma extensão do Azure, a Central de Segurança não substituirá a conexão do workspace existente. Em vez disso, a Central de Segurança usará o workspace existente. A VM será protegida desde que a solução "segurança" ou "SecurityCenterFree" tenha sido instalada no espaço de trabalho para o qual está se comunicando. 

Uma solução da central de segurança é instalada no espaço de trabalho selecionado na tela de coleta de dados, se ainda não estiver presente, e a solução será aplicada somente às VMs relevantes. Quando você adiciona uma solução, ela é implantada automaticamente por padrão em todos os agentes do Windows e Linux conectados ao seu espaço de trabalho do Log Analytics. [Direcionamento de Solução](../operations-management-suite/operations-management-suite-solution-targeting.md) permite a aplicação de um escopo às suas soluções.

> [!TIP]
> Se o Microsoft Monitoring Agent for instalado diretamente na VM (não como uma extensão do Azure), a central de segurança não instalará o Microsoft Monitoring Agent e o monitoramento de segurança será limitado.

## <a name="does-security-center-install-solutions-on-my-existing-log-analytics-workspaces-what-are-the-billing-implications"></a>A Central de Segurança instala soluções em meus workspaces existentes do Log Analytics? Quais são as implicações de cobrança?
Quando a Central de Segurança identificar que uma VM já está conectada a um workspace que você criou, a Central de Segurança habilitará as soluções neste workspace de acordo com seu tipo de preço. As soluções são aplicadas apenas às VMs do Azure relevantes, por meio do [direcionamento de solução](../operations-management-suite/operations-management-suite-solution-targeting.md), portanto, a cobrança permanece igual.

- **Camada gratuita** – A Central de Segurança instala a solução 'SecurityCenterFree' no workspace. Você não será cobrado pela camada gratuita.
- **Camada Standard**: a Central de Segurança instala a solução 'Security' no workspace.

   ![Soluções no workspace padrão](./media/security-center-platform-migration-faq/solutions.png)

## <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a>Eu já tenho workspaces em meu ambiente, posso usá-los para coletar dados de segurança?
Se uma VM já tiver o Microsoft Monitoring Agent instalado como uma extensão do Azure, a Central de Segurança usará o workspace existente conectado. Uma solução da Central de Segurança será instalado no workspace, se ainda não estiver presente, e a solução será aplicada apenas às VMs relevantes por meio do [direcionamento de solução](../operations-management-suite/operations-management-suite-solution-targeting.md).

Quando a Central de Segurança instala o Microsoft Monitoring Agent em VMs, ela usa os workspaces padrão criados pela Central de Segurança.

## <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a>Já tenho a solução de segurança em meus workspaces. Quais são as implicações de cobrança?
A solução de auditoria de & de segurança é usada para habilitar recursos da camada Standard da central de segurança para VMs do Azure. Se a solução de Segurança e Auditoria já estiver instalada em um workspace, a Central de Segurança usará a solução existente. Não há nenhuma alteração na cobrança.