---
author: IEvangelist
ms.service: cognitive-services
ms.subservice: speech-service
ms.date: 01/27/2020
ms.topic: include
ms.author: dapine
zone_pivot_groups: programming-languages-set-two
ms.openlocfilehash: 724f52317ce2afda023ae0514a330da0032e8710
ms.sourcegitcommit: 668b3480cb637c53534642adcee95d687578769a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78924807"
---
## <a name="prerequisites"></a>Pré-requisitos

Antes de começar:

* <a href="~/articles/cognitive-services/Speech-Service/quickstarts/setup-platform.md" target="_blank">Instale o SDK de Fala para seu ambiente de desenvolvimento e crie um projeto de exemplo vazio<span class="docon docon-navigate-external x-hidden-focus"></span></a>.

## <a name="create-a-luis-app-for-intent-recognition"></a>Criar um aplicativo LUIS para reconhecimento de intenção

[!INCLUDE [Create a LUIS app for intent recognition](../luis-sign-up.md)]

## <a name="open-your-project"></a>Abrir o projeto

1. Abra seu IDE preferencial.
2. Crie um projeto e um arquivo chamado `quickstart.py`, que você deve abrir em seguida.

## <a name="start-with-some-boilerplate-code"></a>Comece com código de texto clichê

Vamos adicionar um código que funciona como um esqueleto para o projeto.

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=5-7)]

## <a name="create-a-speech-configuration"></a>Criar uma configuração de Fala

Antes de inicializar um objeto `IntentRecognizer`, é preciso criar uma configuração que use a chave e o local do recurso de previsão do LUIS.

Insira este código em `quickstart.py`. Atualize estes valores:

* Substitua `"YourLanguageUnderstandingSubscriptionKey"` pela sua chave de previsão do LUIS.
* Substitua `"YourLanguageUnderstandingServiceRegion"` pelo seu local do LUIS. Use o **Identificador de região** da [região](https://aka.ms/speech/sdkregion) correta

>[!TIP]
> Se precisar de ajuda para encontrar esses valores, confira [Criar um aplicativo LUIS para reconhecimento de intenção](#create-a-luis-app-for-intent-recognition).

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=12)]

A amostra constrói o objeto `SpeechConfig` usando a chave e a região LUIS. Para ver uma lista completa dos métodos disponíveis, confira a [Classe SpeechConfig](https://docs.microsoft.com/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech.speechconfig).

O SDK de Fala usará como padrão o reconhecimento do uso de en-us como o idioma; confira [Especificar o idioma de origem para conversão de fala em texto](../../../../how-to-specify-source-language.md) para obter informações sobre como escolher o idioma de origem.

## <a name="initialize-an-intentrecognizer"></a>Inicializar um IntentRecognizer

Agora, vamos criar um `IntentRecognizer`. Insira esse código logo abaixo da configuração de fala.

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=15)]

## <a name="add-a-languageunderstandingmodel-and-intents"></a>Adicione um LanguageUnderstandingModel e as Intenções

Você precisa associar um `LanguageUnderstandingModel` ao reconhecedor de intenção e adicionar as intenções que deseja reconhecer. Vamos usar as intenções do domínio predefinido para a automação doméstica.

Insira este código abaixo de seu `IntentRecognizer`. Substitua `"YourLanguageUnderstandingAppId"` pela ID do aplicativo LUIS. 

>[!TIP]
> Se precisar de ajuda para encontrar esse valor, confira [Criar um aplicativo LUIS para reconhecimento de intenção](#create-a-luis-app-for-intent-recognition).

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=19-27)]

## <a name="recognize-an-intent"></a>Reconhecer uma intenção

No objeto `IntentRecognizer`, chame o método `recognize_once()`. Esse método permite que o Serviço de Fala saiba que você está enviando uma única expressão para reconhecimento e permite parar o reconhecimento, assim que a frase é identificada.

Insira este código abaixo de seu modelo.

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=35)]

## <a name="display-the-recognition-results-or-errors"></a>Exibir os resultados do reconhecimento (ou os erros)

Quando o Serviço de Fala retornar o resultado do reconhecimento, você poderá utilizá-lo. Para manter a simplicidade, vamos imprimir o resultado no console.

Abaixo da chamada para `recognize_once()`, adicione este código.

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=38-47)]

## <a name="check-your-code"></a>Verificar o código

Neste momento, seu código deverá ter a seguinte aparência.

> [!NOTE]
> Adicionamos alguns comentários a esta versão.

[!code-python[](~/samples-cognitive-services-speech-sdk/quickstart/python/intent-recognition/quickstart.py?range=5-47)]

## <a name="build-and-run-your-app"></a>Compilar e executar o aplicativo

Execute a amostra no console ou no IDE:

```
python quickstart.py
```

Os próximos 15 segundos de entrada de fala do microfone serão reconhecidos e registrados na janela do console.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [footer](./footer.md)]
