---
title: Suporte a contêiner
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: IEvangelist
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 10/07/2019
ms.author: dapine
ms.openlocfilehash: 2cb2cfbdfbac5d496f109d85977b41a050766ab0
ms.sourcegitcommit: c22327552d62f88aeaa321189f9b9a631525027c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73499094"
---
## <a name="create-an-computer-vision-resource"></a>Criar um recurso de Pesquisa Visual Computacional

1. Faça logon no [Portal do Azure](https://portal.azure.com).
1. Clique em [criar **Pesquisa Visual computacional** ](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesComputerVision) recurso.
1. Insira todas as configurações necessárias:

    |Configuração|Valor|
    |--|--|
    |Nome|Nome desejado (2-64 caracteres)|
    |Assinatura|Selecione a assinatura apropriada|
    |Localização|Selecione qualquer local próximo e disponível|
    |Camada de preços|`F0`-o tipo de preço mínimo|
    |Grupo de recursos|Selecionar um grupo de recursos disponível|

1. Clique em **criar** e aguarde até que o recurso seja criado. Após a criação, navegue até a página de recursos.
1. Coletar `{ENDPOINT_URI}` e `{API_KEY}`configurados, consulte [coletando parâmetros necessários](../computer-vision-how-to-install-containers.md#gathering-required-parameters) para obter detalhes.
