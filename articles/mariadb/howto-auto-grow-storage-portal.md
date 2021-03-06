---
title: Aumento automático do armazenamento-portal do Azure-banco de dados do Azure para MariaDB
description: Este artigo descreve como você pode habilitar o armazenamento de crescimento automático para o banco de dados do Azure para MariaDB usando o portal do Azure
author: ambhatna
ms.author: ambhatna
ms.service: mariadb
ms.topic: conceptual
ms.date: 12/02/2019
ms.openlocfilehash: 5c5e9154260a255d9e9b8bc5775a479df7e41522
ms.sourcegitcommit: 6bb98654e97d213c549b23ebb161bda4468a1997
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74767493"
---
# <a name="auto-grow-storage-in-azure-database-for-mariadb-using-the-azure-portal"></a>Crescimento automático do armazenamento no banco de dados do Azure para MariaDB usando o portal do Azure
Este artigo descreve como você pode configurar um banco de dados do Azure para o armazenamento do MariaDB Server para crescer sem afetar a carga de trabalho.

Quando um servidor atinge o limite de armazenamento alocado, o servidor é marcado como somente leitura. No entanto, se você habilitar o crescimento automático do armazenamento, o armazenamento do servidor aumentará para acomodar os dados em crescimento. Para servidores com menos de 100 GB de armazenamento provisionado, o tamanho do armazenamento provisionado aumenta em 5 GB assim que o armazenamento livre está abaixo do maior que 1 GB ou 10% do armazenamento provisionado. Para servidores com mais de 100 GB de armazenamento provisionado, o tamanho de armazenamento provisionado aumenta em 5% quando o espaço livre de armazenamento está abaixo de 5% do tamanho de armazenamento provisionado. Os limites de armazenamento máximos conforme especificado [aqui](https://docs.microsoft.com/azure/mariadb/concepts-pricing-tiers#storage) se aplicam.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir este guia de instruções, você precisa:
- Um [banco de dados do Azure para servidor MariaDB](./quickstart-create-mariadb-server-database-using-azure-portal.md)

## <a name="enable-storage-auto-grow"></a>Habilitar crescimento automático de armazenamento 

Siga estas etapas para definir o crescimento automático do armazenamento do servidor MariaDB:

1. Na [portal do Azure](https://portal.azure.com/), selecione seu banco de dados do Azure existente para o servidor MariaDB.

2. Na página do servidor MariaDB, em título de **configurações** , clique em **tipo de preço** para abrir a página tipo de preço.

3. Na seção crescimento automático, selecione **Sim** para habilitar o crescimento automático do armazenamento.

    ![Banco de dados do Azure para MariaDB-Settings_Pricing_tier-aumento automático](./media/howto-auto-grow-storage-portal/3-auto-grow.png)

4. Clique em **OK** para salvar as alterações.

5. Uma notificação confirmará que o crescimento automático foi habilitado com êxito.

    ![Banco de dados do Azure para MariaDB-êxito no crescimento automático](./media/howto-auto-grow-storage-portal/5-auto-grow-successful.png)

## <a name="next-steps"></a>Próximos passos

Saiba mais sobre [como criar alertas sobre métricas](howto-alert-metric.md).
