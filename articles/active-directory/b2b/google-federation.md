---
title: Adicionar o Google como um provedor de identidade para B2B-Azure AD
description: Associe ao Google para permitir que usuários convidados entrem em seus aplicativos Azure AD usando as próprias contas do Gmail
services: active-directory
ms.service: active-directory
ms.subservice: B2B
ms.topic: conceptual
ms.date: 03/05/2020
ms.author: mimart
author: msmimart
manager: celestedg
ms.reviewer: mal
ms.custom: it-pro, seo-update-azuread-jan
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72c18e48c27942c7bea47931ec79a31af941064e
ms.sourcegitcommit: f97d3d1faf56fb80e5f901cd82c02189f95b3486
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79126667"
---
# <a name="add-google-as-an-identity-provider-for-b2b-guest-users"></a>Adicionar o Google como provedor de identidade para usuários convidados B2B

Ao configurar a Federação com o Google, você pode permitir que os usuários convidados entrem em seus aplicativos compartilhados e recursos com suas próprias contas do Gmail, sem precisar criar contas da Microsoft (MSAs). 

> [!NOTE]
> O Google Federation foi projetado especificamente para usuários do gmail. Para federar com domínios do G Suite, use o [recurso de Federação direta](direct-federation.md).

## <a name="what-is-the-experience-for-the-google-user"></a>Qual é a experiência do usuário do Google?
Quando você envia um convite para um usuário do Google Gmail, o usuário convidado deve acessar seus aplicativos ou recursos compartilhados utilizando um link que inclui o contexto do locatário. A experiência varia dependendo de a conexão ao Google já ter ocorrido ou não:
  - Se o usuário convidado não entrou no Google, a conexão ao Google será solicitada.
  - Se o usuário convidado já entrou no Google, ele poderá escolher a conta que deseja usar. Ele precisa escolher a conta que foi usada para convidá-lo.

Se o usuário convidado vir um erro de "cabeçalho muito longo", poderá tentar limpar os cookies ou abrir uma janela particular ou incógnita e tentar entrar novamente.

![Captura de tela mostrando a página de entrada do Google](media/google-federation/google-sign-in.png)

## <a name="limitations"></a>Limitações

As equipes dão suporte total aos usuários convidados do Google em todos os dispositivos. Os usuários do Google podem entrar em equipes de um ponto de extremidade comum, como `https://teams.microsoft.com`.

Os pontos de extremidade comuns de outros aplicativos podem não dar suporte a usuários do Google. Os usuários convidados do Google devem entrar usando um link que inclui suas informações de locatário. Veja a seguir exemplos:
  * `https://myapps.microsoft.com/?tenantid=<your tenant id>`
  * `https://portal.azure.com/<your tenant id>`
  * `https://myapps.microsoft.com/<your verified domain>.onmicrosoft.com`

   Se os usuários convidados do Google tentarem usar um link como `https://myapps.microsoft.com` ou `https://portal.azure.com`, eles receberão um erro.

Você também pode conceder aos usuários convidados do Google um link direto para um aplicativo ou recurso, contanto que esse link inclua as informações de seu locatário, por exemplo `https://myapps.microsoft.com/signin/Twitter/<application ID?tenantId=<your tenant ID>`. 

## <a name="step-1-configure-a-google-developer-project"></a>Etapa 1: Configurar um projeto de desenvolvedor do Google
Primeiramente, crie um novo projeto no Console de Desenvolvedores do Google para obter um ID do cliente e um segredo do cliente que possa adicionar posteriormente ao Azure AD. 
1. Acesse as APIs do Google em https://console.developers.google.com e entre com sua conta do Google. É recomendável que você use uma conta do Google de equipe compartilhada.
2. Crie um novo projeto: no painel, selecione **Criar projeto** e, em seguida, selecione **Criar**. Na página Novo projeto, insira um **Nome do projeto** e, em seguida, selecione **Criar**.
   
   ![Captura de tela mostrando uma nova página de projeto para o Google](media/google-federation/google-new-project.png)

3. Verifique se seu novo projeto está selecionado no menu do projeto. Em **APIs & serviços**, selecione **tela de consentimento do OAuth**.

4. Selecione **externo**e, em seguida, selecione **criar**. 
5. Na **tela de consentimento do OAuth**, insira um nome de **aplicativo**. (Deixe as outras configurações.)

   ![Captura de tela mostrando a opção de ecrã de consentimento do Google OAuth](media/google-federation/google-oauth-consent-screen.png)

6. Role até a **autorizado domínios** seção e insira microsoftonline.com.

   ![Captura de tela mostrando a seção domínios autorizados](media/google-federation/google-oauth-authorized-domains.png)

7. Selecione **Salvar**.

