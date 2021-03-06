---
title: Usar o Java para criar uma sala de chat com o Azure Functions e o Serviço do SignalR
description: Um início rápido para usar o Azure SignalR Service e o Azure Functions para criar uma sala de chat.
author: sffamily
ms.service: signalr
ms.devlang: java
ms.topic: quickstart
ms.date: 03/04/2019
ms.author: zhshang
ms.openlocfilehash: 890fc381afe0146e721e084e2dcd7eae9215d004
ms.sourcegitcommit: c2065e6f0ee0919d36554116432241760de43ec8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2020
ms.locfileid: "77083210"
---
# <a name="quickstart-use-java-to-create-a-chat-room-with-azure-functions-and-signalr-service"></a>Início Rápido: Usar o Java para criar uma sala de chat com o Azure Functions e o Serviço do SignalR

O Serviço do Azure SignalR permite que você adicione funcionalidades em tempo real ao seu aplicativo com facilidade, e o Azure Functions é uma plataforma sem servidor que permite que você execute o código sem gerenciar nenhuma infraestrutura. Neste início rápido, você usará o Java para criar um aplicativo de chat em tempo real, sem servidor, usando o Serviço do SignalR e o Functions.

## <a name="prerequisites"></a>Pré-requisitos

- Um editor de códigos, como o [Visual Studio Code](https://code.visualstudio.com/)
- Uma conta do Azure com uma assinatura ativa. [Crie uma conta gratuitamente](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).
- [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools#installing). Usado para executar os aplicativos de funções do Azure localmente.

   > [!NOTE]
   > Só há suporte para as associações do Serviço do SignalR necessárias em Java no Azure Functions Core Tools versão 2.4.419 (versão do host 2.0.12332) ou superior.

   > [!NOTE]
   > Para instalar extensões, o Azure Functions Core Tools exige o [SDK do .NET Core](https://www.microsoft.com/net/download) instalado. No entanto, não é necessário nenhum conhecimento do .NET para criar aplicativos do Azure Functions no JavaScript.

- [Java Developer Kit](https://www.azul.com/downloads/zulu/), versão 8
- [Apache Maven](https://maven.apache.org), versão 3.0 ou posterior

> [!NOTE]
> Este início rápido pode ser executado no macOS, Windows ou Linux.

## <a name="log-in-to-azure"></a>Fazer logon no Azure

Entre no portal do Azure em <https://portal.azure.com/> com sua conta do Azure.

[!INCLUDE [Create instance](includes/signalr-quickstart-create-instance.md)]

[!INCLUDE [Clone application](includes/signalr-quickstart-clone-application.md)]

## <a name="configure-and-run-the-azure-function-app"></a>Configurar e executar o aplicativo do Azure Functions

1. No navegador em que o portal do Azure é aberto, confirme se a instância do SignalR Service implantada anteriormente foi criada com êxito pesquisando pelo nome na caixa de pesquisa na parte superior do portal. Selecione a instância para abri-la.

    ![Pesquisar a instância do SignalR Service](media/signalr-quickstart-azure-functions-csharp/signalr-quickstart-search-instance.png)

1. Selecione **Chaves** para exibir as cadeias de conexão para a instância do SignalR Service.

1. Selecione e copie a cadeia de conexão primária.

    ![Criar Serviço SignalR](media/signalr-quickstart-azure-functions-javascript/signalr-quickstart-keys.png)

1. No editor de códigos, abra a pasta *src/chat/java* no repositório clonado.

1. Renomeie *local.settings.sample.json* como *local.settings.json*.

1. Em **local.settings.json**, cole a cadeia de conexão no valor da configuração **AzureSignalRConnectionString**. Salve o arquivo.

1. O arquivo principal que contém as funções está em *src/chat/java/src/main/java/com/function/Functions.java*:

    - **negociar** – usa a associação de entrada *SignalRConnectionInfo* para gerar e retornar informações de conexão válidas.
    - **sendMessage** – recebe uma mensagem de chat no corpo da solicitação e usa a associação de saída *SignalR* para difundir a mensagem a todos os aplicativos cliente conectados.

1. No terminal, verifique se você está na pasta *src/chat/java*. Compile o aplicativo de funções.

    ```bash
    mvn clean package
    ```

1. Execute o aplicativo de funções localmente.

    ```bash
    mvn azure-functions:run
    ```

[!INCLUDE [Run web application](includes/signalr-quickstart-run-web-application.md)]

[!INCLUDE [Cleanup](includes/signalr-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você criou e executou um aplicativo sem servidor em tempo real usando o Maven. Em seguida, saiba mais sobre como criar Azure Functions em Java do zero.

> [!div class="nextstepaction"]
> [Criar sua primeira função com Java e Maven](../azure-functions/functions-create-first-java-maven.md)