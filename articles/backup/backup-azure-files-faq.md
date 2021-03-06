---
title: Perguntas frequentes sobre fazer backup de Arquivos do Azure
description: Neste artigo, descubra respostas para perguntas comuns sobre como proteger seus compartilhamentos de arquivo do Azure com o serviço de Backup do Azure.
ms.date: 07/29/2019
ms.topic: conceptual
ms.openlocfilehash: c69d4642aefbd599d3783dcdfa059a0cd9d129d9
ms.sourcegitcommit: f915d8b43a3cefe532062ca7d7dbbf569d2583d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78302535"
---
# <a name="questions-about-backing-up-azure-files"></a>Perguntas sobre como fazer backup de Arquivos do Azure

Este artigo responde perguntas frequentes sobre como fazer backup de Arquivos do Azure. Em algumas das respostas, há links para artigos com informações abrangentes. Você também pode postar perguntas sobre o serviço de Backup do Azure no [fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

Para verificar rapidamente as seções neste artigo, use os links à direita, em **Neste artigo**.

## <a name="configuring-the-backup-job-for-azure-files"></a>Configurando o trabalho de backup para Arquivos do Azure

### <a name="why-cant-i-see-some-of-my-storage-accounts-i-want-to-protect-that-contain-valid-azure-file-shares"></a>Por que não consigo ver algumas das minhas contas de armazenamento que desejo proteger e que contêm compartilhamentos de arquivo do Azure válidos?

Durante a versão prévia, o backup de compartilhamentos de arquivos do Azure não dá suporte a todos os tipos de contas de armazenamento. Consulte a lista de [aqui](troubleshoot-azure-files.md#limitations-for-azure-file-share-backup-during-preview) para ver a lista de Contas de Armazenamento com suporte. Também é possível que a Conta de Armazenamento que você está procurando esteja já protegida ou registrada com outro Cofre. [Cancelar o registro](troubleshoot-azure-files.md#configuring-backup) do cofre para descobrir a Conta de Armazenamento em outros Cofres para proteção.

### <a name="why-cant-i-see-some-of-my-azure-file-shares-in-the-storage-account-when-im-trying-to-configure-backup"></a>Por que não vejo alguns dos meus compartilhamentos de arquivos do Azure na conta de armazenamento quando estou tentando configurar o backup?

Verifique se o compartilhamento de arquivos do Azure já está protegido no mesmo cofre dos Serviços de Recuperação ou se foi excluído recentemente.

### <a name="can-i-protect-file-shares-connected-to-a-sync-group-in-azure-files-sync"></a>Posso proteger compartilhamentos de arquivos conectados a um grupo de sincronização na Sincronização de arquivos do Azure?

Sim. A proteção dos compartilhamentos de arquivos do Azure conectados a grupos de sincronização está habilitada e faz parte da versão prévia pública.

### <a name="when-trying-to-back-up-file-shares-i-clicked-on-a-storage-account-for-discovering-the-file-shares-in-it-however-i-did-not-protect-them-how-do-i-protect-these-file-shares-with-any-other-vault"></a>Ao tentar fazer backup de compartilhamentos de arquivos, cliquei em uma Conta de Armazenamento para ver os compartilhamentos de arquivos que estão nela. No entanto, eu não os protegi. Como fazer para proteger esses compartilhamentos de arquivos com outro Cofre?

Ao tentar fazer backup, a seleção de uma Conta de Armazenamento para ver os compartilhamentos de arquivos dentro dela gera o registro da Conta de Armazenamento no Cofre em que isso foi feito. Se você optar por proteger os compartilhamentos de arquivos com um cofre diferente, [Cancele o registro](troubleshoot-azure-files.md#configuring-backup) da Conta de Armazenamento escolhida no Cofre.

### <a name="can-i-change-the-vault-to-which-i-back-up-my-file-shares"></a>É possível alterar o Cofre em que faço backup dos meus compartilhamentos de arquivos?

Sim. No entanto, você precisará [interromper a proteção em um compartilhamento de arquivos](manage-afs-backup.md#stop-protection-on-a-file-share) do cofre conectado, [cancelar o registro](troubleshoot-azure-files.md#configuring-backup) dessa conta de armazenamento e, em seguida, protegê-la de um cofre diferente.

### <a name="in-which-geos-can-i-back-up-azure-file-shares"></a>Em quais áreas geográficas posso fazer backup de compartilhamentos de arquivo do Azure?

O backup para compartilhamentos de arquivos do Azure está atualmente em versão prévia e está disponível apenas nas áreas geográficas abaixo:

- Leste da Austrália (AE)
- Sudeste da Austrália (ASE)
- Sul do Brasil (BRS)
- Canadá Central (CNC)
- Leste do Canadá (CE)
- Central dos EUA (CUS)
- Leste da Ásia (EA)
- Leste dos EUA (EUS)
- Leste dos EUA 2 (EUS2)
- Leste do Japão (JPE)
- Oeste do Japão (JPW)
- Índia Central (INC)
- Sul da Índia (INS)
- Coreia Central (KRC)
- Sul da Coreia (KRS)
- Centro-Norte dos EUA (NCUS)
- Norte da Europa (NE)
- Centro-Sul dos EUA (SCUS)
- Sudeste da Ásia (SEA)
- Sul do Reino Unido (UKS)
- Oeste do Reino Unido (UKW)
- Europa Ocidental (WE)
- Oeste dos EUA (WUS)
- Centro-Oeste dos EUA (WCUS)
- Oeste dos EUA 2 (WUS 2)
- US Gov – Arizona (UGA)
- US Gov – Texas (UGT)
- US Gov – Virgínia (UGV)
- Central da Austrália (ACL)
- Índia ocidental (INW)
- Norte da África do Sul (SAN)
- Norte dos EAU (UAN)
- França central (FRC)
- Norte da Alemanha (GN)                       
- Centro-oeste da Alemanha (GWC)
- Oeste da África do Sul (visto)
- EAU Central (UAC)
- NÉ (leste da Noruega)     
- NWW (oeste da Noruega)
- SZN (Norte da Suíça)

Escreva para [AskAzureBackupTeam@microsoft.com](mailto:askazurebackupteam@microsoft.com) caso precise usá-lo em uma área geográfica específica que não esteja listada acima.

### <a name="how-many-azure-file-shares-can-i-protect-in-a-vault"></a>Quantos compartilhamentos de arquivos do Azure posso proteger em um cofre?

Durante a versão prévia, é possível proteger compartilhamentos de arquivos do Azure de até 50 contas de armazenamento por cofre. Também é possível proteger até 200 compartilhamentos de arquivos do Azure em um único cofre.

### <a name="can-i-protect-two-different-file-shares-from-the-same-storage-account-to-different-vaults"></a>Posso proteger dois compartilhamentos de arquivo diferentes da mesma conta de armazenamento em cofres diferentes?

Não. Os compartilhamentos de arquivos em uma mesma Conta de Armazenamento só podem ser protegidos pelo mesmo Cofre.

## <a name="backup"></a>Backup

### <a name="how-many-scheduled-backups-can-i-configure-per-file-share"></a>Quantos backups agendados é possível configurar por compartilhamento de arquivo?

No momento, o Backup do Azure é compatível com a configuração de backups agendados uma vez por dia do Compartilhamento de Arquivos do Azure.

### <a name="how-many-on-demand-backups-can-i-take-per-file-share"></a>Quantos backups sob demanda posso ter por compartilhamento de arquivo?

Você pode ter até 200 instantâneos para um compartilhamento de arquivos a qualquer hora. O limite inclui instantâneos tirados pelo Backup do Azure conforme definido pela sua política. Se os backups começarem a falhar após atingir o limite, exclua pontos de restauração sob demanda para ter êxito nos backups futuros.

## <a name="restore"></a>Restauração

### <a name="can-i-recover-from-a-deleted-azure-file-share"></a>Posso recuperar a partir de um compartilhamento de arquivos do Azure excluído?

Quando um compartilhamento de arquivos do Azure é excluído, você vê a lista de backups que serão excluídos e uma solicitação de confirmação. Um compartilhamento de arquivos do Azure excluído não pode ser restaurado.

### <a name="can-i-restore-from-backups-if-i-stopped-protection-on-an-azure-file-share"></a>Posso restaurar a partir de backups se parar a proteção em um compartilhamento de arquivos do Azure?

Sim. Caso tenha escolhido **Reter Dados de Backup**, ao parar a proteção, você poderá restaurar a partir de todos os pontos de restauração existentes.

### <a name="what-happens-if-i-cancel-an-ongoing-restore-job"></a>O que acontecerá se eu cancelar um trabalho de restauração em andamento?

Se um trabalho de restauração em andamento for cancelado, o processo de restauração será interrompido e todos os arquivos restaurados antes do cancelamento permanecerão no destino configurado (local original ou alternativo) sem nenhuma reversão.

## <a name="manage-backup"></a>Gerenciar backups

### <a name="can-i-use-powershell-to-configuremanagerestore-backups-of-azure-file-shares"></a>Posso usar o PowerShell para configurar/gerenciar/restaurar backups de compartilhamentos de Arquivos do Azure?

Sim. Consulte a documentação detalhada [aqui](backup-azure-afs-automation.md)

### <a name="can-i-access-the-snapshots-taken-by-azure-backups-and-mount-it"></a>Posso acessar os instantâneos tirados por Backups do Azure e montá-los?

Todos os instantâneos tirados pelo Backup do Azure podem ser acessados pelas opções Exibir Instantâneos no portal, PowerShell ou CLI. Para saber mais sobre instantâneos de compartilhamento de arquivos do Azure, consulte [Visão geral de instantâneos de compartilhamento de arquivos do Azure (versão prévia)](../storage/files/storage-snapshots-files.md).

### <a name="what-is-the-maximum-retention-i-can-configure-for-backups"></a>Qual é a retenção máxima que posso configurar para backups?

O backup para compartilhamentos de arquivos do Azure oferece a capacidade de configurar políticas com retenção de até 180 dias. No entanto, usando a [opção "Backup sob demanda" no PowerShell](backup-azure-afs-automation.md#trigger-an-on-demand-backup), você pode manter um ponto de recuperação até mesmo por 10 anos.

### <a name="what-happens-when-i-change-the-backup-policy-for-an-azure-file-share"></a>O que acontece quando altero a política de backup de um compartilhamento de arquivos do Azure?

Quando uma nova política for aplicada em compartilhamento de arquivos, a agenda e a retenção da nova política serão seguidas. Se a retenção for estendida, os pontos de recuperação existentes serão marcados para mantê-los de acordo com a nova política. Se a retenção for reduzida, eles são marcados para remoção no próximo trabalho de limpeza e excluídos.

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

Para saber mais sobre outras áreas do Backup do Azure, confira algumas destas outras perguntas frequentes sobre backups:

- [Perguntas Frequentes sobre o cofre dos Serviços de Recuperação](backup-azure-backup-faq.md)
- [Perguntas frequentes sobre o backup de VM do Azure](backup-azure-vm-backup-faq.md)
- [Perguntas frequentes sobre o agente de Backup do Azure](backup-azure-file-folder-backup-faq.md)
