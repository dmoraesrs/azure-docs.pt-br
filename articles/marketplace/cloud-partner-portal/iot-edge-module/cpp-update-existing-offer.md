---
title: Atualizar uma oferta de módulo de Azure IoT Edge existente | Azure Marketplace
description: Atualizar uma oferta de módulo do IoT Edge existente no Azure Marketplace.
services: Azure, Marketplace, Cloud Partner Portal,
author: dan-wesley
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: article
ms.date: 10/18/2018
ms.author: pabutler
ms.openlocfilehash: cd0167e1af5bf8ef667df88237d83e9f33ed41f9
ms.sourcegitcommit: ac56ef07d86328c40fed5b5792a6a02698926c2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73813388"
---
# <a name="update-an-existing-iot-edge-module-offer"></a>Atualizar uma oferta de módulo do IoT Edge existente

Este artigo percorre os diferentes aspectos da atualização de sua oferta de módulo do IoT Edge no [Portal do Cloud Partner](https://cloudpartner.azure.com/) e, em seguida, republicar a oferta.

Há várias razões por que você talvez queira atualizar sua oferta, tais como:

-  Adicionar uma nova versão de imagem de módulo do IoT Edge para SKUs existentes.
-  Adicionando novo SKUs.
-  Atualizar os metadados do mercado para a oferta ou SKUs individuais.

Para ajudá-lo nessas modificações, o portal oferece os recursos **Comparar** e **Histórico**.  


## <a name="unpermitted-changes-to-iot-edge-module-offer-or-sku"></a>Alterações não permitidas na oferta de módulo do IoT Edge ou SKU

Há atributos de uma oferta de módulo IoT Edge ou SKU que não pode ser alterado depois que a oferta está ativa no Azure Marketplace. Você não pode alterar as configurações a seguir:

-  **ID da oferta** e **ID do Publicador** da oferta
-  **ID da SKU** de SKUs existentes
-  Marcas de versão, por exemplo: `1.0.1`
-  Alterações no modelo de cobrança/licença para SKUs existentes

## <a name="common-update-operations"></a>Operações comuns de atualização

As operações de inserção e atualização são comuns.

### <a name="update-the-iot-edge-module-image-version-for-a-sku"></a>Atualizar a versão de imagem do módulo do IoT Edge para uma SKU

É comum que uma imagem de módulo IoT Edge seja atualizada periodicamente com patches de segurança, recursos adicionais e assim por diante. Nesse cenário, você deseja atualizar a imagem de módulo do IoT Edge que faz referência a sua SKU usando as seguintes etapas:

1.  Entrar no [Portal do Cloud Partner](https://cloudpartner.azure.com/).

2.  Em **Todas as ofertas**, localize a oferta que você gostaria de atualizar.

3.  Na guia **SKUs**, clique na SKU associada à imagem do módulo do IoT Edge para atualizar.

4.  Em **Imagem do módulo do Edge**, selecione **+ Nova versão da imagem** para adicionar uma nova imagem de módulo do IoT Edge.

5.  Forneça as versões da imagem do módulo **do IoT Edge**. A versão da imagem precisa seguir as mesmas diretrizes de marcas como versões anteriores. As marcas de versão devem estar no formato X.Y.Z, onde X, Y e Z são inteiros. Verifique se a nova versão que você fornecer seja maior que todas as versões anteriores.

6.  Clique em **Publicar** para iniciar o fluxo de trabalho para publicar sua nova versão do IoT Edge para o Azure Marketplace.

### <a name="add-a-new-sku"></a>Adicionar uma nova SKU

Use as etapas a seguir para disponibilizar uma nova SKU para sua oferta existente: 

1.  Entrar no [Portal do Cloud Partner](https://cloudpartner.azure.com/).

2.  Em **Todas as ofertas**, localize a oferta que você gostaria de atualizar.

3.  Na guia **SKUs**, selecione **Adicionar nova SKU** e forneça uma **ID DE SKU** na janela pop-up.

4.  Republique o módulo IoT Edge usando as etapas descritas em [publicar um módulo IOT Edge no Azure Marketplace](./cpp-publish-offer.md).

5.  Selecione **Publicar** para iniciar o fluxo de trabalho para publicar a sua nova SKU.


### <a name="update-offer-marketplace-metadata"></a>Atualizar metadados do marketplace da oferta

Utilize os seguintes passos para atualizar os metadados do mercado associados à sua oferta. (por exemplo: nome da empresa, logotipos, etc.)

1.  Entrar no [Portal do Cloud Partner](https://cloudpartner.azure.com/).

2.  Em **Todas as ofertas**, localize a oferta que você gostaria de atualizar.

3.  Vá para a guia **Marketplace** . Use as instruções no artigo [publicar um módulo IOT Edge no Azure Marketplace](./cpp-publish-offer.md) para fazer alterações de metadados.

4.  Selecione **Publicar** para iniciar o fluxo de trabalho para publicar suas alterações.

## <a name="compare-feature"></a>Comparar recursos

Quando você fizer alterações em uma oferta publicada, você pode usar o recurso **Comparar** para auditar as alterações feitas. 

**Para usar o recurso de comparação:**

1.  A qualquer momento do processo de edição, clique no botão **Comparar** para sua oferta.

    ![Comparar o botão de recurso](./media/iot-edge-module-compare.png)


2.  Veja as versões lado a lado de metadados e ativos de marketing.


## <a name="history-of-publishing-actions"></a>Histórico de ações de publicação

Para ver a atividade de histórico de publicação, selecione a guia **Histórico** na barra de menu de navegação esquerda do Portal do Cloud Partner. Você pode ver as ações de data/hora executadas durante o tempo de vida das ofertas do Marketplace do Azure.  <!-- Need to find correct link here:  legal time windowsFor more information, see [History page](cpp-history-page.md) -->
