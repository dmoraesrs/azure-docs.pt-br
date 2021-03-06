---
title: Enviar e receber mensagens AS2 para B2B
description: Trocar mensagens AS2 para cenários de integração corporativa B2B usando aplicativos lógicos do Azure com Enterprise Integration Pack
services: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, logicappspm
ms.topic: article
ms.date: 02/27/2020
ms.openlocfilehash: 0ce813e91750db3cdfa1e651a68fbb82d593eb32
ms.sourcegitcommit: 96dc60c7eb4f210cacc78de88c9527f302f141a9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77650548"
---
# <a name="exchange-as2-messages-for-b2b-enterprise-integration-in-azure-logic-apps-with-enterprise-integration-pack"></a>Trocar mensagens AS2 para Enterprise Integration B2B nos Aplicativos Lógicos do Azure com Enterprise Integration Pack

> [!IMPORTANT]
> O conector AS2 original está sendo preterido, portanto, certifique-se de usar o conector **AS2 (v2)** em vez disso. Essa versão fornece os mesmos recursos que a versão original, é nativa para o tempo de execução dos aplicativos lógicos e fornece melhorias significativas de desempenho em termos de taxa de transferência e tamanho da mensagem. Além disso, o conector v2 nativo não exige que você crie uma conexão com sua conta de integração. Em vez disso, conforme descrito em pré-requisitos, certifique-se de vincular sua conta de integração ao aplicativo lógico em que você planeja usar o conector.

Para trabalhar com mensagens AS2 em aplicativos lógicos do Azure, você pode usar o conector do AS2, que fornece gatilhos e ações para gerenciar a comunicação AS2. Por exemplo, para estabelecer a segurança e a confiabilidade ao transmitir mensagens, você pode usar estas ações:

