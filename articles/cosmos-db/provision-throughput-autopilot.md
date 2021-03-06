---
title: Crie contêineres e bancos de dados do Azure Cosmos no modo de piloto automático.
description: Saiba mais sobre os benefícios, casos de uso e como provisionar bancos de dados e contêineres do Azure Cosmos no modo de piloto automático.
author: kirillg
ms.author: kirillg
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 11/04/2019
ms.openlocfilehash: 89af30788fe5129cddc6a3607b8c722549b610d1
ms.sourcegitcommit: 7b25c9981b52c385af77feb022825c1be6ff55bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79246650"
---
# <a name="create-azure-cosmos-containers-and-databases-in-autopilot-mode-preview"></a>Criar contêineres e bancos de dados do Azure Cosmos no modo de piloto automático (versão prévia)

O Azure Cosmos DB permite provisionar a taxa de transferência em seus contêineres no modo manual ou piloto automático. Este artigo descreve os benefícios e casos de uso do modo de piloto automático.

> [!NOTE]
> O modo AutoPilot está disponível atualmente na visualização pública. Você pode [habilitar o AutoPilot somente para novos bancos de dados e contêineres](#create-a-database-or-a-container-with-autopilot-mode) . Ele não está disponível para contêineres e bancos de dados existentes.

Além do provisionamento manual da taxa de transferência, agora você pode configurar contêineres do cosmos do Azure no modo AutoPilot. Os contêineres e os bancos de dados configurados no modo de piloto automático irão **dimensionar automaticamente e de forma instantânea a taxa de transferência provisionada com base nas necessidades do aplicativo sem afetar a disponibilidade, a latência, a taxa de transferência ou o desempenho da carga de trabalho globalmente.**

Ao configurar contêineres e bancos de dados no modo de piloto automático, você precisa especificar que a taxa de transferência máxima não `Tmax` ser excedida. Os contêineres podem dimensionar sua taxa de transferência para que `0.1*Tmax < T < Tmax`. Em outras palavras, os contêineres e os bancos de dados são dimensionados instantaneamente com base nas necessidades de carga de trabalho, de até 10% do valor máximo de taxa de transferência que você configurou até o valor máximo de taxa de transferência configurado. Você pode alterar a configuração de taxa de transferência máxima (`Tmax`) em um banco de dados ou contêiner do AutoPilot em qualquer momento. Com a opção AutoPilot, a taxa de transferência mínima de 400 RU/s por contêiner ou banco de dados não é mais aplicável.

Durante a versão prévia do piloto automático, para a taxa de transferência máxima especificada no contêiner ou no banco de dados, o sistema permite operar dentro do limite de armazenamento calculado. Se o limite de armazenamento for excedido, a taxa de transferência máxima será ajustada automaticamente para um valor mais alto. Ao usar a taxa de transferência no nível do banco de dados com o modo AutoPilot, o número de contêineres permitidos em um banco de dados é calculado como: `0.001*TMax`. Por exemplo, se você provisionar 20.000 AutoPilot RU/s, o banco de dados poderá ter 20 contêineres.

## <a name="benefits-of-autopilot-mode"></a>Benefícios do modo AutoPilot

Os contêineres do cosmos do Azure que são configurados no modo AutoPilot têm os seguintes benefícios:

* **Simples:** Os contêineres no modo AutoPilot removem a complexidade para gerenciar a taxa de transferência provisionada (RUs) e a capacidade manualmente para vários contêineres.

* **Escalonável:** Os contêineres no modo AutoPilot dimensionam diretamente a capacidade de taxa de transferência provisionada conforme necessário. Não há interrupção nas conexões de cliente, aplicativos e elas não afetam nenhum SLA existente.

* Econômico **:** Quando você usa contêineres configurados no modo de piloto automático, você paga apenas pelos recursos de que suas cargas de trabalho precisam por hora.

* **Altamente disponível:** Os contêineres no modo de AutoPilot usam o mesmo back-end de alta disponibilidade, tolerante a falhas e distribuída globalmente para garantir a durabilidade dos dados e a alta disponibilidade.

## <a name="use-cases-of-autopilot-mode"></a>Casos de uso do modo AutoPilot

Os casos de uso dos contêineres Cosmos do Azure configurados no modo AutoPilot incluem:

* **Cargas de trabalho variáveis:** Quando você estiver executando um aplicativo levemente usado com pico de uso de 1 hora a várias horas algumas vezes por dia ou várias vezes por ano. Os exemplos incluem aplicativos para recursos humanos, orçamento e relatórios operacionais. Para esses cenários, os contêineres configurados no modo de piloto automático podem ser usados e você não precisa mais provisionar manualmente para a capacidade de pico ou média.

* **Cargas de trabalho imprevisíveis:** Quando você estiver executando cargas de trabalho em que há uso de banco de dados ao longo do dia, mas também aos picos de atividade que são difíceis de prever. Um exemplo inclui um site de tráfego que vê um surto de atividade quando a previsão do tempo muda. Os contêineres configurados no modo de piloto automático ajustam a capacidade para atender às necessidades da carga de pico do aplicativo e de reduzir verticalmente quando o surto da atividade terminar.

* **Novos aplicativos:** Se você estiver implantando um novo aplicativo e não tiver certeza quanto à quantidade de produtividade provisionada (ou seja, quantos RUs) você precisa. Com os contêineres configurados no modo AutoPilot, você pode dimensionar automaticamente para as necessidades de capacidade e os requisitos de seu aplicativo.

* **Aplicativos usados com pouca frequência:** Se você tiver um aplicativo que só é usado por algumas horas várias vezes por dia ou semana ou mês, como um aplicativo de baixo volume/Web/site de blog.

* **Bancos de dados de desenvolvimento e teste:** Se você tiver desenvolvedores que usam contêineres durante horas de trabalho, mas não precisarem deles em noites ou fins de semana. Com contêineres configurados no modo AutoPilot, eles são reduzidos verticalmente para um mínimo quando não estão em uso.

* **Cargas de trabalho/consultas de produção agendadas:** Quando você tem uma série de solicitações/operações/consultas agendadas em um único contêiner e, se houver períodos ociosos em que você deseja executar com uma taxa de transferência baixa absoluta, agora você pode fazer isso facilmente. Quando uma consulta/solicitação agendada for enviada para um contêiner configurado no modo de piloto automático, ela aumentará automaticamente o máximo possível e executará a operação.

As soluções para os problemas anteriores não só exigem uma enorme quantidade de tempo na implementação, mas também introduzem complexidade na configuração ou no código, e muitas vezes exigem intervenção manual para solucioná-los. O modo AutoPilot habilita os cenários acima prontos para uso, para que você não precise mais se preocupar com esses problemas.

## <a name="comparison--containers-configured-in-manual-mode-vs-autopilot-mode"></a>Comparação – contêineres configurados no modo manual vs. modo AutoPilot

|  | Contêineres configurados no modo manual  | Contêineres configurados no modo AutoPilot |
|---------|---------|---------|
| **Taxa de transferência provisionada** | Provisionado manualmente. | Escalado de imediato e instantâneo com base nos padrões de uso da carga de trabalho. |
| **Taxa-limitação de solicitações/operações (429)**  | Pode acontecer se o consumo exceder a capacidade provisionada. | Não ocorrerá se a taxa de transferência consumida estiver dentro da taxa de transferência máxima escolhida com o modo AutoPilot.   |
| **Planejamento da capacidade** |  Você precisa fazer um planejamento de capacidade inicial e provisionar a taxa de transferência de que precisa. |    Você não precisa se preocupar com o planejamento de capacidade. O sistema cuida automaticamente do planejamento de capacidade e do gerenciamento de capacidade. |
| **Preços** | O provisionamento manual de RU/s por hora. | Para contas de região de gravação única, você paga pela taxa de transferência usada por hora, usando o AutoPilot RU/s por hora. <br/><br/>Para contas com várias regiões de gravação, não há nenhum custo adicional para o piloto automático. Você paga pela taxa de transferência usada por hora usando a mesma tarifa de RU/s de vários mestres por hora. |
| **Mais adequado para tipos de carga de trabalho** |  Cargas de trabalho previsíveis e estáveis|   Cargas de trabalho imprevisíveis e variáveis  |

## <a name="create-a-database-or-a-container-with-autopilot-mode"></a>Criar um banco de dados ou um contêiner com o modo de piloto automático

Você pode configurar o AutoPilot para novos bancos de dados ou contêineres ao criá-los por meio do portal do Azure. Use as etapas a seguir para criar um novo banco de dados ou contêiner, habilitar o AutoPilot e especificar a taxa de transferência máxima (RU/s).

1. Entre no [portal do Azure](https://portal.azure.com) ou no [Azure Cosmos DB Explorer.](https://cosmos.azure.com/)

1. Navegue até sua conta do Azure Cosmos DB e abra a guia **Data Explorer** .

1. Selecione **novo contêiner.** Insira um nome para seu banco de dados, contêiner e uma chave de partição. Em **taxa de transferência**, selecione a opção **AutoPilot** e escolha a taxa de transferência máxima (ru/s) que o banco de dados ou o contêiner não pode exceder ao usar a opção AutoPilot.

   ![Criando um contêiner e configurando a taxa de transferência do AutoPilot](./media/provision-throughput-autopilot/create-container-autopilot-mode.png)

1. Selecione **OK**.

Você pode criar um banco de dados de produtividade compartilhado com o modo AutoPilot selecionando a opção **provisionar taxa de transferência de banco de dados** .

## <a id="autopilot-limits"></a>Taxa de transferência e limites de armazenamento para o piloto automático

A tabela a seguir mostra o máximo em todo e os limites de armazenamento para diferentes opções no modo de piloto automático:

|Limite máximo de taxa de transferência  |Limite máximo de armazenamento  |
|---------|---------|
|4000 RU/s  |   50 GB    |
|20.000 RU/s  |  200 GB  |
|100.000 RU/s    |  1 TB   |
|500.000 RU/s    |  5 TB  |

## <a name="next-steps"></a>Próximas etapas

* Examine as [perguntas frequentes do AutoPilot](autopilot-faq.md).
* Saiba mais sobre [partições lógicas](partition-data.md).
* Saiba como [provisionar taxa de transferência em um contêiner do Azure Cosmos DB](how-to-provision-container-throughput.md).
* Saiba como [provisionar taxa de transferência em um banco de dados do Azure Cosmos DB](how-to-provision-database-throughput.md).
