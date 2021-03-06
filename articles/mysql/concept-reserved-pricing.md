---
title: Pagar antecipadamente por computação com capacidade reservada-banco de dados do Azure para MySQL
description: Pagar antecipadamente pelos recursos de computação do banco de dados do Azure para MySQL com capacidade reservada
author: kummanish
ms.author: manishku
ms.service: mysql
ms.topic: conceptual
ms.date: 12/02/2019
ms.openlocfilehash: 44bdd9a58bfe2f1a8d3a0102aa6652bb340ac719
ms.sourcegitcommit: 6bb98654e97d213c549b23ebb161bda4468a1997
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74773824"
---
# <a name="prepay-for-azure-database-for-mysql-compute-resources-with-reserved-capacity"></a>Pagar antecipadamente pelos recursos de computação do banco de dados do Azure para MySQL com capacidade reservada

O banco de dados do Azure para MySQL agora ajuda você a economizar dinheiro prestando por recursos de computação em comparação com os preços pagos conforme o uso. Com a capacidade reservada do banco de dados do Azure para MySQL, você faz um compromisso antecipado no servidor MySQL por um período de um ano para obter um desconto significativo nos custos de computação. Para comprar a capacidade reservada do banco de dados do Azure para MySQL, você precisa especificar a região do Azure, o tipo de implantação, o nível de desempenho e o termo. </br>

