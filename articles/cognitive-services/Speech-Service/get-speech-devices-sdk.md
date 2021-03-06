---
title: Obter SDK dos dispositivos de fala
titleSuffix: Azure Cognitive Services
description: O serviço de fala funciona com uma ampla variedade de dispositivos e fontes de áudio. Agora, você pode levar os aplicativos de fala para o próximo nível com hardware e software correspondentes. Neste artigo, você aprenderá a obter acesso ao SDK de dispositivos de fala e começar a desenvolver.
services: cognitive-services
author: erhopf
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 07/05/2019
ms.author: erhopf
ms.openlocfilehash: f8c1500dbbd9135a850e145199de8fea68cc4630
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79220529"
---
# <a name="get-the-cognitive-services-speech-devices-sdk"></a>Obter o SDK de Dispositivos de Fala dos Serviços Cognitivos

O SDK de dispositivos de fala é uma biblioteca predefinida projetada para funcionar com kits de desenvolvimento criados por finalidade e diversas configurações de matriz de microfone.

## <a name="choose-a-development-kit"></a>Escolha um kit de desenvolvimento

|Dispositivos|Especificação|DESCRIÇÃO|Cenários|
|--|--|--|--|
|[Kit de desenvolvimento de áudio inteligente Roobo](https://ddk.roobo.com)<br>[Setup](speech-devices-sdk-roobo-v1.md) / [início rápido](speech-devices-sdk-android-quickstart.md)![kit de desenvolvimento de áudio inteligente do Roobo](media/speech-devices-sdk/device-roobo-v1.jpg)|7 matriz do MIC, SOC do ARM, WIFI, saída de áudio, e/s. <br>[Android](speech-devices-sdk-android-quickstart.md)|O primeiro SDK de dispositivos de fala para adaptar a matriz MIC da Microsoft e o SDK de processamento frontal, para desenvolver cenários de transcrição e de fala de alta qualidade|Transcrição de conversa, palestrante inteligente, agente de voz, portátil|
|[Azure Kinect DK](https://azure.microsoft.com/services/kinect-dk/)<br>[Setup](https://docs.microsoft.com/azure/Kinect-dk/set-up-azure-kinect-dk) / [início rápido](speech-devices-sdk-windows-quickstart.md)![Azure Kinect DK](media/speech-devices-sdk/device-azure-kinect-dk.jpg)|7 a matriz MIC RGB e câmeras de profundidade. <br>[Windows](speech-devices-sdk-windows-quickstart.md)/[Linux](speech-devices-sdk-linux-quickstart.md)|Um kit de desenvolvedor com sensores de ia (inteligência artificial avançada) para a criação de modelos sofisticados de visão e fala de computadores. Ele combina uma melhor matriz de microfone espacial e uma câmera de profundidade com uma câmera de vídeo e um sensor de orientação, tudo em um dispositivo pequeno com vários modos, opções e SDKs para acomodar uma variedade de tipos de computação.|Transcrição de conversa, robótica, criação inteligente|
|Kit de desenvolvimento de áudio inteligente do Roobo 2<br>[Instalação](speech-devices-sdk-roobo-v2.md)<br>![kit de desenvolvimento de áudio inteligente do Roobo 2](media/speech-devices-sdk/device-roobo-v2.jpg)|7 matriz MIC, SOC do ARM, WIFI, Bluetooth, e/s. <br>Linux|O SDK de 2ª geração de dispositivos de fala que fornece um sistema operacional alternativo e mais recursos em um design de referência econômico.|Transcrição de conversa, palestrante inteligente, agente de voz, portátil|
|Placa de desenvolvimento URbetter T11![URbetter DDK](media/speech-devices-sdk/device-urbetter.jpg)|7 matriz MIC, SOC do ARM, WIFI, Ethernet, HDMI, câmera USB. <br>Linux|Um SDK de dispositivos de fala no nível do setor que adapta a matriz de Mic da Microsoft e dá suporte a e/s estendida, como HDMI/Ethernet e mais periféricos USB|Transcrição de conversa, educação, hospital, robôs, caixa OTT, agente de voz, unidade por meio|

## <a name="download-the-speech-devices-sdk"></a>Fazer download do SDK de Dispositivos de Fala

Baixe o [SDK dos dispositivos de fala](https://aka.ms/sdsdk-download).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Introdução ao SDK de Dispositivos de Fala](https://aka.ms/sdsdk-quickstart)