* [Ação de **codificação AS2** ](#encode) para fornecer criptografia, assinatura digital e confirmações por meio de notificações de disposição de mensagem (MDN), que ajudam a dar suporte a não-repúdio. Por exemplo, essa ação aplica cabeçalhos AS2/HTTP e executa essas tarefas quando configurado:

  * Assina mensagens de saída.
  * Criptografa mensagens de saída.
  * Compacta a mensagem.
  * Transmite o nome do arquivo no cabeçalho MIME.

* [Ação de **decodificação AS2** ](#decode) para fornecer descriptografia, assinatura digital e confirmações por meio de notificações de disposição de mensagem (MDN). Por exemplo, essa ação executa estas tarefas:

  * Processa cabeçalhos AS2/HTTP.
  * Reconcilia o MDNs recebido com as mensagens de saída originais.
  * Atualiza e correlaciona registros no banco de dados de não-repúdio.
  * Grava registros para relatório de status AS2.
  * Gera o conteúdo da carga como codificado na base64.
  * Determina se MDNs são necessárias. Com base no contrato AS2, determina se MDNs deve ser síncrono ou assíncrono.
  * Gera MDNs síncronos ou assíncronos com base no contrato AS2.
  * Define os tokens de correlação e as propriedades em MDNs.

  Essa ação também executa essas tarefas quando configuradas:

  * Verifica a assinatura.
  * Descriptografa as mensagens.
  * Descompacta a mensagem.
  * Verificar e proibir duplicatas de ID de mensagem.

Este artigo mostra como adicionar as ações de codificação e decodificação AS2 a um aplicativo lógico existente.

## <a name="prerequisites"></a>Prerequisites

* Uma assinatura do Azure. Caso você ainda não tenha uma assinatura do Azure, [inscreva-se em uma conta gratuita do Azure](https://azure.microsoft.com/free/).

* O aplicativo lógico do qual você deseja usar o conector AS2 e um gatilho que inicia o fluxo de trabalho do aplicativo lógico. O conector do AS2 fornece apenas ações, não gatilhos. Se você não estiver familiarizado com os Aplicativos Lógicos, examine [O que são Aplicativos Lógicos do Azure](../logic-apps/logic-apps-overview.md) e [Início rápido: crie seu primeiro aplicativo lógico](../logic-apps/quickstart-create-first-logic-app-workflow.md).

* Uma [conta de integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) associada à sua assinatura do Azure e vinculada ao aplicativo lógico no qual você planeja usar o conector do AS2. O aplicativo lógico e a conta de integração devem existir no mesmo local ou na região do Azure.

* Pelo menos dois [parceiros comerciais](../logic-apps/logic-apps-enterprise-integration-partners.md) que você já definiu em sua conta de integração usando o qualificador de identidade AS2.

* Antes de usar o conector do AS2, você deve criar um [contrato](../logic-apps/logic-apps-enterprise-integration-agreements.md) AS2 entre seus parceiros comerciais e armazenar esse contrato em sua conta de integração.

* Se você usar [Azure Key Vault](../key-vault/key-vault-overview.md) para o gerenciamento de certificados, verifique se as chaves do cofre permitem as operações **criptografar** e **descriptografar** . Caso contrário, as ações de codificação e decodificação falharão.

  Na portal do Azure, vá para a chave no cofre de chaves, examine as **operações permitidas**da chave e confirme se as operações **criptografar** e **descriptografar** estão selecionadas, por exemplo:

  ![Verificar operações de chave do cofre](media/logic-apps-enterprise-integration-as2/key-vault-permitted-operations.png)

<a name="encode"></a>

## <a name="encode-as2-messages"></a>Codificar mensagens AS2

1. Se você ainda não fez isso, na [portal do Azure](https://portal.azure.com), abra seu aplicativo lógico no designer de aplicativo lógico.

1. No designer, adicione uma nova ação ao seu aplicativo lógico.

1. Em **Escolha uma ação** e na caixa de pesquisa, selecione **Todas**. Na caixa de pesquisa, digite "AS2 Encode" e certifique-se de selecionar a ação AS2 (v2): **codificação AS2**

   ![Selecione "codificação AS2"](./media/logic-apps-enterprise-integration-as2/select-as2-encode.png)

1. Agora, forneça informações para essas propriedades:

   | Propriedade | DESCRIÇÃO |
   |----------|-------------|
   | **Mensagem a ser codificada** | A carga da mensagem |
   | **AS2 de** | O identificador do remetente da mensagem conforme especificado pelo seu contrato AS2 |
   | **AS2 para** | O identificador do destinatário da mensagem, conforme especificado pelo seu contrato AS2 |
   |||

   Por exemplo:

   ![Propriedades de codificação de mensagem](./media/logic-apps-enterprise-integration-as2/as2-message-encoding-details.png)

> [!TIP]
> Se você tiver problemas ao enviar mensagens assinadas ou criptografadas, considere a possibilidade de experimentar diferentes formatos de algoritmo SHA256. A especificação AS2 não fornece nenhuma informação sobre formatos SHA256, de modo que cada provedor usa sua própria implementação ou formato.

<a name="decode"></a>

## <a name="decode-as2-messages"></a>Decodificar mensagens AS2

1. Se você ainda não fez isso, na [portal do Azure](https://portal.azure.com), abra seu aplicativo lógico no designer de aplicativo lógico.

1. No designer, adicione uma nova ação ao seu aplicativo lógico.

1. Em **Escolha uma ação** e na caixa de pesquisa, selecione **Todas**. Na caixa de pesquisa, insira "decodificação AS2" e certifique-se de selecionar a ação AS2 (v2): **decodificação AS2**

   ![Selecione "decodificação AS2"](media/logic-apps-enterprise-integration-as2/select-as2-decode.png)

1. Para a **mensagem a ser codificada** e as propriedades de **cabeçalhos de mensagem** , selecione esses valores de saídas anteriores de gatilho ou ação.

   Por exemplo, suponha que seu aplicativo lógico receba mensagens por meio de um gatilho de solicitação. Você pode selecionar as saídas desse gatilho.

   ![Selecione Corpo e Cabeçalhos de saídas de Solicitação](media/logic-apps-enterprise-integration-as2/as2-message-decoding-details.png)

## <a name="sample"></a>Amostra

Para tentar implantar um aplicativo lógico totalmente operacional e o cenário de AS2 de exemplo, confira o[modelo e cenário de aplicativo lógico AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="connector-reference"></a>Referência de conector

Para obter mais detalhes técnicos sobre esse conector, como ações e limites, conforme descrito pelo arquivo Swagger do conector, consulte a [página de referência do conector](https://docs.microsoft.com/connectors/as2/). 

> [!NOTE]
> Para aplicativos lógicos em um [ambiente do serviço de integração (ISE)](../logic-apps/connect-virtual-network-vnet-isolated-environment-overview.md), a versão original com rótulo do ISE do conector usa os [limites de mensagem do ISE](../logic-apps/logic-apps-limits-and-config.md#message-size-limits) em vez disso.

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre outros [conectores de Aplicativos Lógicos](../connectors/apis-list.md)
