---
title: Gerenciar os dispositivos no aplicativo Azure IoT Central | Microsoft Docs
description: Como um operador, saiba como gerenciar dispositivos no aplicativo Azure IoT Central.
author: sarahhubbard
ms.author: sahubbar
ms.date: 12/06/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: dfbfd65223ddad5e8a20958d62ef86b5aa16af43
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79271571"
---
# <a name="manage-devices-in-your-azure-iot-central-application"></a>Gerenciar dispositivos no aplicativo Azure IoT Central



Este artigo descreve como, como operador, gerenciar dispositivos no seu Microsoft IoT Central. Como um operador, você pode:

- Use a página **dispositivos** para exibir, adicionar e excluir dispositivos conectados ao seu aplicativo IOT central do Azure.
- Mantenha um inventário atualizado dos seus dispositivos.
- Mantenha os metadados do dispositivo atualizados alterando os valores armazenados nas propriedades do dispositivo de suas exibições.
- Controle o comportamento de seus dispositivos atualizando uma configuração em um dispositivo específico de suas exibições.

## <a name="view-your-devices"></a>Exibir dispositivos

Para exibir um dispositivo individual:

1. Escolha **dispositivos** no painel esquerdo. Aqui você vê uma lista de todos os dispositivos e de seus modelos de dispositivo.

1. Escolha um modelo de dispositivo.

1. No painel à direita da página **dispositivos** , você verá uma lista de dispositivos criados a partir desse modelo de dispositivo. Escolha um dispositivo individual para ver a página de detalhes do dispositivo para o dispositivo:

    ![Página Detalhes do Dispositivo](./media/howto-manage-devices/devicelist.png)


## <a name="add-a-device"></a>Adicionar um dispositivo

Para adicionar um dispositivo ao aplicativo Azure IoT Central:

1. Escolha **dispositivos** no painel esquerdo.

1. Escolha o modelo de dispositivo, a partir do qual você deseja criar um dispositivo.

1. Escolha + **Novo**.

1. Ativar ou **desativar** **a alternância** **simulada** . Um dispositivo real é para um dispositivo físico que você conecta ao aplicativo Azure IoT Central. Um dispositivo simulado tem dados de exemplo gerados a você pelo Azure IoT Central.

1. Clique em **Criar**.

1. Este dispositivo agora aparece na sua lista de dispositivos para este modelo. Selecione o dispositivo para ver a página de detalhes do dispositivo que contém todas as exibições do dispositivo.

## <a name="import-devices"></a>Importar dispositivos

Para conectar um grande número de dispositivos ao seu aplicativo, você pode importar em massa os dispositivos de um arquivo CSV. O arquivo CSV deve ter as seguintes colunas e cabeçalhos:

* **IOTC_DeviceID** – a ID do dispositivo deve estar toda em letras maiúsculas ou toda em letras minúsculas.
* **IOTC_DeviceName** – essa coluna é opcional.

Para dispositivos de registro em massa no aplicativo:

1. Escolha **dispositivos** no painel esquerdo.

1. No painel esquerdo, escolha o modelo de dispositivo para o qual você deseja criar os dispositivos em massa.

    > [!NOTE]
    > Se você ainda não tiver um modelo de dispositivo, poderá importar dispositivos em **todos os dispositivos** e registrá-los sem um modelo. Depois que os dispositivos tiverem sido importados, você poderá migrá-los para um modelo.

1. Selecione **Importar**.

    ![Ação Importar](./media/howto-manage-devices/bulkimport1a.png)


1. Selecione o arquivo CSV que contém a lista de IDs dos Dispositivos a serem importados.

1. A importação de dispositivo inicia assim que o arquivo é carregado. Você pode acompanhar o status da importação no painel de operações do dispositivo. Esse painel aparece automaticamente depois que a importação é iniciada ou você pode acessá-la por meio do ícone de sino no canto superior direito.

1. Quando a importação for concluída, uma mensagem de êxito será mostrada no painel operações do dispositivo.

    ![Importação com êxito](./media/howto-manage-devices/bulkimport3a.png)


Se a operação de importação de dispositivo falhar, você verá uma mensagem de erro no painel de operações do dispositivo. É gerado um arquivo de log captura todos os erros que você pode baixar.

**Migrando dispositivos para um modelo**

Se você registrar dispositivos iniciando a importação em **todos os dispositivos**, os dispositivos serão criados sem nenhuma associação de modelo de dispositivo. Os dispositivos devem estar associados a um modelo para explorar os dados e outros detalhes sobre o dispositivo. Siga estas etapas para associar dispositivos a um modelo:

1. Escolha **dispositivos** no painel esquerdo.

1. No painel esquerdo, escolha **todos os dispositivos**:

    ![Dispositivos não associados](./media/howto-manage-devices/unassociateddevices1a.png)