8. Escolha **credenciais**. No menu **Criar credenciais**, escolha **ID do cliente OAuth**.

   ![Captura de tela mostrando a opção criar credenciais do Google APIs](media/google-federation/google-api-credentials.png)

9. Em **Tipo de aplicativo**, escolha **Aplicativo Web** e, em **URIs de redirecionamento autorizados**, insira estes URIs:
   - `https://login.microsoftonline.com` 
   - `https://login.microsoftonline.com/te/<directory id>/oauth2/authresp` <br>(em que `<directory id>` é a ID do seu diretório)
   
     > [!NOTE]
     > Para localizar a ID do seu diretório, acesse https://portal.azure.com e, em **Azure Active Directory**, escolha **Propriedades** e copie o **ID do diretório**.

   ![Captura de tela mostrando a seção de URIs de redirecionamento autorizados](media/google-federation/google-create-oauth-client-id.png)

10. Selecione **Criar**. Copie a ID do cliente e o segredo do cliente, que você usará quando adicionar o provedor de identidade no portal do Azure AD.

   ![Captura de tela mostrando a ID do cliente OAuth e o segredo do cliente](media/google-federation/google-auth-client-id-secret.png)

## <a name="step-2-configure-google-federation-in-azure-ad"></a>Etapa 2: Configurar a federação do Google no Azure AD 
Agora, você definirá a ID do cliente e o segredo do cliente do Google, seja inserindo-o no portal do Azure AD ou usando o PowerShell. Lembre-se de testar sua configuração da federação do Google. Convide-se usando um endereço do Gmail e tente resgatar o convite com sua conta do Google convidada. 

#### <a name="to-configure-google-federation-in-the-azure-ad-portal"></a>Como configurar a federação do Google no portal do Azure AD 
1. Vá para o [Portal do Azure](https://portal.azure.com). No painel esquerdo, selecione **Azure Active Directory**. 
2. Selecione **Relações organizacionais**.
3. Selecione **Provedores de identidade** e, em seguida, clique no botão **Google**.
4. Insira um nome. Em seguida, insira a ID do cliente e o segredo do cliente obtidos anteriormente. Selecione **Salvar**. 

   ![Captura de tela mostrando a página Adicionar provedor de identidade do Google](media/google-federation/google-identity-provider.png)

#### <a name="to-configure-google-federation-by-using-powershell"></a>Como configurar a federação do Google usando o PowerShell
1. Instale a versão mais recente do módulo PowerShell for Graph ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)) do Azure AD.
2. Execute o seguinte comando: `Connect-AzureAD`.
3. No prompt de entrada, entre com a conta de Administrador Global gerenciada.  
4. Execute o comando a seguir: 
   
   `New-AzureADMSIdentityProvider -Type Google -Name Google -ClientId [Client ID] -ClientSecret [Client secret]`
 
   > [!NOTE]
   > Use a ID do cliente e o segredo do cliente do aplicativo criado na "Etapa 1: Configurar um projeto de desenvolvedor do Google". Para obter mais informações, consulte o artigo [New-AzureADMSIdentityProvider](https://docs.microsoft.com/powershell/module/azuread/new-azureadmsidentityprovider?view=azureadps-2.0-preview). 
 
## <a name="how-do-i-remove-google-federation"></a>Como fazer a remoção da federação do Google?
É possível excluir sua configuração da federação do Google. Se fizer isso, os usuários convidados do Google que já resgataram seu convite não conseguirão entrar, mas você poderá conceder novamente a eles o acesso a seus recursos se os excluir do diretório e convidá-los outra vez. 
 
### <a name="to-delete-google-federation-in-the-azure-ad-portal"></a>Para excluir a federação do Google no portal do Azure AD: 
1. Vá para o [Portal do Azure](https://portal.azure.com). No painel esquerdo, selecione **Azure Active Directory**. 
2. Selecione **Relações organizacionais**.
3. Selecione **provedores de identidade**.
4. Na linha do **Google** , selecione o menu de contexto ( **...** ) e, em seguida, selecione **excluir**. 
   
   ![Captura de tela mostrando a opção Excluir para o provedor de identidade social](media/google-federation/google-social-identity-providers.png)

1. Clique em **Sim** para confirmar a exclusão. 

### <a name="to-delete-google-federation-by-using-powershell"></a>Para excluir a federação do Google usando o PowerShell: 
1. Instale a versão mais recente do módulo PowerShell for Graph ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)) do Azure AD.
2. Execute `Connect-AzureAD`.  
4. No prompt de logon, entre com a conta de Administrador Global gerenciada.  
5. Insira o seguinte comando:

    `Remove-AzureADMSIdentityProvider -Id Google-OAUTH`

   > [!NOTE]
   > Para obter mais informações, consulte [AzureADMSIdentityProvider remover](https://docs.microsoft.com/powershell/module/azuread/Remove-AzureADMSIdentityProvider?view=azureadps-2.0-preview). 
