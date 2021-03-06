---
title: Usar o Portal do Azure para criar um Hub IoT | Microsoft Docs
description: Como criar, gerenciar e excluir Hubs IoT do Azure por meio do Portal do Azure. Inclui informações sobre tipos de preço, escala, segurança e configurações de mensagens.
author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: robinsh
ms.openlocfilehash: c43c142b22709d42416b2dd14dfc78812970916a
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79284727"
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a>Criar um Hub IoT usando o portal do Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Este artigo descreve como criar e gerenciar hubs IoT usando o [portal do Azure](https://portal.azure.com).

Para usar as etapas neste tutorial, você precisa de uma assinatura do Azure. Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="create-an-iot-hub"></a>Crie um hub IoT

[!INCLUDE [iot-hub-include-create-hub](../../includes/iot-hub-include-create-hub.md)]

## <a name="change-the-settings-of-the-iot-hub"></a>Alterar as configurações do Hub IoT

Você poderá alterar as configurações de um Hub IoT existente depois que ele for criado no painel Hub IoT.

![Captura de tela mostrando as configurações do Hub IoT](./media/iot-hub-create-through-portal/iot-hub-settings-panel.png)

Aqui estão algumas das propriedades que você pode definir para um hub IoT:

**Preço e escala**: você pode usar essa propriedade para migrar para uma camada diferente ou definir o número de unidades do Hub IoT. 

**Monitoramento de operações**: ative ou desative as diferentes categorias de monitoramento, como registro em log para eventos relacionados a mensagens de dispositivo para nuvem ou mensagens de nuvem para dispositivo.

**Filtro de IP**: especifique um intervalo de endereços IP que serão aceitos ou rejeitados pelo Hub IoT.

**Propriedades**: fornece a lista de propriedades que você pode copiar e usar em outros lugares, como ID de recurso, grupo de recursos, local e assim por diante.

### <a name="shared-access-policies"></a>Políticas de acesso compartilhado

Você também pode exibir ou modificar a lista de políticas de acesso compartilhado clicando em **Políticas de acesso compartilhado** na seção **Configurações**. Essas políticas definem as permissões para que dispositivos e serviços se conectem ao Hub IoT. 

Clique em **Adicionar** para abrir a folha **Adicionar uma política de acesso compartilhado**.  Você poderá inserir o nome da nova política e as permissões que quer associar a essa política, como mostrado na seguinte figura:

![Captura de tela mostrando a adição de uma política de acesso compartilhado](./media/iot-hub-create-through-portal/iot-hub-add-shared-access-policy.png)

* As políticas **Leitura do Registro** e **Gravação do Registro** concedem direitos de acesso de leitura e de gravação registro de identidade. Essas permissões são usadas pelos serviços de nuvem de back-end para gerenciar identidades de dispositivo. A escolha da opção de gravação escolhe automaticamente a opção de leitura.

* A política de **conexão de serviço** concede permissão para acessar pontos de extremidade de serviço. Essa permissão é usada pelos serviços de nuvem de back-end para enviar e receber mensagens de dispositivos, bem como para atualizar e ler dados de dispositivo e do módulo.

* A política **Conectar dispositivo** concede permissões para enviar e receber mensagens usando os pontos de extremidade do lado do dispositivo do Hub IoT. Essa permissão é usada pelos dispositivos para enviar e receber mensagens de um hub IoT, atualizar e ler os dados do dispositivo e do módulo e executar carregamentos de arquivos.

Clique em **Criar** para adicionar essa política recém-criada à lista existente.

Para obter informações mais detalhadas sobre o acesso concedido por permissões específicas, consulte [permissões do Hub IOT](./iot-hub-devguide-security.md#iot-hub-permissions).

## <a name="register-a-new-device-in-the-iot-hub"></a>Registrar um novo dispositivo no hub IoT

[!INCLUDE [iot-hub-include-create-device](../../includes/iot-hub-include-create-device.md)]

## <a name="message-routing-for-an-iot-hub"></a>Roteamento de Mensagem para um hub IoT

Clique em **Roteamento de Mensagens** em **Mensagens** para ver o painel de Roteamento de Mensagens, no qual você define rotas e pontos de extremidade personalizados para o hub. [Roteamento de mensagens](iot-hub-devguide-messages-d2c.md) permite que você gerencie como os dados são enviados de seus dispositivos para seus pontos de extremidade. A primeira etapa é adicionar uma nova rota. Em seguida, você pode adicionar um ponto de extremidade existente à rota ou criar um novo dos tipos compatíveis, como Armazenamento de Blobs. 

![Painel de roteamento de mensagem](./media/iot-hub-create-through-portal/iot-hub-message-routing.png)

### <a name="routes"></a>Rotas

Rotas é a primeira guia no painel Roteamento de Mensagens. Para adicionar uma nova rota, clique em +**Adicionar**. Você verá a tela a seguir. 

![Captura de tela mostrando a adição de uma nova rota](./media/iot-hub-create-through-portal/iot-hub-add-route-storage-endpoint.png)

Dê um nome a seu hub. O nome deve ser exclusivo dentro da lista de rotas para o hub. 

Para **Ponto de Extremidade**, você pode selecionar um na lista suspensa ou adicionar um novo. Neste exemplo, uma conta de armazenamento e o contêiner já estão disponíveis. Para adicioná-los como um ponto de extremidade, clique em +**Adicionar** ao lado da lista suspensa Ponto de Extremidade e selecione **Armazenamento de Blobs**. A tela a seguir mostra o local em que a conta de armazenamento e o contêiner são especificados.

![Captura de tela mostrando a adição de um ponto de extremidade de armazenamento para a regra de roteamento](./media/iot-hub-create-through-portal/iot-hub-routing-add-storage-endpoint.png)

Clique em **Escolher um contêiner** para selecionar a conta de armazenamento e o contêiner. Quando você tiver selecionado esses campos, ele retornará para o painel do Ponto de Extremidade. Use os padrões para o restante dos campos e **Criar** para criar o ponto de extremidade da conta de armazenamento e adicioná-lo às regras de roteamento.

Para **Fonte de dados**, selecione Mensagens de Telemetria do Dispositivo. 

Em seguida, adicione uma consulta de roteamento. Neste exemplo, as mensagens que têm uma propriedade de aplicativo chamada `level` com um valor igual a `critical` são roteadas para a conta de armazenamento.

![Captura de tela mostrando como salvar uma nova regra de roteamento](./media/iot-hub-create-through-portal/iot-hub-add-route.png)

Clique em **Salvar** para salvar a regra de roteamento. Você retorna ao painel de Roteamento de Mensagens e a nova regra de roteamento é exibida.

### <a name="custom-endpoints"></a>Pontos de extremidade personalizados

Clique na guia **pontos de extremidade personalizados** . Você verá todos os pontos de extremidade personalizados já criados. Daqui, você pode adicionar novos pontos de extremidade ou excluir pontos de extremidade existentes. 

> [!NOTE]
> Se você excluir uma rota, não serão excluídos os pontos de extremidade atribuídos a ela. Para excluir um ponto de extremidade, clique na guia Pontos de extremidade personalizados, selecione o ponto de extremidade que você deseja excluir e clique em Excluir.
>

Você pode ler mais sobre pontos de extremidade personalizados em [Referência - Pontos de extremidade do Hub IoT](iot-hub-devguide-endpoints.md).

Você pode definir até 10 pontos de extremidade personalizados para o Hub IoT. 

Para ver um exemplo completo de como usar pontos de extremidade personalizados com o roteamento, veja [Roteamento de mensagem com o Hub IoT](tutorial-routing.md).

## <a name="find-a-specific-iot-hub"></a>Localize um hub IoT específico

Aqui estão duas maneiras de localizar um hub IoT específico em sua assinatura:

1. Se você souber a qual grupo de recursos o hub IoT pertence, clique em **Grupos de recursos** e selecione o grupo de recursos na lista. A tela de grupo de recursos mostra todos os recursos nesse grupo, incluindo os hubs IoT. Clique no hub que você está procurando.

2. Clique em **Todos os recursos**. No painel **Todos os recursos**, há uma lista suspensa que assume `All types` como padrão. Clique na lista suspensa e desmarque a opção `Select all`. Localize `IoT Hub` e verifique-o. Clique na caixa de listagem suspensa para fechá-la, e as entradas serão filtradas, mostrando apenas seus hubs IoT.

## <a name="delete-the-iot-hub"></a>Excluir o Hub IoT

Para excluir um hub IoT, localize o hub IoT que você deseja excluir e, em seguida, clique no botão **Excluir** abaixo do nome do hub IoT.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o gerenciamento do Hub IoT do Azure, siga estes links:

* [Roteamento de mensagem com o Hub IoT](tutorial-routing.md)
* [Métricas do IoT Hub](iot-hub-metrics.md)
* [Monitoramento de operações](iot-hub-operations-monitoring.md)