Você não precisa atribuir a reserva a servidores específicos do banco de dados do Azure para MySQL. Um banco de dados do Azure já em execução para MySQL ou aqueles que foram implantados recentemente obterá automaticamente o benefício do preço reservado. Ao comprar uma reserva, você está pagando pelos custos de computação por um período de um ano. Assim que você comprar uma reserva, os encargos de computação do banco de dados do Azure para MySQL que correspondam aos atributos de reserva não serão mais cobrados com as tarifas pagas pelo uso. Uma reserva não abrange os encargos de software, rede ou armazenamento associados ao servidor de banco de dados MySQL. No final do prazo de reserva, o benefício de cobrança expira e o banco de dados do Azure para MySQL são cobrados pelo preço pago conforme o uso. As reservas não são renovadas automaticamente. Para obter informações sobre preços, consulte a [oferta de capacidade reservada do banco de dados do Azure para MySQL](https://azure.microsoft.com/pricing/details/mysql/). </br>

Você pode comprar a capacidade reservada do banco de dados do Azure para MySQL no [portal do Azure](https://portal.azure.com/). Para comprar a capacidade reservada:

* Você deve estar na função de proprietário de pelo menos uma assinatura corporativa ou individual com tarifas pagas conforme o uso.
* Para as assinaturas Enterprise, a opção **Adicionar Instâncias Reservadas** deve estar habilitada no [Portal EA](https://ea.azure.com/). Ou, se essa configuração estiver desabilitada, você deve ser um administrador de EA na assinatura.
* Para o programa CSP (provedor de soluções na nuvem), somente os agentes de administração ou os agentes de vendas podem comprar a capacidade reservada do banco de dados do Azure para MySQL. </br>

Para saber detalhes sobre como clientes empresariais e clientes do método de pagamento conforme o uso são cobrados para compras de reserva, confira [Entenda o uso de reserva do Azure para seu registro Enterprise](https://docs.microsoft.com/azure/billing/billing-understand-reserved-instance-usage-ea) e [Entenda o uso de reserva do Azure para sua assinatura paga conforme o uso](https://docs.microsoft.com/azure/billing/billing-understand-reserved-instance-usage).


## <a name="determine-the-right-database-size-before-purchase"></a>Determinar o tamanho correto do banco de dados antes da compra

O tamanho da reserva deve ser baseado na quantidade total de computação usada pelo servidor existente ou em breve para ser implantado em uma região específica e usando o mesmo nível de desempenho e geração de hardware.</br>

Por exemplo, suponhamos que você esteja executando uma finalidade geral, um banco de dados MySQL de Gen5 – 32 vCore e duas Gen5 de memória otimizada para 16. Além disso, digamos que você planeja implantar no próximo mês uma finalidade geral adicional, Gen5 – servidor de banco de dados vCore de 32 e um servidor de banco de dados com otimização de memória, Gen5 – 16 vCore. Vamos supor que você saiba que precisará desses recursos por pelo menos 1 ano. Nesse caso, você deve comprar um vCores de 64 (2x32), reserva de 1 ano para o banco de dados único de uso geral-Gen5 e um 48 (2x16 + 16) reserva de 1 ano para a memória de banco de dados individual otimizada-Gen5


## <a name="buy-azure-database-for-mysql-reserved-capacity"></a>Comprar a capacidade reservada do banco de dados do Azure para MySQL

1. Entre no [portal do Azure](https://portal.azure.com/).
2. Selecione **Todos os serviços** > **Reservas**.
3. Selecione **Adicionar** e, em seguida, no painel reservas de compra, selecione **banco de dados do Azure para MySQL** para comprar uma nova reserva para seus bancos de dados MySQL.
4. Preencha os campos obrigatórios. Bancos de dados novos ou existentes que correspondem aos atributos que você selecionar qualificar para obter o desconto de capacidade reservada. O número real de seu banco de dados do Azure para servidores MySQL que obtém o desconto depende do escopo e da quantidade selecionada.


![Visão geral de preços reservados](media/concepts-reserved-pricing/mysql-reserved-price.png)


A tabela a seguir descreve os campos obrigatórios.

| Campo | Descrição |
| :------------ | :------- |
| Subscription   | A assinatura usada para pagar o banco de dados do Azure para reserva de capacidade reservada do MySQL. O método de pagamento na assinatura é cobrado pelos custos antecipados do banco de dados do Azure para reserva de capacidade reservada do MySQL. O tipo de assinatura deve ser um Enterprise Agreement (números de oferta: MS-AZR-0017P ou MS-AZR-0148P) ou um contrato individual com preço pago conforme o uso (números de oferta: MS-AZR-0003P ou MS-AZR-0023P). Para uma assinatura de empresa, os encargos são deduzidos do saldo do compromisso monetário do registro ou cobrados como média. Para uma assinatura individual com o preço pago conforme o uso, os encargos são cobrados no cartão de crédito ou no método de pagamento de fatura na assinatura.
| Escopo | O escopo da reserva vCore pode cobrir uma assinatura ou várias assinaturas (escopo compartilhado). Se você selecionar: </br></br> **Compartilhado**, o desconto de reserva vCore é aplicado ao banco de dados do Azure para servidores MySQL em execução em qualquer assinatura em seu contexto de cobrança. Para clientes empresariais, o escopo compartilhado é o registro e inclui todas as assinaturas no registro. Para clientes de Pagamento Conforme o Uso, o escopo compartilhado consiste em todas as assinaturas de Pagamento Conforme o Uso criadas pelo administrador da conta.</br></br> **Assinatura única**, o desconto de reserva vCore é aplicado ao banco de dados do Azure para servidores MySQL nesta assinatura. </br></br> **Um grupo de recursos único**, o desconto de reserva é aplicado ao banco de dados do Azure para servidores MySQL na assinatura selecionada e ao grupo de recursos selecionado dentro dessa assinatura.
| Região | A região do Azure que é coberta pelo banco de dados do Azure para MySQL reserva de capacidade reservada.
| Tipo de implantação | O tipo de recurso do banco de dados do Azure para MySQL do qual você deseja comprar a reserva.
| Nível de desempenho | A camada de serviço do banco de dados do Azure para servidores MySQL.
| Prazo | Um ano
| Quantidade | A quantidade de recursos de computação que está sendo adquirida no banco de dados do Azure para MySQL reserva de capacidade reservada. A quantidade é um número de vCores na região do Azure e no nível de desempenho selecionados que estão sendo reservados e receberão o desconto de cobrança. Por exemplo, se você estiver executando ou planejando executar um banco de dados do Azure para servidores MySQL com a capacidade de computação total de Gen5 16 vCores na região leste dos EUA, você deverá especificar a quantidade como 16 para maximizar o benefício para todos os servidores.

## <a name="cancel-exchange-or-refund-reservations"></a>Cancelar, trocar ou reembolsar reservas

É possível cancelar, trocar ou reembolsar reservas com determinadas limitações. Para saber mais, confira [Trocas e reembolsos via autoatendimento para Reservas do Azure](https://docs.microsoft.com/azure/billing/billing-azure-reservations-self-service-exchange-and-refund).

## <a name="vcore-size-flexibility"></a>Flexibilidade de tamanho do vCore

A flexibilidade de tamanho do vCore ajuda você a aumentar ou diminuir dentro de uma região e nível de desempenho sem perder o benefício de capacidade reservada. 

## <a name="need-help--contact-us"></a>Precisa de ajuda? Contate-nos

Se você tiver dúvidas ou precisar de ajuda, [crie uma solicitação de suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## <a name="next-steps"></a>Próximos passos

O desconto de reserva vCore é aplicado automaticamente ao número de servidores do banco de dados do Azure para MySQL que correspondem ao banco de dados do Azure para o escopo de reserva de capacidade reservada do MySQL e atributos. Você pode atualizar o escopo do banco de dados do Azure para MySQL reserva de capacidade reservada por meio de portal do Azure, PowerShell, CLI ou por meio da API. </br></br>
Para saber como gerenciar a capacidade reservada do banco de dados do Azure para MySQL, veja gerenciar a capacidade reservada do banco de dados do Azure para MySQL.

Para saber mais sobre as reservas do Azure, consulte os seguintes artigos:

* [O que são as reservas do Azure](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations)?
* [Gerenciar Reservas do Azure](https://docs.microsoft.com/azure/billing/billing-manage-reserved-vm-instance)
* [Compreender o desconto de Reservas do Azure](https://docs.microsoft.com/azure/billing/billing-understand-reservation-charges)
* [Entender o uso de reserva para a sua assinatura paga conforme o uso](https://docs.microsoft.com/azure/billing/billing-understand-reservation-charges-mysql)
* [Entender o uso de reserva para seu registro de empresa](https://docs.microsoft.com/azure/billing/billing-understand-reserved-instance-usage-ea)
* [Reservas do Azure no programa de CSP (Provedor de Soluções na Nuvem) do Partner Center.](https://docs.microsoft.com/partner-center/azure-reservations)

