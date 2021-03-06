---
title: 'Tutorial: Integração do SSO (logon único) do Azure Active Directory ao Greenlight Compliant Access Management | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Greenlight Compliant Access Management.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 47a80d88-d921-4fae-8c05-818662c396f5
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 04/03/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 85fb972027170871cad62133965c7dc43d6374a3
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/24/2020
ms.locfileid: "78968432"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-greenlight-compliant-access-management"></a>Tutorial: Integração do SSO (logon único) do Azure Active Directory ao Greenlight Compliant Access Management

Neste tutorial, você aprenderá a integrar o Greenlight Compliant Access Management ao Azure AD (Azure Active Directory). Ao integrar o Greenlight Compliant Access Management ao Azure AD, você pode:

* Controlar no Azure AD que tem acesso ao Greenlight Compliant Access Management.
* Permitir que os usuários sejam conectados automaticamente ao Greenlight Compliant Access Management com as respectivas contas do Azure AD.
* Gerenciar suas contas em um local central: o portal do Azure.

Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, confira [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on).

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Caso você não tenha uma assinatura, obtenha uma [conta gratuita](https://azure.microsoft.com/free/).
* Assinatura habilitada para SSO (logon único) do Greenlight Compliant Access Management.

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o SSO do Azure AD em um ambiente de teste.

* O Greenlight Compliant Access Management dá suporte ao SSO iniciado por **SP e IdP**
* Depois de configurar o Greenlight Compliant Access Management, você poderá impor um controle de sessão, que fornece proteção contra exfiltração e infiltração dos dados confidenciais da sua organização em tempo real. O controle da sessão é estendido do Acesso Condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-greenlight-compliant-access-management-from-the-gallery"></a>Como adicionar o Greenlight Compliant Access Management por meio da galeria

Para configurar a integração do Greenlight Compliant Access Management ao Azure AD, você precisará adicionar o Greenlight Compliant Access Management por meio da galeria à lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) usando uma conta corporativa ou de estudante ou uma conta pessoal da Microsoft.
1. No painel de navegação esquerdo, escolha o serviço **Azure Active Directory**.
1. Navegue até **Aplicativos Empresariais** e, em seguida, escolha **Todos os Aplicativos**.
1. Para adicionar um novo aplicativo, escolha **Novo aplicativo**.
1. Na seção **Adicionar por meio da galeria**, digite **Greenlight Compliant Access Management** na caixa de pesquisa.
1. Selecione **Greenlight Compliant Access Management** no painel de resultados e, em seguida, adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.

## <a name="configure-and-test-azure-ad-single-sign-on-for-greenlight-compliant-access-management"></a>Configurar e testar o logon único do Azure AD para o Greenlight Compliant Access Management

Configure e teste o SSO do Azure AD com o Greenlight Compliant Access Management usando um usuário de teste chamado **B.Fernandes**. Para que o SSO funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Greenlight Compliant Access Management.

Para configurar e testar o SSO do Azure AD com o Greenlight Compliant Access Management, conclua os seguintes blocos de construção:

