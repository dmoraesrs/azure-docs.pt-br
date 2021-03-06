---
title: 'Início rápido: criar, treinar e publicar a base de dados de conhecimento-QnA Maker'
description: É possível criar uma KB (base de dados de conhecimento) do QnA Maker com base no seu próprio conteúdo, como perguntas frequentes ou manuais de produto. Este artigo inclui um exemplo de como criar uma base de dados de conhecimento do QnA Maker com base em uma página da Web simples de perguntas frequentes para responder a perguntas sobre o QnA Maker.
ms.topic: conceptual
ms.date: 02/08/2020
ms.openlocfilehash: b1f80006e2dc72b5b623f4c29c093c734dc1efea
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79220573"
---
# <a name="quickstart-create-train-and-publish-your-qna-maker-knowledge-base"></a>Início rápido: criar, treinar e publicar sua base de dados de conhecimento QnA Maker

É possível criar uma KB (base de dados de conhecimento) do QnA Maker com base no seu próprio conteúdo, como perguntas frequentes ou manuais de produto. Este artigo inclui um exemplo de como criar uma base de dados de conhecimento do QnA Maker com base em uma página da Web simples de perguntas frequentes para responder a perguntas sobre o QnA Maker.

## <a name="prerequisites"></a>Prerequisites

> [!div class="checklist"]
> * Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.
> * Um [recurso](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker) do QnA Maker criado no portal do Azure. Lembre-se de sua ID e sua assinatura do Azure Active Directory, bem como do nome do recurso do QnA que você selecionou ao criar o recurso.

## <a name="create-your-first-qna-maker-knowledge-base"></a>Criar sua primeira base de dados de conhecimento do QnA Maker