1. Use o filtro na grade para determinar se o valor na coluna de **modelo de dispositivo** é "não associado" para qualquer um de seus dispositivos.

1. Selecione os dispositivos que você deseja associar a um modelo:

1. Selecione **migrar**:

    ![Associar Dispositivos](./media/howto-manage-devices/unassociateddevices2a.png)


1. Escolha o modelo na lista de modelos disponíveis e selecione **migrar**.

1. Os dispositivos selecionados estão associados ao modelo de dispositivo que você escolheu.


## <a name="export-devices"></a>Exportar dispositivos

Para conectar um dispositivo real à IoT Central, você precisa de sua cadeia de conexão. Você pode exportar detalhes do dispositivo em massa para obter as informações necessárias para criar cadeias de conexão de dispositivo. O processo de exportação cria um arquivo CSV com a identidade do dispositivo, o nome do dispositivo e as chaves para todos os dispositivos selecionados.

Para exportar em massa os dispositivos do seu aplicativo:

1. Escolha **dispositivos** no painel esquerdo.

1. No painel esquerdo, escolha o modelo de dispositivo do qual você deseja exportar os dispositivos.

1. Selecione os dispositivos que você deseja exportar e, em seguida, selecione a ação **Exportar** .

    ![Exportação](./media/howto-manage-devices/export1a.png)


1. O processo de exportação tem início. Você pode acompanhar o status usando o painel de operações do dispositivo.

1. Quando a exportação for concluída, será mostrada uma mensagem com um link para baixar o arquivo gerado.

1. Selecione o link **baixar arquivo** para baixar o arquivo em uma pasta local no disco.

    ![Exportação bem-sucedida](./media/howto-manage-devices/export2a.png)


1. O arquivo CSV exportado contém as seguintes colunas: ID do dispositivo, nome do dispositivo, chaves de dispositivo e impressões digitais de certificado X509:

    * IOTC_DEVICEID
    * IOTC_DEVICENAME
    * IOTC_SASKEY_PRIMARY
    * IOTC_SASKEY_SECONDARY
    * IOTC_X509THUMBPRINT_PRIMARY
    * IOTC_X509THUMBPRINT_SECONDARY

Para obter mais informações sobre cadeias de conexão e conectar dispositivos reais ao seu aplicativo IoT Central, consulte [conectividade de dispositivo no IOT central do Azure](concepts-get-connected.md).

## <a name="delete-a-device"></a>Excluir um dispositivo

Para excluir um dispositivo real ou simulado do aplicativo Azure IoT Central:

1. Escolha **dispositivos** no painel esquerdo.

1. Escolha o modelo de dispositivo do dispositivo que você deseja excluir.

1. Use as ferramentas de filtro para filtrar e pesquisar seus dispositivos. Marque a caixa ao lado dos dispositivos a serem excluídos.

1. Clique em **Excluir**. Você pode acompanhar o status dessa exclusão no painel de operações do dispositivo.

## <a name="change-a-property"></a>Alterar uma propriedade

As propriedades de nuvem são os metadados de dispositivo associados ao dispositivo, como cidade e número de série. As propriedades graváveis controlam o comportamento de um dispositivo. Em outras palavras, elas permitem que você forneça entradas ao dispositivo.  As propriedades do dispositivo são definidas pelo dispositivo e são somente leitura no IoT Central. Você pode exibir e atualizar as propriedades nos modos de exibição de **detalhes** do dispositivo para seu dispositivo.

1. Escolha **dispositivos** no painel esquerdo.

1. Escolha o modelo de dispositivo do dispositivo cujas propriedades você deseja alterar e selecione o dispositivo de destino.

1. Escolha a exibição que contém as propriedades do seu dispositivo. essa exibição permite que você insira valores e selecione **salvar** na parte superior da página. Aqui você vê as propriedades que seu dispositivo tem e seus valores atuais. As propriedades de nuvem e as propriedades graváveis têm campos editáveis, enquanto as propriedades do dispositivo são somente leitura. Para propriedades graváveis, você pode ver o status de sincronização na parte inferior do campo. 

1. Modifique as propriedades para os valores necessários. Você pode modificar várias propriedades por vez e atualizá-las ao mesmo tempo.

1. Escolha **Salvar**. Se você salvou as propriedades graváveis, os valores serão enviados ao seu dispositivo. Quando o dispositivo confirma a alteração da propriedade Writeable, o status retorna de volta para **sincronizado**. Se você salvou uma propriedade de nuvem, o valor será atualizado.


## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como gerenciar dispositivos no aplicativo Azure IoT Central, a próxima etapa sugerida é apresentada:

> [!div class="nextstepaction"]
> [Como usar grupos de dispositivos](tutorial-use-device-groups.md)

<!-- Next how-tos in the sequence -->
