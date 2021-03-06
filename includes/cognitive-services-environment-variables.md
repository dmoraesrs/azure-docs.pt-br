---
author: aahill
ms.service: cognitive-services
ms.topic: include
ms.date: 06/24/2019
ms.author: aahi
ms.openlocfilehash: 367ae27a6afec803d2e3f98f54bdcf852330ddc6
ms.sourcegitcommit: 32242bf7144c98a7d357712e75b1aefcf93a40cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70274648"
---
## <a name="configure-an-environment-variable-for-authentication"></a>Configurar uma variável de ambiente para autenticação

Os aplicativos precisam autenticar o acesso aos serviços cognitivas que eles usam. Para autenticar, é recomendável criar uma variável de ambiente para armazenar as chaves para os recursos do Azure. 

Depois de ter sua chave, grave-a em uma nova variável de ambiente no computador local que executa o aplicativo. Para definir a variável de ambiente, abra uma janela de console e siga as instruções do seu sistema operacional. Substitua `your-key` por uma das chaves do recurso.

#### <a name="windowstabwindows"></a>[Windows](#tab/windows)

```console
setx COGNITIVE_SERVICE_KEY "your-key"
```

Depois de adicionar a variável de ambiente, talvez seja necessário reiniciar todos os programas em execução que precisarem ler a variável de ambiente, incluindo a janela do console. Por exemplo, se estiver usando o Visual Studio como seu editor, reinicie-o antes de executar o exemplo.

#### <a name="linuxtablinux"></a>[Linux](#tab/linux)

```bash
export COGNITIVE_SERVICE_KEY=your-key
```

Depois de adicionar a variável de ambiente, execute `source ~/.bashrc` a partir da janela de console para que as alterações entrem em vigor.

#### <a name="macostabunix"></a>[macOS](#tab/unix)

Edite seu .bash_profile e adicione a variável de ambiente:

```bash
export COGNITIVE_SERVICE_KEY=your-key
```

Depois de adicionar a variável de ambiente, execute `source .bash_profile` a partir da janela de console para que as alterações entrem em vigor.

***