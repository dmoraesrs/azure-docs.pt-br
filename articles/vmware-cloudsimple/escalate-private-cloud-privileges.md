---
title: Escalonar privilégios de nuvem privada da AVS-solução VMware do Azure por AVS
description: Descreve como escalonar privilégios em sua nuvem privada de AVS para funções administrativas no vCenter
titleSuffix: Azure VMware Solutions (AVS)
author: sharaths-cs
ms.author: b-shsury
ms.date: 06/05/2019
ms.topic: article
ms.service: azure-vmware-cloudsimple
ms.reviewer: cynthn
manager: dikamath
ms.openlocfilehash: 211960af359e19f93afef58162c5b09ae1d9b23f
ms.sourcegitcommit: 21e33a0f3fda25c91e7670666c601ae3d422fb9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2020
ms.locfileid: "77025309"
---
# <a name="escalate-avs-private-cloud-vcenter-privileges-from-the-avs-portal"></a>Escalonar privilégios de vCenter da nuvem privada da AVS no portal da AVS

Para ter acesso administrativo à sua nuvem privada de AVS privado, você pode escalonar temporariamente seus privilégios de AVS. Usando privilégios elevados, você pode instalar soluções VMware, adicionar fontes de identidade e gerenciar usuários.

Novos usuários podem ser criados no domínio de SSO do vCenter e recebem acesso ao vCenter. Ao criar novos usuários, adicione-os aos grupos internos da AVS para acessar o vCenter. Para obter mais informações, consulte [modelo de permissão de nuvem privada da AVS do VMware vCenter](https://docs.azure.cloudsimple.com/learn-private-cloud-permissions/).

> [!CAUTION]
> Não faça nenhuma alteração de configuração para os componentes de gerenciamento. As ações executadas durante o estado de privilégio escalonado podem afetar negativamente o sistema ou podem fazer com que o sistema fique indisponível.

## <a name="sign-in-to-azure"></a>Entrar no Azure

Entre no Portal do Azure em [https://portal.azure.com](https://portal.azure.com).

## <a name="escalate-privileges"></a>Escalonar privilégios

1. Acesse o [portal da AVS](access-cloudsimple-portal.md).

2. Abra a página **recursos** , selecione a nuvem privada AVS para a qual você deseja escalonar privilégios.

3. Próximo à parte inferior da página Resumo em **alterar privilégios de vSphere**, clique em **escalar**.

    ![Alterar o privilégio de vSphere](media/escalate-private-cloud-privilege.png)

4. Selecione o tipo de usuário vSphere. Somente `CloudOwner@cloudsimple.local` usuário local pode ser escalonado.

5. Selecione o intervalo de tempo de escalonamento na lista suspensa. Escolha o período mais curto que permitirá que você conclua a tarefa.

6. Marque a caixa de seleção para confirmar que você entendeu os riscos.

    ![Caixa de diálogo escalar privilégio](media/escalate-private-cloud-privilege-dialog.png)

7. Clique em **OK**.

8. O processo de escalonamento pode levar alguns minutos. Ao concluir, clique em **OK**.

O escalonamento de privilégios começa e dura até o final do intervalo selecionado. Você pode entrar em seu vCenter de nuvem privada da AVS para realizar tarefas administrativas.

> [!IMPORTANT]
> Somente um usuário pode ter privilégios escalonados. Você deve desescalonar os privilégios do usuário antes de poder escalonar os privilégios de outro usuário.

> [!CAUTION]
> Novos usuários devem ser adicionados somente a *Cloud-Owner-Group*, *Cloud-global-cluster-admin-Group*, *Cloud-Global-Storage-admin-Group*, *Cloud-Global-Network-admin-Group* ou, *Cloud-global-VM-admin-Group*.  Os usuários adicionados ao grupo de *Administradores* serão removidos automaticamente.  Somente as contas de serviço devem ser adicionadas ao grupo de *Administradores* e as contas de serviço não devem ser usadas para entrar na interface do usuário da Web do amvSphere.

## <a name="extend-privilege-escalation"></a>Estender elevação de privilégio

Se precisar de mais tempo para concluir suas tarefas, você poderá estender o período de escalonamento de privilégios. Escolha o intervalo de tempo de escalonamento adicional que permite que você conclua as tarefas administrativas.

1. Nos **recursos** > **nuvens privadas da AVS** no portal da AVS, selecione a nuvem privada da AVS para a qual você deseja estender o escalonamento de privilégios.

2. Próximo à parte inferior da guia Resumo, clique em **estender elevação de privilégio**.

    ![Estender elevação de privilégio](media/de-escalate-private-cloud-privilege.png)

3. Selecione um intervalo de tempo de escalonamento na lista suspensa. Examine a nova hora de término do escalonamento.

4. Clique em **salvar** para estender o intervalo.

## <a name="de-escalate-privileges"></a>Desescalonamento de privilégios

Depois que suas tarefas administrativas forem concluídas, você deverá desescalonar seus privilégios. 

1. Nos **recursos** > **nuvens privadas da AVS** no portal da AVS, selecione a nuvem privada da AVS para a qual você deseja desescalonar privilégios.

2. Clique em **desescalonamento**.

3. Clique em **OK**.

> [!IMPORTANT]
> Para evitar erros, saia do vCenter e entre novamente depois de desescalonamento de privilégios.

## <a name="next-steps"></a>Próximos passos

* [Configurar fontes de identidade do vCenter para usar Active Directory](https://docs.azure.cloudsimple.com/set-vcenter-identity/)
* Instalar solução de backup para [fazer backup de máquinas virtuais de carga de trabalho](https://docs.azure.cloudsimple.com/backup-workloads-veeam/)