1. Entre no portal [QnAMaker.ai](https://QnAMaker.ai) com suas credenciais do Azure.

1. No portal do QnA Maker, selecione **Criar uma base de dados de conhecimento**.

1. Na página **Criar**, pule a **Etapa 1** caso já tenha o recurso do QnA Maker.

    Se você ainda não criou o recurso, selecione **Criar um serviço do QnA**. Você será direcionado para o [portal do Azure](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker) para configurar o serviço do QnA Maker na sua assinatura. Lembre-se de sua ID e sua assinatura do Azure Active Directory, bem como do nome do recurso do QnA que você selecionou ao criar o recurso.

    Quando terminar de criar o recurso no portal do Azure, retorne ao portal do QnA Maker, atualize a página do navegador e prossiga para a **Etapa 2**.

1. Na **Etapa 3**, selecione a sua assinatura do Active Directory, o serviço (recurso) e o idioma para todas as bases de dados de conhecimento criadas no serviço.

   ![Captura de tela da seleção de uma base de dados de conhecimento do serviço do QnA Maker](../media/qnamaker-quickstart-kb/qnaservice-selection.png)

1. Na **Etapa 3**, dê à base de dados de conhecimento o nome **Minha Base de Dados de QnA de Exemplo**.

1. Na **Etapa 4**, defina as configurações com a seguinte tabela:

    |Configuração|Valor|
    |--|--|
    |**Habilitar a extração de vários turnos de URLs, arquivos .pdf ou .docx.**|Verificado|
    |**Texto de resposta padrão**| `Quickstart - default answer not found.`|
    |**+ Adicionar URL**|`https://docs.microsoft.com/azure/cognitive-services/qnamaker/troubleshooting`|
    |**Bate-papo**|Selecione **Professional**|

1. Na **Etapa 5**, selecione **Criar sua base de dados**.

    O processo de extração leva alguns instantes para ler o documento e identificar perguntas e respostas.

    Depois que o QnA Maker criar com êxito a base de dados de conhecimento, a página **Base de dados de conhecimento** será aberta. Você pode editar o conteúdo da base de dados de conhecimento nesta página.

## <a name="add-a-new-question-and-answer-set"></a>Adicionar um novo par de pergunta e resposta

1. No portal do QnA Maker, na página **Editar**, selecione **+ Adicionar par de P e R** na barra de ferramentas de contexto.
1. Adicione a seguinte pergunta:

    `How many Azure services are used by a knowledge base?`

1. Adicione a resposta formatada com _Markdown_:

    ` * Azure QnA Maker service\n* Azure Cognitive Search\n* Azure web app\n* Azure app plan`

    ![ Adicione a pergunta como texto e a resposta formatada com Markdown.](../media/qnamaker-create-publish-knowledge-base/add-question-and-answer.png)

    O símbolo de Markdown, `*`, é usado para marcadores. O `\n` é usado para uma nova linha.

    A página **Editar** mostra o Markdown. Quando você usar o painel **Testar** posteriormente, verá o Markdown exibido corretamente.

## <a name="save-and-train"></a>Salvar e treinar

No canto superior direito, selecione **Salvar e treinar** para salvar as edições e treinar o QnA Maker. As edições não serão mantidas se não forem salvas.

## <a name="test-the-knowledge-base"></a>Testar a base de dados de conhecimento

1. No portal do QnA Maker, selecione **Testar** para verificar se as alterações entraram em vigor.
1. Insira um exemplo de consulta de usuário na caixa de texto.

    `How many Azure services are used by a knowledge base?`

    ![ Insira um exemplo de consulta de usuário na caixa de texto. ](../media/qnamaker-create-publish-knowledge-base/test-panel-in-qna-maker.png)

1. Selecione **Inspecionar** para examinar a resposta mais detalhadamente. A janela de teste é usada para testar as alterações na base de dados de conhecimento antes que ela seja publicada.

1. Selecione **Testar** novamente para fechar o painel **Testar**.

## <a name="publish-the-knowledge-base"></a>Publicar a base de dados de conhecimento

Ao publicar uma base de dados de conhecimento, o conteúdo da base de dados de conhecimento é movido do índice `test` para um índice `prod` no Azure Search.

![Captura de tela da movimentação do conteúdo de sua base de dados de conhecimento](../media/qnamaker-how-to-publish-kb/publish-prod-test.png)

1. No portal do QnA Maker, selecione **Publicar**. Para confirmar, selecione **Publicar** na página.

    O serviço do QnA Maker foi publicado com êxito. É possível usar o ponto de extremidade no aplicativo ou código de bot.

    ![Captura de tela da publicação bem-sucedida](../media/qnamaker-create-publish-knowledge-base/publish-knowledge-base-to-endpoint.png)

## <a name="create-a-bot"></a>Criar um bot

Após a publicação, é possível criar um bot na página **Publicar**:

* Você pode criar vários bots rapidamente, todos apontando para a mesma base de dados conhecimento para diferentes regiões ou planos de preço para os bots individuais.
* Se você quiser apenas um bot para a base de dados de conhecimento, use o link **Exibir todos os bots no portal do Azure** para exibir uma lista de seus bots atuais.

Quando você faz alterações na base de dados de conhecimento e republica, não é necessário fazer mais nada com o bot. Ele já está configurado para trabalhar com a base de dados de conhecimento e trabalha com todas as alterações futuras na base de dados de conhecimento. Sempre que você publica uma base de dados de conhecimento, todos os bots conectados a ela são atualizados automaticamente.

1. No portal do QnA Maker, na página **Publicar**, selecione **Criar bot**. Esse botão será exibido somente depois que você tiver publicado a base de dados de conhecimento.

    ![Captura de tela da criação de um bot](../media/qnamaker-create-publish-knowledge-base/create-bot-from-published-knowledge-base-page.png)

1. É aberta uma nova guia do navegador para o portal do Azure com a página de criação do Serviço de Bot do Azure. Configure o serviço de bot do Azure. O bot e o QnA Maker podem compartilhar o plano do serviço de aplicativo Web, mas não podem compartilhar o aplicativo Web. Isso significa que o **nome do aplicativo** para o bot deve ser diferente do nome do aplicativo usado para o serviço do QnA Maker.

    * **Deve ser feito**
        * Alterar o identificador de bot se ele não for exclusivo.
        * Selecionar a linguagem de programação do SDK. Depois que o bot for criado, você poderá baixar o código em seu ambiente de desenvolvimento local e continuar o processo de desenvolvimento.
    * **Não deve ser feito**
        * Alterar as configurações a seguir no portal do Azure ao criar o bot. Elas são preenchidas previamente para sua base de dados de conhecimento existente:
           * Chave de autenticação do QnA
           * Plano e local do serviço de aplicativo


1. Depois que o bot for criado, abra o recurso **Serviço de bot**.
1. Em **Gerenciamento de Bot**, selecione **Testar no Webchat**.
1. No prompt de chat de **Digite sua mensagem**, digite:

    `Azure services?`

    O chatbot responde com uma resposta de sua base de dados de conhecimento.

    ![Insira uma consulta de usuário no Webchat de teste.](../media/qnamaker-create-publish-knowledge-base/test-web-chat.png)

## <a name="what-did-you-accomplish"></a>O que você realizou?

Você criou uma base de dados de conhecimento, adicionou uma URL pública à base de dados de conhecimento, adicionou seu conjunto do QnA, treinou, testou e publicou a base de dados de conhecimento.

Depois de publicar a base de dados de conhecimento, você criou e testou um bot.

Isso tudo foi feito em alguns minutos, sem a necessidade de escrever nenhum código nem de limpar o conteúdo.

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não for prosseguir para o próximo início rápido, exclua os recursos do QnA Maker e do Bot Framework no portal do Azure.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Adicionar perguntas com metadados](add-question-metadata-portal.md)

Para mais informações:

* [Formato de Markdown nas respostas](../reference-markdown-format.md)
* [Fontes de dados](../concepts/knowledge-base.md) do QnA Maker.


