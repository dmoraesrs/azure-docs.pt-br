---
title: Transformar dados com o Python do databricks
description: Saiba como processar ou transformar dados executando um Python do Databricks.
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 03/15/2018
author: djpmsft
ms.author: daperlov
ms.reviewer: maghan
manager: anandsub
ms.openlocfilehash: be2e389a0f103983a566a3f74d201e5589d84586
ms.sourcegitcommit: a5ebf5026d9967c4c4f92432698cb1f8651c03bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74926732"
---
# <a name="transform-data-by-running-a-python-activity-in-azure-databricks"></a>Transformar dados executando uma atividade de Python no Azure Databricks

A atividade de Python do Azure Databricks em um [pipeline do Data Factory](concepts-pipelines-activities.md) executa um arquivo de Python em seu cluster do Azure Databricks. Este documento baseia-se no artigo sobre  [atividades de transformação de dados](transform-data.md) , que apresenta uma visão geral da transformação de dados e das atividades de transformação permitidas. Azure Databricks é uma plataforma gerenciada para executar o Apache Spark.

Para ver uma introdução de 11 minutos e uma demonstração desse recurso, assista ao seguinte vídeo:

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Execute-Jars-and-Python-scripts-on-Azure-Databricks-using-Data-Factory/player]

## <a name="databricks-python-activity-definition"></a>Definição de atividade do Databricks Python

A seguir está a definição JSON de exemplo de uma Atividade de Python do Databricks:

```json
{
    "activity": {
        "name": "MyActivity",
        "description": "MyActivity description",
        "type": "DatabricksSparkPython",
        "linkedServiceName": {
            "referenceName": "MyDatabricksLinkedservice",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "pythonFile": "dbfs:/docs/pi.py",
            "parameters": [
                "10"
            ],
            "libraries": [
                {
                    "pypi": {
                        "package": "tensorflow"
                    }
                }
            ]
        }
    }
}
```

## <a name="databricks-python-activity-properties"></a>Propriedades de atividade do Databricks Python

A tabela a seguir descreve as propriedades JSON usadas na definição de JSON:

|Propriedade|Descrição|obrigatórios|
|---|---|---|
|Nome|Nome da atividade no pipeline.|SIM|
|Descrição|Texto que descreve o que a atividade faz.|Não|
|type|Para a Atividade do Databricks Python, o tipo de atividade é DatabricksSparkPython.|SIM|
|linkedServiceName|Nome do serviço vinculado ao Databricks no qual a atividade de Python é executado. Para saber mais sobre esse serviço vinculado, consulte o artigo  [Serviços de computação vinculados](compute-linked-services.md) .|SIM|
|pythonFile|O URI do arquivo Python a ser executado. Há suporte para apenas os caminhos DBFS.|SIM|
|parâmetros|Parâmetros de linha de comando que serão passados para o arquivo Python. Isto é uma matriz de cadeias de caracteres.|Não|
|bibliotecas|Uma lista de bibliotecas a serem instaladas no cluster, que executará o trabalho. Ele pode ser uma matriz de <string, object>|Não|

## <a name="supported-libraries-for-databricks-activities"></a>Bibliotecas com suporte para atividades do databricks

Na definição da atividade acima do Databricks você especifica esses tipos de biblioteca: *jar*, *egg*, *maven*, *pypi*,  *cran*.

```json
{
    "libraries": [
        {
            "jar": "dbfs:/mnt/libraries/library.jar"
        },
        {
            "egg": "dbfs:/mnt/libraries/library.egg"
        },
        {
            "maven": {
                "coordinates": "org.jsoup:jsoup:1.7.2",
                "exclusions": [ "slf4j:slf4j" ]
            }
        },
        {
            "pypi": {
                "package": "simplejson",
                "repo": "http://my-pypi-mirror.com"
            }
        },
        {
            "cran": {
                "package": "ada",
                "repo": "https://cran.us.r-project.org"
            }
        }
    ]
}

```

Para obter mais detalhes, consulte [documentação do Databricks](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) para tipos de biblioteca.

## <a name="how-to-upload-a-library-in-databricks"></a>Como carregar uma biblioteca no Databricks

#### <a name="using-databricks-workspace-uihttpsdocsazuredatabricksnetuser-guidelibrarieshtmlcreate-a-library"></a>[Usando o workspace do Databricks da interface do usuário](https://docs.azuredatabricks.net/user-guide/libraries.html#create-a-library)

Para obter o caminho dbfs da biblioteca adicionada usando a interface do usuário, você pode usar [CLI do Databricks (instalação)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli). 

Normalmente, as bibliotecas Jar são armazenadas em dbfs:/FileStore/jars ao usar a interface do usuário. Você pode listar todos os por meio da CLI: *databricks fs ls dbfs:/FileStore/jars* 



#### <a name="copy-library-using-databricks-clihttpsdocsazuredatabricksnetuser-guidedev-toolsdatabricks-clihtmlcopy-a-file-to-dbfs"></a>[Copie a biblioteca usando a CLI do Databricks](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#copy-a-file-to-dbfs)

Exemplo: *databricks fs cp SparkPi-assembly-0.1.jar dbfs:/FileStore/jars*