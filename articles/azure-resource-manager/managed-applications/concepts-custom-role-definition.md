---
title: Visão geral das definições de função personalizadas
description: Descreve o conceito de criação de definições de função personalizadas para aplicativos gerenciados.
ms.topic: conceptual
ms.author: jobreen
author: jjbfour
ms.date: 09/16/2019
ms.openlocfilehash: 88e42fd9626276f6c77b46b33c138407f91d06ca
ms.sourcegitcommit: f788bc6bc524516f186386376ca6651ce80f334d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75650754"
---
# <a name="custom-role-definition-artifact-in-azure-managed-applications"></a>Artefato de definição de função personalizada em aplicativos gerenciados do Azure

A definição de função personalizada é um artefato opcional em aplicativos gerenciados. Ele é usado para determinar quais permissões o aplicativo gerenciado precisa para executar suas funções.

Este artigo fornece uma visão geral do artefato de definição de função personalizada e seus recursos.

## <a name="custom-role-definition-artifact"></a>Artefato de definição de função personalizada

Você precisa nomear o artefato de definição de função personalizada customRoleDefinition. JSON. Coloque-o no mesmo nível que createUiDefinition. JSON e MainTemplate. JSON no pacote. zip que cria uma definição de aplicativo gerenciado. Para saber como criar o pacote. zip e publicar uma definição de aplicativo gerenciado, consulte [publicar uma definição de aplicativo gerenciado.](publish-managed-app-definition-quickstart.md)

## <a name="custom-role-definition-schema"></a>Esquema de definição de função personalizada

O arquivo customRoleDefinition. JSON tem uma propriedade de `roles` de nível superior que é uma matriz de funções. Essas funções são as permissões que o aplicativo gerenciado precisa para funcionar. Atualmente, somente funções internas são permitidas, mas você pode especificar várias funções. Uma função pode ser referenciada pela ID da definição de função ou pelo nome da função.

Exemplo de JSON para definição de função personalizada:

```json
{
    "contentVersion": "0.0.0.1",
    "roles": [
        {
            "properties": {
                "roleName": "Contributor"
            }
        },
        {
            "id": "acdd72a7-3385-48ef-bd42-f606fba81ae7"
        },
        {
            "id": "/providers/Microsoft.Authorization/roledefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
        }
    ]
}
```

## <a name="roles"></a>Funções

Uma função é composta por um `$.properties.roleName` ou um `id`:

```json
{
    "id": null,
    "properties": {
        "roleName": "Contributor"
    }
}
```

> [!NOTE]
> Você pode usar o campo `id` ou `roleName`. Apenas uma é necessária. Esses campos são usados para pesquisar a definição de função que deve ser aplicada. Se ambos forem fornecidos, o campo `id` será usado.

|Propriedade|Obrigatório?|Description|
|---------|---------|---------|
|id|Sim|A ID da função interna. Você pode usar a ID completa ou apenas o GUID.|
|roleName|Sim|O nome da função interna.|