1. **[Configurar o SSO do Azure AD](#configure-azure-ad-sso)** – para permitir que os usuários usem esse recurso.
    * **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD com B.Fernandes.
    * **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que B.Fernandes use o logon único do Azure AD.
1. **[Configurar o SSO do Greenlight Compliant Access Management](#configure-greenlight-compliant-access-management-sso)** : para configurar o logon único no lado do aplicativo.
    * **[Criar um usuário de teste do Greenlight Compliant Access Management](#create-greenlight-compliant-access-management-test-user)** : para ter um equivalente de B.Fernandes no Greenlight Compliant Access Management que esteja vinculado à representação de usuário do Azure AD.
1. **[Testar o SSO](#test-sso)** – para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **Greenlight Compliant Access Management**, localize a seção **Gerenciar** e selecione **Logon único**.
1. Na página **Selecionar um método de logon único**, escolha **SAML**.
1. Na página **Configurar o logon único com o SAML**, clique no ícone de edição/caneta da **Configuração Básica do SAML** para editar as configurações.

   ![Editar a Configuração Básica de SAML](common/edit-urls.png)

1. Na seção **Configuração Básica do SAML**, caso deseje configurar o aplicativo no modo iniciado por **IDP**, digite os valores dos seguintes campos:

    a. No **identificador** caixa de texto, digite uma URL usando o seguinte padrão: `https://<CUSTOMER>.greenlightcorp.com/ebcpresq/checkLoginSAML.do`

    b. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://<CUSTOMER>.greenlightcorp.com/ebcpresq/checkLoginSAML.do`

1. Clique em **Definir URLs adicionais** e execute o passo seguinte se quiser configurar a aplicação no modo **SP** iniciado:

    Na caixa de texto **URL de logon**, digite um URL usando o seguinte padrão: `https://<CUSTOMER>.greenlightcorp.com/ebcpresq/checkLoginSAML.do`

    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais. Entre em contato com a [equipe de suporte ao cliente do Greenlight Compliant Access Management](mailto:support@greenlightcorp.com) para obter esses valores. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

1. Na página **Configurar o logon único com o SAML**, na seção **Certificado de Autenticação SAML**, localize **XML de Metadados de Federação** e selecione **Baixar** para baixar o certificado e salvá-lo no computador.

    ![O link de download do Certificado](common/metadataxml.png)

1. Na seção **Configurar o Greenlight Compliant Access Management**, copie as URLs apropriadas de acordo com as suas necessidades.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, você criará um usuário de teste no portal do Azure chamado B.Fernandes.

1. No painel esquerdo do portal do Azure, escolha **Azure Active Directory**, **Usuários** e, em seguida, **Todos os usuários**.
1. Selecione **Novo usuário** na parte superior da tela.
1. Nas propriedades do **Usuário**, siga estas etapas:
   1. No campo **Nome**, insira `B.Simon`.  
   1. No campo **Nome de usuário**, insira username@companydomain.extension. Por exemplo, `B.Simon@contoso.com`.
   1. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha**.
   1. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que B.Fernandes use o logon único do Azure permitindo acesso ao Greenlight Compliant Access Management.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.
1. Na lista de aplicativos, selecione **Greenlight Compliant Access Management**.
1. Na página de visão geral do aplicativo, localize a seção **Gerenciar** e escolha **Usuários e grupos**.

   ![O link “Usuários e grupos”](common/users-groups-blade.png)

1. Escolha **Adicionar usuário** e, em seguida, **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição**.

    ![O link Adicionar Usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos**, selecione **B.Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função**, escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar atribuição**, clique no botão **Atribuir**.

## <a name="configure-greenlight-compliant-access-management-sso"></a>Configurar o SSO do Greenlight Compliant Access Management

Para configurar o logon único no lado do **Greenlight Compliant Access Management**, é necessário enviar o **XML de Metadados de Federação** baixado e as URLs apropriadas copiadas do portal do Azure para a [equipe de suporte do Greenlight Compliant Access Management](mailto:support@greenlightcorp.com). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-greenlight-compliant-access-management-test-user"></a>Criar um usuário de teste do Greenlight Compliant Access Management

Nesta seção, você criará um usuário chamado B.Fernandes no Greenlight Compliant Access Management. Trabalhe com a [equipe de suporte do Greenlight Compliant Access Management](mailto:support@greenlightcorp.com) para adicionar os usuários à plataforma Greenlight Compliant Access Management. Os usuários devem ser criados e ativados antes de usar o logon único.

## <a name="test-sso"></a>Testar o SSO 

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Greenlight Compliant Access Management no Painel de Acesso, você deverá ser conectado automaticamente ao Greenlight Compliant Access Management, para o qual configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos adicionais

- [ Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Experimentar o Greenlight Compliant Access Management com o Azure AD](https://aad.portal.azure.com/)

- [O que é controle de sessão no Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)

- [Como proteger o Greenlight Compliant Access Management com visibilidade e controles avançados](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)