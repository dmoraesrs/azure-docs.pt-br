---
title: Conectar-se ao Azure Cosmos DB usando o Compass
description: Saiba como usar o MongoDB Compass para armazenar e gerenciar dados no Azure Cosmos DB.
ms.service: cosmos-db
ms.subservice: cosmosdb-mongo
ms.topic: conceptual
ms.date: 06/24/2019
author: LuisBosquez
ms.author: lbosq
ms.openlocfilehash: 0924476a81027e2979616036cd828593e320a3fe
ms.sourcegitcommit: 668b3480cb637c53534642adcee95d687578769a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78898175"
---
# <a name="use-mongodb-compass-to-connect-to-azure-cosmos-dbs-api-for-mongodb"></a>Use o MongoDB Compass para conectar-se à API do Azure Cosmos DB para MongoDB 

Este tutorial demonstra como usar o [MongoDB Compass](https://www.mongodb.com/products/compass) ao armazenar o Cosmos DB. Usaremos a API do Azure Cosmos DB para o MongoDB para este passo a passo. Para aqueles não familiarizados, o Compass é uma interface gráfica de usuário para MongoDB. É comumente usado para visualizar dados, executar consultas ad-hoc e gerenciar dados. 

O Azure Cosmos DB é um serviço de banco de dados multimodelo distribuído globalmente da Microsoft. É possível criar e consultar rapidamente bancos de dados de documentos, de chave/valor e de grafo, que se beneficiem das funcionalidades de escala horizontal e distribuição global no núcleo do Cosmos DB.


## <a name="pre-requisites"></a>Pré-requisitos 
Para se conectar à sua conta do Cosmos DB usando o Robo 3T, você precisa:

* Baixar e instalar [Compass](https://www.mongodb.com/download-center/compass?jmp=hero)
* Obtenha informações da [cadeia de conexão](connect-mongodb-account.md) do Cosmos DB

## <a name="connect-to-cosmos-dbs-api-for-mongodb"></a>Conectar-se à API do Azure Cosmos DB para MongoDB 
Para conectar sua conta do Cosmos DB ao Compass, você pode seguir as etapas:

1. Recupere as informações de conexão da sua conta do Cosmos configurada com a API do Azure Cosmos DB para MongoDB usando as instruções que estão [aqui](connect-mongodb-account.md).

    ![Captura de tela da folha de cadeia de conexão](./media/mongodb-compass/mongodb-compass-connection.png)

2. Clique no botão que diz **Copiar para a Área de Transferência** ao lado de sua **Cadeia de conexão primária/secundária** no Cosmos DB. Clicar nesse botão copiará toda a cadeia de conexão para a área de transferência. 

    ![Captura de tela do botão Copiar para Área de Transferência](./media/mongodb-compass/mongodb-connection-copy.png)

3. Abra o Compass na sua área de trabalho/computador e clique em **Conectar** e em **Conectar a...** . 

4. O Compass irá detectar automaticamente uma cadeia de conexão na área de transferência, e irá pedir para perguntar se você deseja usar isso para se conectar. Clique em **Sim** conforme mostrado na captura de tela abaixo.

    ![Captura de tela do prompt do Compass para conectar](./media/mongodb-compass/mongodb-compass-detect.png)

5. Ao clicar em **Sim** na etapa anterior, os detalhes da cadeia de conexão serão preenchidos automaticamente. Remova o valor preenchido automaticamente a **nome do conjunto de réplica** campo para garantir que é deixado em branco. 

    ![Captura de tela do prompt do Compass para conectar](./media/mongodb-compass/mongodb-compass-replica.png)

6. Na parte inferior da página, clique em **Conectar**. Sua conta e bancos de dados do Cosmos DB agora devem estar visíveis no MongoDB Compass.

## <a name="next-steps"></a>Próximas etapas

- Saiba como [usar o Studio 3T](mongodb-mongochef.md) com a API do Azure Cosmos DB para MongoDB.
- Explore [exemplos](mongodb-samples.md) do MongoDB com a API do Azure Cosmos DB para MongoDB.