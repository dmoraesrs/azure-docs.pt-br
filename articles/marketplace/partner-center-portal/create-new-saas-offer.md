---
title: Criar uma nova oferta de SaaS no Marketplace comercial
description: Como criar uma nova oferta de SaaS (software como serviço) para listagem ou venda no Azure Marketplace, AppSource ou por meio do programa CSP (provedor de soluções na nuvem) usando o portal do Marketplace comercial no Microsoft Partner Center.
author: ChJenk
manager: evansma
ms.author: v-chjen
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 02/28/2020
ms.openlocfilehash: 9d06b34b459bf1d48aa293a889af57fb6192015d
ms.sourcegitcommit: 5192c04feaa3d1bd564efe957f200b7b1a93a381
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78208858"
---
# <a name="create-a-new-saas-offer"></a>Criar uma nova oferta de SaaS

Para começar a criar ofertas de SaaS (software como serviço), certifique-se de primeiro [criar uma conta do Partner Center](./create-account.md) e abra o [painel do Marketplace comercial](https://partner.microsoft.com/dashboard/commercial-marketplace/offers), com a guia **visão geral** selecionada.

![Painel do Marketplace comercial no Partner Center](./media/new-offer-overview.png)

>[!Note]
> Depois que uma oferta tiver sido publicada, edições para a oferta feita no Partner Center serão atualizadas somente no sistema e armazenará os frontais após a republicação. Certifique-se de enviar a oferta para publicação depois de fazer alterações.

Selecione a **nova oferta + novo...** , selecione o item de menu **software como um serviço** .

Se você selecionar outro tipo de oferta, poderá ser redirecionado para o [portal do Cloud Partner](https://cloudpartner.azure.com/)mais antigo. Somente as ofertas de SaaS e Dynamics 365 estão disponíveis no portal do Marketplace comercial no Partner Center no momento.

![Criar janela de oferta no Partner Center](./media/new-offer-click.png)

A caixa de diálogo **nova oferta** é exibida.

![Caixa de diálogo nova oferta](./media/new-offer-popup.png)

## <a name="offer-id-and-alias"></a>ID da oferta e alias

- **ID da oferta**: identificador exclusivo para cada oferta em sua conta. Essa ID será visível para os clientes no endereço URL para a oferta do Marketplace e os modelos de Azure Resource Manager (se aplicável). A ID da oferta deve estar em letras minúsculas, alfanuméricas (incluindo hifens e sublinhados, mas sem espaço em branco). A **ID da oferta** é limitada a 50 caracteres e não pode ser alterada depois que você seleciona *criar*.  
Exemplo: Test-offer-1
<br>Resultando na URL: `https://azuremarketplace.microsoft.com/marketplace/../test-offer-1`

- **Alias da oferta**: o nome usado para fazer referência à oferta no portal do Partner Center. Esse nome não será usado no Marketplace e será diferente do nome da *oferta* e outros valores que serão mostrados aos clientes. Esse valor não pode ser alterado depois que você seleciona *criar*.

<br>Exemplo: oferta de teste 1&#8482;

Selecione **Criar**.  Uma página de **visão geral da oferta** é criada para esta oferta.  

<!---
![Offer overview on Partner Center](./media/commercial-marketplace-offer-overview.png)
-->

## <a name="offer-overview"></a>Visão geral da oferta

A página **visão geral da oferta** inclui:

- O **status de publicação** exibe uma representação visual das etapas necessárias para publicar essa oferta e quanto tempo cada etapa levará para ser concluída. Os ícones de etapa de publicação incompletos ficarão esmaecidos.

- O menu **visão geral da oferta** contém uma lista de links para executar operações nessa oferta. Essa lista de operações será alterada com base na seleção feita para sua oferta.  
    - Se a oferta for um rascunho de exclusão de rascunho
    - Se a oferta for Live-Stop Reseller offer
    - Se a oferta estiver em visualização-Go-Live
    - Se você ainda não concluiu a saída do Publicador, cancelar publicação

## <a name="offer-setup"></a>Instalação da oferta

A guia **instalação da oferta** solicita as seguintes informações. Selecione **salvar** depois de concluir esses campos.

- **Você gostaria de vender pela Microsoft?** (Sim/Não)
    - **Sim**, você gostaria de vender sua oferta pela Microsoft, com as transações do Marketplace de hospedagem da Microsoft em seu nome; or 
    - **Não**, você prefere apenas listar sua oferta por meio dos Marketplaces, processando quaisquer transações monetárias independentemente da Microsoft.

### <a name="sell-through-microsoft"></a>Vender por meio da Microsoft

A venda pela Microsoft fornece melhor descoberta de clientes e aquisição, permite que a Microsoft hospede transações de Marketplace em seu nome e aproveita os recursos de comércio disponíveis globalmente da Microsoft.

#### <a name="saas-offer-requirements"></a>Requisitos da oferta de SaaS

Para listar ofertas de SaaS (software como serviço) com o Marketplace comercial no Partner Center, os critérios a seguir devem ser atendidos:

- Sua oferta deve usar [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) para gerenciamento de identidade e autenticação.
- Sua oferta deve usar [APIs de preenchimento de SaaS](https://docs.microsoft.com/azure/marketplace/partner-center-portal/pc-saas-fulfillment-api-v2) para integrar com o Azure Marketplace.
- Para obter requisitos mais amplos, consulte o [Guia de publicação da oferta de SaaS](https://docs.microsoft.com/azure/marketplace/marketplace-saas-applications-technical-publishing-guide).

#### <a name="saas-pricing-and-billing-options"></a>Opções de preços e cobrança de SaaS
Com as soluções de SaaS em execução na assinatura do Azure do Publicador, as taxas de licença pagas pelos clientes incluem o custo da infraestrutura na qual o software é implantado. O uso de infraestrutura do Azure é gerenciado e cobrado para você, o parceiro, diretamente. Os valores reais de uso da infraestrutura não são vistos pelo cliente. Os editores devem agrupar as taxas de uso de infraestrutura do Azure em seus preços de licença de software. 

O SaaS oferece suporte à cobrança mensal ou anual com base em taxas fixas, por usuário ou cobranças de consumo usando o serviço de cobrança limitado. O Marketplace comercial da Microsoft opera em um modelo de agência, no qual os editores definem preços, a Microsoft Bills Customers e a Microsoft paga receita para o Publicador durante a retenção de uma tarifa de agência.

A tabela a seguir mostra um exemplo de divisão de custos e pagamentos para demonstrar o modelo de agência.

|**Seu custo de licença**|**$100 por mês**|
|:---|:---|
|Custo de uso do Azure (D1/1-Núcleo)|Cobrados diretamente para o publicador, não o cliente|
|O cliente é cobrado pela Microsoft|$100 por mês (o Publicador deve considerar os custos incorridos ou da infraestrutura de passagem na taxa de licença)|

|**Faturas da Microsoft**|**$100 por mês**|
|:---|:---|
|A Microsoft paga para você 80% do seu custo de licença <br>**para aplicativos SaaS qualificados, a Microsoft paga 90% do seu custo de licença*|US $80,00 por mês <br>*$* 90, 0 por mês *|

- Neste exemplo, a Microsoft fatura $100 para o cliente para sua licença de software e paga $80 para o Publicador.
- Os parceiros qualificados para a **taxa reduzida de serviço do Marketplace** verão uma taxa de transação reduzida nas ofertas de SaaS de maio de 2019 até junho de 2020. Nesse cenário, a Microsoft cobra $100 pela sua licença de software e paga $90 para o Publicador.

> [!NOTE]
> **Redução da taxa de serviço do Marketplace**: para determinadas ofertas de SaaS que você publicou em nosso mercado comercial, a Microsoft reduzirá sua taxa de serviço do Marketplace de 20% (conforme descrito no contrato do Microsoft Publisher) para 10%. Para que sua oferta seja qualificada, pelo menos uma de suas ofertas deve ter sido designada pela Microsoft como sendo de revenda de IP coexistente ou em uma venda de IP.  A qualificação deve ser atendida pelo menos cinco (5) dias úteis antes do final de cada mês do calendário para receber essa taxa de serviço do Marketplace reduzida para o mês.  A taxa reduzida de serviço do Marketplace não se aplica a VMs, aplicativos gerenciados ou quaisquer outros produtos disponibilizados por meio de nosso mercado comercial.  A taxa reduzida de serviço do Marketplace só estará disponível para ofertas qualificadas para encargos de licença coletados pela Microsoft entre 1º de maio de 2019 e 30 de junho de 2020.  Após esse período, a taxa de serviço do Marketplace voltará ao seu valor normal.

### <a name="list-through-microsoft"></a>Listar pela Microsoft

Promova seus negócios com a Microsoft criando uma listagem do Marketplace. Selecionar para listar sua oferta somente e não realizar transações por meio da Microsoft significa que a Microsoft não participará diretamente da transação de licença de software. Não há nenhuma taxa de transação associada e o Publicador mantém 100% de quaisquer taxas de licenciamento de software coletadas do cliente. No entanto, o Publicador é responsável por dar suporte a todos os aspectos da transação de licença de software, incluindo, mas não se limitando a: preenchimento de pedido, medição, cobrança, faturamento, pagamento e coleção.

- **Como você deseja que clientes potenciais interajam com esta oferta de listagem?**

##### <a name="get-it-now-free"></a>Obtenha agora (gratuito)
Liste sua oferta aos clientes gratuitamente fornecendo uma URL válida (começando com *http* ou *https*), na qual eles podem obter uma avaliação por meio da [autenticação com um clique usando Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/marketplace/marketplace-saas-applications-technical-publishing-guide#using-azure-active-directory-to-enable-trials).  Por exemplo: `https://contoso.com/saas-app`

##### <a name="free-trial-listing"></a>Avaliação gratuita (listagem)
Liste sua oferta aos clientes com um link para uma avaliação gratuita fornecendo uma URL válida (começando com *http* ou *https*), em que eles podem obter uma avaliação por meio de [autenticação com um clique usando Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/marketplace/marketplace-saas-applications-technical-publishing-guide#using-azure-active-directory-to-enable-trials).  Por exemplo: `https://contoso.com/trial/saas-app`. As avaliações gratuitas de listagem de ofertas são criadas, gerenciadas e configuradas pelo seu serviço e não têm assinaturas gerenciadas pela Microsoft.

> [!NOTE]
> Os tokens que seu aplicativo receberá por meio do link de avaliação só podem ser usados para obter informações do usuário por meio do Azure AD para automatizar a criação de contas em seu aplicativo. As contas da Microsoft (MSA) não têm suporte para autenticação usando esse token.

##### <a name="contact-me"></a>Entrar em contato comigo
Colete informações de contato do cliente conectando seu sistema de gerenciamento de relacionamento com o cliente (CRM). O cliente será solicitado a fornecer permissão para compartilhar suas informações. Esses detalhes do cliente, juntamente com o nome da oferta, a ID e a origem do Marketplace onde encontraram sua oferta, serão enviados para o sistema CRM que você configurou. Para obter mais informações sobre como configurar seu CRM, consulte [Connect Lead Management](#connect-lead-management).

## <a name="example-marketplace-offer-listing"></a>Exemplo de listagem de oferta do Marketplace

![Exemplo de listagem de oferta do Marketplace com observações](./media/marketplace-offer.svg)

## <a name="enable-a-test-drive"></a>Habilitar um test drive

Uma test drive é uma ótima maneira de demonstrar sua oferta a clientes potenciais, fornecendo a eles a opção "tentar antes de comprar", resultando em uma maior conversão e na geração de clientes potenciais altamente qualificados. [Saiba mais sobre test drives.](https://docs.microsoft.com/azure/marketplace/cloud-partner-portal/test-drive/what-is-test-drive)

- **Habilitar um test drive** (caixa de seleção)

Ao habilitar o test drive, você será solicitado a configurar um ambiente de demonstração para os clientes experimentarem sua oferta por um período de tempo fixo. 

#### <a name="test-drive-resources"></a>Recursos do Test Drive
- [Práticas recomendadas técnicas do Test Drive](https://github.com/Azure/AzureTestDrive/wiki/Test-Drive-Best-Practices)
- [Práticas recomendadas de marketing do Test Drive](https://docs.microsoft.com/azure/marketplace/cloud-partner-portal/test-drive/marketing-and-best-practices)
- [Visão geral do Test Drive One pager](https://assetsprod.microsoft.com/mpn/azure-marketplace-appsource-test-drives.pdf)

## <a name="connect-lead-management"></a>Conectar gerenciamento de leads

[!INCLUDE [Connect lead management](./includes/connect-lead-management-a.md)]

#### <a name="additional-lead-management-resources"></a>Recursos adicionais de gerenciamento de leads
- [Perguntas frequentes sobre gerenciamento de leads](https://docs.microsoft.com/azure/marketplace/lead-management-for-cloud-marketplace#frequently-asked-questions)
- [Erros comuns de configuração de leads](https://docs.microsoft.com/azure/marketplace/lead-management-for-cloud-marketplace#common-lead-configuration-errors-during-publishing-on-cloud-partner-portal)
- [Visão geral do gerenciamento de leads um pager](https://assetsprod.microsoft.com/mpn/cloud-marketplace-lead-management.pdf)

Lembre-se de **salvar** antes de passar para a próxima seção.

## <a name="properties"></a>{1&gt;Propriedades&lt;1}

A guia **Propriedades** solicita que você defina as categorias e os setores usados para agrupar sua oferta nos Marketplaces, os contratos legais que dão suporte à sua oferta e a versão do aplicativo.

Selecione **salvar** depois de concluir esses campos.

### <a name="category"></a>Categoria

Selecione no mínimo um (1) e no máximo três (3) categorias usadas para agrupar sua oferta nas áreas de pesquisa do Marketplace apropriadas. Descubra como sua oferta dá suporte a essas categorias na descrição da oferta.

### <a name="industry"></a>Setor

[!INCLUDE [Industry Taxonomy](./includes/industry-taxonomy.md)]

### <a name="app-version"></a>Versão do aplicativo

Esse campo é opcional e usado no AppSource Marketplace para identificar o número de versão da sua oferta.

### <a name="standard-contract-for-the-microsoft-commercial-marketplace"></a>Contrato padrão para o Marketplace comercial da Microsoft

A Microsoft fornece um modelo de contrato padrão.

- **Usar o contrato padrão para o Marketplace comercial da Microsoft?**

Para simplificar o processo de aquisição para clientes e reduzir a complexidade legal para fornecedores de software, a Microsoft oferece um contrato padrão para o Microsoft Commercial Marketplace para ajudar a facilitar as transações no Marketplace. Em vez de criar termos e condições personalizados, os editores de mercado comercial podem optar por oferecer seu software sob o contrato padrão, que os clientes precisam apenas examinaremos e aceitar uma vez. O contrato padrão pode ser encontrado aqui: https://go.microsoft.com/fwlink/?linkid=2041178.

Você pode optar por usar o contrato padrão em vez de fornecer seus próprios termos e condições personalizados selecionando a caixa de seleção "usar o contrato padrão para o Marketplace comercial".

![Usando a caixa de seleção de contrato padrão](./media/use-standard-contract.png)

> [!NOTE]
> Depois de publicar uma oferta usando o contrato padrão do Microsoft Commercial Marketplace, você não poderá usar seus próprios termos e condições personalizados. É um cenário de "ou". Você pode oferecer sua solução sob o contrato Standard **ou** seus próprios termos e condições. Se você quiser modificar os termos do contrato padrão, poderá fazer isso por meio de emendas de contrato padrão.

#### <a name="standard-contract-amendments"></a>Emendas de contrato padrão

As emendas de contrato padrão permitem que os editores selecionem os termos de contrato padrão para simplificar e personalizar os termos para seus produtos ou negócios. Os clientes precisam apenas examinar as emendas ao contrato, caso já tenham revisado e aceito o contrato padrão da Microsoft.

Há dois tipos de emendas disponíveis para editores de mercado comercial:

- Emendas universais: essas emendas são aplicadas universalmente ao contrato padrão para todos os clientes. As emendas universais são mostradas a todos os clientes da oferta no fluxo de compra. Os clientes devem aceitar os termos do contrato padrão e o aditamento antes de poderem usar sua oferta.
- Emendas personalizadas: essas emendas são emendas especiais ao contrato padrão que são direcionados a clientes específicos somente por meio de IDs de locatário do Azure. Os editores podem escolher o locatário que desejam direcionar. Somente os clientes do locatário serão apresentados com os termos personalizados de emenda no fluxo de compra da oferta.  Os clientes devem aceitar os termos do contrato padrão e as emendas antes de poderem usar sua oferta.

>[!NOTE]
> Esses dois tipos de emendas se empilham um sobre o outro. Os clientes destinados a emendas personalizadas também terão a emenda universal ao contrato padrão durante a compra.

**Termos de emenda universal para o contrato padrão do Marketplace comercial da Microsoft**: Insira os termos de emenda universal nesta caixa. Você pode fornecer uma única emenda universal por oferta. Você pode inserir um número ilimitado de caracteres nesta caixa. Esses termos são exibidos para clientes no AppSource, no Azure Marketplace e/ou portal do Azure durante a descoberta e o fluxo de compra.

**Termos personalizados de emenda para o contrato padrão do Marketplace comercial da Microsoft**: comece selecionando **Adicionar termos de emenda personalizada**. Você pode fornecer até 10 termos personalizados de emenda por oferta.

- **Termos personalizados de emenda**: insira seus termos de emenda personalizada na caixa termos personalizados de emenda. Você pode inserir um número ilimitado de caracteres nesta caixa. Somente os clientes das IDs de locatário que você especificar para esses termos personalizados serão apresentados com os termos personalizados de emenda no fluxo de compra da oferta no portal do Azure.  
- **IDs de locatário** (obrigatório): cada alteração personalizada pode ser direcionada para até 20 IDs de locatário. Se você adicionar uma emenda personalizada, deverá fornecer pelo menos uma ID de locatário. A ID de locatário identifica seu cliente no Azure. Você pode solicitar que o cliente tenha essa ID e pode encontrá-la navegando até portal.azure.com > Azure Active Directory Propriedades de >. O valor da ID de diretório é a ID do locatário (por exemplo, 50c464d3-4930-494c-963c-1e951d15360e). Você também pode pesquisar a ID de locatário da organização de seu cliente usando a URL do nome de domínio em [qual Microsoft Azure é a ID do locatário do Office 365 e do Microsoft?](https://www.whatismytenantid.com).
- **Descrição** (opcional): opcionalmente, forneça uma descrição amigável para a ID do locatário que ajuda a identificar o cliente que você está direcionando para o aditamento.

#### <a name="terms-and-conditions"></a>Termos e condições

Se você quiser fornecer seus próprios termos e condições personalizados, poderá optar por inseri-los no campo termos e condições. Você pode inserir até 10.000 caracteres de texto neste campo. Se seus termos e condições exigirem uma descrição mais longa, insira um link de URL único nesse campo, onde os termos e condições podem ser encontrados. Ele será exibido aos clientes como um link ativo.

Os clientes precisam aceitar esses termos antes de tentarem sua oferta.

Lembre-se de **salvar** antes de passar para a próxima seção.

## <a name="offer-listing"></a>Listagem de ofertas

A guia listagem de ofertas exibe os idiomas (e os mercados) onde sua oferta está disponível, atualmente em inglês (Estados Unidos) é o único local disponível. Além disso, essa página exibe o status da listagem específica do idioma e a data/hora em que ela foi adicionada. Você precisará definir os detalhes do Marketplace (nome da oferta, descrição, termos de pesquisa, etc.) para cada idioma/mercado.

> [!NOTE]
> A oferta de conteúdo de listagem (como descrição da oferta, documentos, capturas de tela, termos de uso e política de privacidade) não precisa estar em inglês, desde que a descrição da oferta comece com a frase ", este aplicativo está disponível somente em [idioma diferente do inglês]". Também é aceitável fornecer uma URL de *Link útil* para oferecer conteúdo em um idioma diferente daquele usado no conteúdo de listagem da oferta.

### <a name="offer-listings"></a>Listagens de oferta

Forneça detalhes a serem exibidos no Marketplace, incluindo descrições de sua oferta e ativos de marketing.

- **Nome** (obrigatório): o nome definido aqui será exibido como o título da listagem de oferta no (s) Marketplace (es) que você escolheu. O nome é preenchido previamente com base na nova entrada de **oferta** anterior. O nome pode ser marcado. Ele não pode conter emojis (a menos que sejam a marca registrada e os símbolos de direitos autorais) e deve ser limitado a 50 caracteres.
- **Resumo** (obrigatório): forneça uma breve descrição da sua oferta a ser usada em resultados da pesquisa de listagem (s) do Marketplace. Até 100 caracteres de texto podem ser inseridos neste campo.
- **Descrição** (obrigatório): forneça uma descrição da sua oferta a ser exibida na visão geral das listagem (s) do Marketplace. Considere incluir uma proposta de valor, benefícios principais, qualquer associação de categoria ou do setor, oportunidades de compra no aplicativo, quaisquer divulgações necessárias e um link para saber mais.
Até 3.000 caracteres de texto podem ser inseridos neste campo, incluindo marcação. Para obter dicas adicionais, consulte o artigo [escrever uma excelente descrição do aplicativo](https://docs.microsoft.com/windows/uwp/publish/write-a-great-app-description).
- **Pesquisar palavras-chave**: Insira até três palavras-chave de pesquisa que os clientes podem usar para localizar sua oferta no (s) Marketplace (es).
- **Instruções de introdução** (obrigatório): explique como configurar e começar a usar seu aplicativo para clientes potenciais.  Este guia de início rápido pode conter links para documentação online mais detalhada. Até 3.000 caracteres de texto podem ser inseridos neste campo.

#### <a name="description"></a>**Descrição**

Este campo é obrigatório. Itens a serem incluídos na **Descrição**:

* Descreva claramente a proposição de valor da sua oferta nas primeiras frases de sua descrição.  
* Tenha em mente que as primeiras frases podem ser exibidas nos resultados da pesquisa.  
* Não dependa de recursos e em funcionalidades para vender seu produto. Em vez disso, concentre-se no valor que você oferece.  
* Use o vocabulário específico do setor ou palavras com base no benefício tanto quanto possível.

Os componentes principais da sua proposta de valor devem incluir informações sobre:

* Descrição do produto.
* Tipo de usuário que se beneficia do produto.
* O cliente precisa ou problemático que o produto aborda.

Para tornar a **Descrição** da sua oferta mais atraente, use o editor de Rich Text para formatar sua descrição.

![Usando o editor de Rich Text](./media/text-editor2.png)

Use as instruções a seguir para usar o editor de Rich Text:

- Para alterar o formato do seu conteúdo, realce o texto que você deseja formatar e selecione um estilo de texto, conforme mostrado abaixo:

     ![Usando o editor de Rich Text para alterar o formato de texto](./media/text-editor3.png)

- Para adicionar uma lista com marcadores ou numerada ao texto, use as opções abaixo:

     ![Usando o editor de Rich Text para adicionar listas](./media/text-editor4.png)

- Para adicionar ou remover o recuo para o texto, use as opções abaixo:

     ![Usando o editor de Rich Text para recuar](./media/text-editor5.png)

#### <a name="links"></a>Links

- **Política de privacidade** (obrigatória): link para a política de privacidade da sua organização. Você é responsável por garantir que seu aplicativo esteja em conformidade com as leis e regulamentos de privacidade e para fornecer uma política de privacidade válida
- **Materiais de marketing do programa CSP** (opcional): forneça um link para materiais de marketing se você optar por estender sua oferta para o programa [CSP (provedor de soluções na nuvem)](https://docs.microsoft.com/azure/marketplace/cloud-solution-providers) . O CSP amplia sua oferta para uma variedade maior de clientes qualificados, permitindo que os parceiros do CSP agrupem, comercializam e revendam sua oferta. Esses revendedores precisarão de acesso aos materiais para marketing de sua oferta. Para obter mais informações, consulte [serviços de entrada no mercado](https://partner.microsoft.com/reach-customers/gtm).
- **Links úteis** (opcional): documentos online complementares opcionais sobre seu aplicativo ou serviços relacionados listados fornecendo um **título** e uma **URL**. Adicione links úteis adicionais clicando em **+ Adicionar uma URL**.

#### <a name="contact-information"></a>Informações de contato

- **Contatos**: para cada contato de cliente, forneça um **nome**de funcionário, **número de telefone**e endereço de **email** .  (Eles *não serão* exibidos publicamente). Uma **URL de suporte** também é necessária para o grupo de **contato de suporte** .  (Essas informações *serão* exibidas publicamente).

**Contato de suporte** (obrigatório): para perguntas de suporte geral.

**Contato de engenharia** (obrigatório): para perguntas técnicas.

**Contato do Gerenciador de canal** (obrigatório): para perguntas de revendedor relacionadas ao programa CSP.

#### <a name="files-and-images"></a>Arquivos e imagens

- **Documentos** (obrigatório): Adicione documentos de marketing relacionados para sua oferta, em formato PDF, fornecendo no mínimo um (1) e no máximo três (3) documentos por oferta.
- **Imagens** (opcional): há vários locais onde as imagens de logotipo da sua oferta podem aparecer em todo o Marketplace, exigindo os seguintes tamanhos--pequeno: 48 x 48 pixels _(obrigatório),_ médio: 90 x 90 pixels _(obrigatório)_ , grande: 216 x 216 pixels _(obrigatório),_ largo: 255 x 115 pixels e Hero: 815 x 290 pixels. Todas as imagens devem estar no. Formato PNG.
- **Capturas de tela** (obrigatórias): Adicionar capturas de tela que demonstram sua oferta. No máximo cinco (5) capturas de tela podem ser adicionadas e devem ser dimensionadas em 1280 x 720 pixels. Todas as imagens devem estar no. Formato PNG.
- **Vídeos** (opcional): adicionar links a vídeos demonstrando sua oferta. É possível usar links para vídeos do YouTube e/ou do Vimeo, que são mostrados juntamente com sua oferta aos clientes. Também será necessário inserir uma imagem em miniatura do vídeo, dimensionada para 1280 x 720 pixels no formato PNG. Você pode exibir um máximo de quatro vídeos por oferta.

Lembre-se de **salvar** antes de passar para a próxima seção.

#### <a name="additional-marketplace-listing-resources"></a>Recursos adicionais de listagem do Marketplace

- [Práticas recomendadas para listagens de ofertas do Marketplace](https://docs.microsoft.com/azure/marketplace/gtm-offer-listing-best-practices)

## <a name="preview"></a>{1&gt;Preview&lt;1}

A guia **Visualização** permite que você defina um **público de visualização** limitado para liberar sua oferta antes de publicar sua oferta em tempo real para o público mais amplo do Marketplace.

> [!IMPORTANT]
> Depois de verificar sua oferta em versão prévia, selecione **entrar em operação** para que sua oferta possa ser publicada em tempo real para o público público do Marketplace.

- **Definir um público de visualização: Adicione um único email de conta do AAD/MSA por linha, juntamente com uma descrição opcional.**

Adicione até dez (10) endereços de email manualmente ou vinte (20) se estiver carregando um arquivo CSV, para a conta da Microsoft existente (MSA) ou Azure Active Directory contas para ajudar a validar sua oferta antes de publicar em tempo real. Ao adicionar essas contas, você está definindo um público que terá permissão para visualizar o acesso à sua oferta antes que ele seja publicado no (s) Marketplace (es). Se sua oferta já estiver ativa, você ainda poderá definir um público de visualização para testar quaisquer alterações ou atualizações na sua oferta.

> [!NOTE]
> O público de visualização difere de um público privado. Um público de visualização tem permissão de acesso à sua oferta _antes_ de ser publicado em tempo real nos Marketplaces. Você também pode optar por criar um plano e torná-lo disponível somente para um público privado. Na guia **lista de planos** , você pode definir um público privado com a caixa de seleção **este é um plano privado** . Em seguida, você pode definir um público privado de até 20.000 clientes usando as IDs de locatário do Azure.

## <a name="technical-configuration"></a>Configuração técnica

A guia **configuração técnica** define os detalhes técnicos (caminho da URL, webhook, ID do locatário e ID do aplicativo) usados para se conectar à sua oferta. Essa conexão nos permite provisionar sua oferta para o cliente final se ele optar por adquiri-lo. Os diagramas que descrevem o uso dos campos coletados estão disponíveis na documentação para [APIs de preenchimento de SaaS](https://docs.microsoft.com/azure/marketplace/partner-center-portal/pc-saas-fulfillment-api-v2).

- **URL da página de aterrissagem** (obrigatório): defina a URL do site na qual os clientes serão acessados depois de adquirir sua oferta do Marketplace. Essa URL será o ponto de extremidade que recebe um token quando um cliente é roteado para a página. Esse token pode ser trocado para detalhes de provisionamento usando a resolução nas APIs de preenchimento. Esses detalhes e quaisquer outros que você coletar podem ser usados como parte de uma página da Web interativa pelo cliente, criada em sua experiência para concluir o registro e ativar sua compra.

- **Webhook de conexão** (obrigatório): para todos os eventos assíncronos que a Microsoft precisa enviar para você em nome do cliente (exemplo: a assinatura de SaaS deixou inválida), exigimos que você forneça um webhook de conexão. Se você ainda não tiver um sistema de webhook em vigor, a configuração mais simples é ter um aplicativo lógico de ponto de extremidade HTTP que escutará todos os eventos postados nele e, em seguida, tratá-los adequadamente (por exemplo, https:\//prod-1westus.logic.azure.com:443/work). Para saber mais, confira [Chamar, disparar ou aninhar fluxos de trabalho com pontos de extremidade HTTP em aplicativos lógicos](https://docs.microsoft.com/azure/logic-apps/logic-apps-http-endpoint).

- **ID de locatário do Azure ad** (obrigatório): dentro de portal do Azure, exigimos que você [crie um aplicativo de Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal) para que possamos validar a conexão entre nossos dois serviços está por trás de uma comunicação autenticada. Para localizar a [ID do locatário](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in), vá para o Azure Active Directory e selecione **Propriedades**, em seguida, procure o número de **ID de diretório** listado (por exemplo, 50c464d3-4930-494c-963c-1e951d15360e).

- **ID do aplicativo do Azure ad** (obrigatório): você também precisa da [ID do aplicativo](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) e de uma chave de autenticação. Para obter esses valores, vá para o Azure Active Directory e selecione **registros de aplicativo**, em seguida, procure o número de **ID do aplicativo** listado (por exemplo, 50c464d3-4930-494c-963c-1e951d15360e). Para localizar a chave de autenticação, vá para **configurações** e selecione **chaves**. Você precisará fornecer uma descrição e uma duração e, em seguida, será fornecido um valor numérico.

>[!Note]
>A ID do aplicativo do Azure está associada à sua ID de editor, portanto, certifique-se de que a mesma ID de aplicativo seja usada em todas as suas ofertas.

## <a name="plan-overview"></a>Visão geral do plano

A guia **visão geral do plano** permite que você forneça uma variedade de opções de plano na mesma oferta. Esses planos (às vezes chamados de SKUs) poderiam diferir em termos de versão, monetização ou camadas de serviço. Você deve configurar pelo menos um plano para vender sua oferta no Marketplace.

Depois de criado, você verá os nomes do plano, as IDs, os modelos de preços, a disponibilidade (pública ou privada), o status de publicação atual e as ações disponíveis.

As **ações** disponíveis na **visão geral do plano** variam de acordo com o status atual do seu plano e podem incluir:

- Se o status do plano for **rascunho** -excluir rascunho
- Se o status do plano for **Live** -parar o plano de venda ou sincronizar público privado

**Criar novo plano** (mínimo de um plano para aqueles que selecionam vender pela Microsoft)

- **ID do plano:** Crie uma ID de plano exclusiva para cada plano nesta oferta. Essa ID será visível para os clientes na URL do produto e nos modelos de Azure Resource Manager (se aplicável). Use apenas caracteres minúsculos, alfanuméricos, traços ou sublinhados. São permitidos no máximo 50 caracteres para essa ID de plano. A ID não pode ser modificada após a seleção de Create.
- **Nome do plano:** Os clientes verão esse nome ao decidir qual plano selecionar dentro de sua oferta. Crie um nome de oferta exclusivo para cada plano nesta oferta. O nome do plano é usado para diferenciar os planos de software que podem fazer parte da mesma oferta (por exemplo, nome da oferta: Windows Server; planos: Windows Server 2016, Windows Server 2019).

### <a name="plan-listing"></a>Lista de planos

A guia **lista de planos** exibe os idiomas (e os mercados) em que o plano está disponível, atualmente em inglês (Estados Unidos) é o único local disponível. Além disso, essa página exibe o status da listagem específica do idioma e a data/hora em que ela foi adicionada. Você precisará definir os detalhes do Marketplace (nome da oferta, descrição, termos de pesquisa, etc.) para cada idioma/mercado.

#### <a name="plan-listing-details"></a>Detalhes da listagem de plano

A seleção de uma das linguagens do plano exibirá as informações de **listagem do plano** , incluindo o **nome** e a **Descrição.**

- **Nome**: preenchido previamente com base na entrada do **novo plano** de visualização e aparecerá como o título do "plano de software" da sua oferta exibido no Marketplace.
- **Descrição:** Essa descrição é uma oportunidade para explicar o que torna este plano de software exclusivo e quaisquer diferenças de outros planos de software dentro de sua oferta. Pode conter até 500 caracteres.

Selecione **salvar** depois de concluir esses campos.

#### <a name="plan-pricing-and-availability"></a>Planejar preços e disponibilidade

A guia **preços e disponibilidade** permite que você configure os mercados nos quais esse plano estará disponível, o modelo de monetização, o preço e o termo de cobrança desejados. Além disso, você pode indicar se deseja tornar o plano visível para todos ou apenas para clientes específicos (um público privado).

##### <a name="enabling-free-trials"></a>Habilitando avaliações gratuitas

As ofertas de SaaS por meio do Marketplace comercial permitem que você forneça uma avaliação gratuita de um mês ao vender pela Microsoft. Para todos os modelos de cobrança e termos, exceto planos medidos, há suporte para avaliações gratuitas. Essa opção permite que os clientes tenham uma barreira baixa para entrada por meio de um mês de acesso gratuito.  Se você optar por habilitar uma avaliação gratuita para os planos em sua oferta, o cliente não poderá converter para uma assinatura paga antes do final do período de um mês inicial.  Durante esse tempo, os clientes que comprarem sua oferta poderão experimentar qualquer um dos planos com suporte que tenham a avaliação gratuita habilitada e convertê-los.  A conversão para uma assinatura paga é feita automaticamente no final do prazo.

>[!Note]
>Se o cliente optar por converter em um plano sem avaliações gratuitas, a conversão ocorrerá, mas a avaliação gratuita será perdida imediatamente.  Além disso, quando um cliente começa a pagar por um plano, ele não pode mais obter uma avaliação gratuita na mesma assinatura novamente, mesmo que eles convertam em uma SKU que ofereça suporte a avaliações gratuitas.

A capacidade de configurar uma avaliação gratuita está disponível para cada plano em sua oferta. Basta navegar até os preços e a disponibilidade de cada oferta e marcar a caixa para permitir uma avaliação de um mês.

![Caixa de seleção de avaliação gratuita de um mês](./media/free-trial-enable.png)

>[!Note]
>Depois que sua oferta de transação for publicada com uma avaliação gratuita, ela não poderá ser desabilitada para esse plano. Verifique se essa configuração está correta para a primeira publicação para evitar ter que recriar o plano.

Para obter informações sobre as assinaturas de cliente que estão participando de uma avaliação gratuita, use a nova propriedade de API `isFreeTrial`, que será marcada como verdadeira ou falsa. Para obter mais informações, consulte a [API de obter assinatura de SaaS](https://docs.microsoft.com/azure/marketplace/partner-center-portal/pc-saas-fulfillment-api-v2#get-subscription).

>[!Note]
>Não há suporte para avaliações gratuitas para planos que aproveitam o serviço de medição do Marketplace.

#### <a name="markets"></a>Mercados

- **Editar mercados** (opcional)

Cada plano deve estar disponível em pelo menos um mercado. Marque a caixa de seleção de qualquer local de mercado onde você gostaria de disponibilizar esse plano. Uma caixa de pesquisa e um botão para selecionar os países "impostos remetidos", no qual a Microsoft remete as vendas e o imposto sobre o uso em seu nome, estão incluídas para ajudar.

Se você já tiver definido preços para seu plano em dólares de Estados Unidos (USD) e adicionar outro local de mercado, o preço do novo mercado será calculado de acordo com as tarifas de câmbio atuais. Você sempre deve examinar o preço de cada mercado antes da publicação. Os preços podem ser revisados usando o link "exportar preços (xlsx)" depois de salvar as alterações.

#### <a name="pricing"></a>Preços

- **Modelo de preços**: taxa simples ou baseada em assentos

**Taxa fixa:** Habilite o acesso à sua oferta com um preço de taxa simples mensal ou anual. Isso às vezes é chamado de preços baseados em site. Com esse modelo de preços, opcionalmente, você pode definir planos medidos que usam a API do serviço de medição do Marketplace para cobrar clientes de acordo com unidades não padrão.  Para obter mais informações sobre cobrança limitada, consulte [cobrança limitada usando o serviço de medição do Marketplace](./saas-metered-billing.md).

**Por usuário:** Habilite o acesso à sua oferta com o preço com base no número de usuários que estão acessando a oferta ou ocupando estações. Esse modelo baseado no usuário permite que você defina o número mínimo e máximo de usuários permitidos com base no preço. Dessa forma, diferentes pontos de preço podem ser configurados com base no número de usuários Configurando vários planos.  Esses campos são opcionais. Se deixado desmarcado, o número de usuários será interpretado como não tendo um limite (mínimo de 1 e máximo de quantas o sistema pode oferecer suporte). Esses campos podem ser editados como parte de uma atualização para seu plano.

Depois de publicado, a opção de modelo de preços de cobrança não pode ser alterada. Além disso, todos os planos para a mesma oferta devem compartilhar o mesmo modelo de preços.

- **Termo de cobrança**: mensal ou anual

Selecione a frequência com que os clientes devem pagar o preço listado. Pelo menos um preço mensal ou anual deve ser fornecido ou ambas as opções podem ser disponibilizadas para os clientes.

- **Preço**: USD por mês ou USD por ano

Os preços definidos na moeda local (USD = Estados Unidos dólar) são convertidos na moeda local de todos os mercados selecionados usando as tarifas de câmbio atuais disponíveis durante a instalação. Valide esses preços antes de publicar exportando a planilha de preços e revisando o preço em cada mercado. Se você quiser definir preços personalizados em um mercado individual, modifique e importe a planilha de preços. Você é responsável por validar esse preço e possuir essas configurações.
*\*você deve primeiro salvar as alterações de preços para habilitar a exportação de dados de preços.*

Examine seus preços cuidadosamente antes de publicar, pois há algumas restrições sobre o que pode ser alterado depois que um plano é publicado:

- Depois que um plano é publicado, o modelo de preços não pode ser alterado.
- Depois que um termo de cobrança for publicado para um plano, ele não poderá ser removido mais tarde.
- Depois que o preço de um mercado em seu plano for publicado, ele não poderá ser alterado posteriormente.

### <a name="plan-audience"></a>Planejar público

Você tem a opção de configurar cada plano para ser visível para todos ou apenas para um público específico de sua escolha. Você pode atribuir associação a esse público restrito usando as IDs de locatário do Azure AD.

#### <a name="privacy"></a>Privacidade

- **Este é um plano privado** (caixa de seleção opcional)

Marque esta caixa para tornar seu plano privado e visível somente para o público restrito de sua escolha. Depois de publicado como um plano privado, você pode atualizar o público ou optar por disponibilizar o plano para todos. Depois que um plano é publicado como visível para todos, ele deve permanecer visível para todos. (O plano não pode ser configurado como um plano privado novamente).

- **Público-alvo restrito (IDs de locatário)**

Atribua o público que terá acesso a este plano privado. O acesso é atribuído usando IDs de locatário com a opção de incluir uma descrição de cada ID de locatário atribuída. Um máximo de 10 IDs de locatário pode ser adicionado ou 20.000 clientes IDs de locatário se importar um arquivo de planilha. csv.

Um locatário é uma representação de uma organização, com uma ID representada como um GUID (identificador global exclusivo, um número inteiro de 128 bits usado para identificar recursos). É uma instância dedicada do Azure AD que uma organização ou um desenvolvedor de aplicativos recebe ao criar uma relação com Microsoft, como inscrever-se no Azure, no Microsoft Intune ou no Microsoft 365. Cada locatário do AD do Azure é distinto e separado de outros diretórios do AD do Azure. Para verificar o locatário, entre no portal do Azure com a conta que você deseja usar para gerenciar seu aplicativo. Se houver um locatário, você será conectado a ele automaticamente e verá o nome do locatário diretamente abaixo do nome da conta. Passe o mouse sobre o nome da conta no canto superior direito do portal do Azure para ver seu nome, email, diretório e ID do locatário (um GUID) e seu domínio. Se sua conta estiver associada a vários locatários, você pode selecionar o nome da sua conta para abrir um menu no qual você pode alternar entre locatários. Cada locatário tem sua própria ID exclusiva. Você também pode pesquisar a ID de locatário da sua organização usando uma URL de nome de domínio em: [https://www.whatismytenantid.com](https://www.whatismytenantid.com).

Embora o SaaS ofereça usar IDs de locatário para definir um público privado, outros tipos de oferta podem usar IDs de assinatura do Azure (que também são representadas como GUIDs).

> [!NOTE]
> O público privado (ou público restrito) difere de um público de visualização. Na guia **[Visualização](#preview)** , você pode definir um público de visualização. Um público de visualização tem permissão de acesso à sua oferta *antes* que a oferta seja publicada ao vivo no Marketplace. Embora a designação de público privado se aplique apenas a um plano específico, o público-alvo da visualização pode exibir todos os planos (privado ou não), mas somente durante o período de visualização limitado, enquanto o plano é testado e validado.

## <a name="example-list-of-plans-within-a-marketplace-offer"></a>Exemplo de lista de planos em uma oferta do Marketplace

![Exemplo de listagem de planos do Marketplace com observações](./media/marketplace-plan.svg)

## <a name="test-drive"></a>Test drive

[!INCLUDE [Test drive content](./includes/commercial-marketplace-test-drive.md)]

## <a name="cloud-solution-provider-csp-reseller-audience"></a>Público do revendedor do CSP (provedor de soluções na nuvem)

Optar por tornar sua oferta disponível no programa CSP permite que os provedores de soluções de nuvem vendam seu produto como parte de uma solução agrupada para seus clientes. Para obter mais informações, consulte [provedores de soluções de nuvem](https://go.microsoft.com/fwlink/?linkid=2111109).

## <a name="publish"></a>Publicar

Depois de concluir todas as seções necessárias da oferta, selecione **publicar** no canto superior direito do Portal. Você será redirecionado para a página **revisar e publicar** .

#### <a name="submit-offer-to-preview"></a>Enviar oferta para visualização

Se esta for a primeira vez que você publica essa oferta, você pode:

- Consulte o status de conclusão de cada seção da oferta.
    - *Não iniciado* -significa que a seção não foi tocada e precisa ser concluída.
    - *Incompleto* -significa que a seção tem erros que precisam ser corrigidos ou que requer mais informações a serem fornecidas. Você precisará voltar para a seção e atualizá-la.
    - *Concluir* -significa que a seção está concluída, todos os dados necessários foram fornecidos e não há erros. Todas as seções da oferta devem estar em um estado completo antes que você possa enviar a oferta.
- Forneça instruções de teste à equipe de certificação para garantir que seu aplicativo seja testado corretamente, além de qualquer nota suplementar útil para entender seu aplicativo.
- Envie a oferta para publicação selecionando **Enviar**. Enviaremos um email para que você saiba quando uma versão prévia da oferta está disponível para revisão e aprovação. Você deve retornar ao Partner Center e selecionar **Go-Live** para a oferta para publicar sua oferta no público (ou se uma oferta privada, para o público privado).

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

- [Atualizar uma oferta existente no Marketplace comercial](./update-existing-offer.md)
