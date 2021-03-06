---
title: Criar funções Web e de trabalho do Azure para PHP
description: Um guia para a criação de funções da Web do PHP e de trabalho em um serviço de nuvem do Azure e para a configuração do runtime do PHP.
services: ''
documentationcenter: php
author: msangapu
manager: cfowler
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/11/2018
ms.author: msangapu
ms.openlocfilehash: 54410e1e70a2ec0d3a9e2f853dc9556cd05996ad
ms.sourcegitcommit: c29b7870f1d478cec6ada67afa0233d483db1181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79297247"
---
# <a name="create-php-web-and-worker-roles"></a>Criar funções de trabalho e funções Web de PHP

## <a name="overview"></a>Visão geral

Este guia mostrará como criar funções Web ou de trabalho do PHP em um ambiente de desenvolvimento Windows, como escolher uma versão específica do PHP nas versões "internas" disponíveis, como alterar a configuração do PHP, habilitar extensões e, finalmente, como implantar no Azure. Também descreve como configurar uma função Web ou de trabalho para usar um runtime do PHP (com configuração e extensões personalizadas) que você fornece.

O Azure fornece três modelos de computação para a execução de aplicativos: Serviço de Aplicativo do Azure, Máquinas Virtuais do Azure e Serviços de Nuvem do Azure. Todos os três modelos oferecem suporte ao PHP. Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)* . Dentro de um serviço de nuvem, uma função web fornece um servidor Web de IIS (Serviços de Informações da Internet) dedicado, usado para hospedar aplicativos Web de front-end. Uma função de trabalho pode executar tarefas assíncronas, de execução longa ou perpétuas, independentemente da interação do usuário ou da entrada.

Para obter mais informações sobre essas opções, consulte [Opções de hospedagem de computação fornecidas pelo Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-the-azure-sdk-for-php"></a>Baixar o SDK do Azure para PHP

O [SDK do Azure para PHP](https://github.com/Azure/azure-sdk-for-php) consiste em vários componentes. Este artigo usará dois deles: o Azure PowerShell e os emuladores do Azure. Esses dois componentes podem ser instalados pelo Microsoft Web Platform Installer. Para obter mais informações, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Criar um projeto de Serviço de Nuvem

A primeira etapa na criação de uma função Web ou de trabalho do PHP é criar um projeto de Serviço do Azure. um projeto de Serviço do Azure serve como um contêiner lógico para as funções da Web e de trabalho, e contém os arquivos de [definição do serviço (.csdef)] e [configuração do serviço (.cscfg)] do projeto.

Para criar um novo projeto de Serviço do Azure, execute o Azure PowerShell como administrador e execute o seguinte comando:

    PS C:\>New-AzureServiceProject myProject

Esse comando criará um novo diretório (`myProject`) ao qual você pode adicionar funções Web e de trabalho.

## <a name="add-php-web-or-worker-roles"></a>Adicionar funções de trabalho ou Web PHP

Para adicionar uma função Web do PHP a um projeto, execute o seguinte comando no diretório raiz do projeto:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Para uma função de trabalho, use este comando:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> O `roleName` é opcional. Se for omitido, o nome da função será gerado automaticamente. A primeira função web criada será `WebRole1`, a segunda será `WebRole2` e assim por diante. A primeira função de trabalho criada será `WorkerRole1`, a segunda será `WorkerRole2` e assim por diante.
>
>

## <a name="use-your-own-php-runtime"></a>Usar seu próprio runtime PHP

Em alguns casos, em vez de selecionar um runtime do PHP interno e configurá-lo conforme descrito acima, você pode desejar fornecer seu próprio runtime do PHP. Por exemplo, você pode usar o mesmo runtime do PHP em uma função Web ou de trabalho que você usa no seu ambiente de desenvolvimento. Isso torna mais fácil garantir que o aplicativo não mudará o comportamento no ambiente de produção.

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a>Configurar uma função web para usar o seu próprio runtime do PHP

Para configurar uma função web para usar um runtime do PHP fornecido por você, siga as etapas a seguir:

1. Crie um projeto de Serviço do Azure e adicione uma função Web do PHP conforme descrito anteriormente neste tópico.
2. Crie uma pasta `php` na pasta `bin` que está no diretório raiz de sua função web e adicione o runtime do PHP (todos os binários, arquivos de configuração, subpastas etc.) à pasta `php`.
3. ADICIONAL Se o tempo de execução do PHP usar os [drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará configurar sua função Web para instalar o [SQL Server Native Client 2012][sql native client] quando ele for provisionado. Para fazer isso, adicione o [instalador sqlncli.msi x64] à pasta `bin` no diretório-raiz de sua função Web. O script de inicialização descrito na próxima etapa executará o instalador silenciosamente quando a função for provisionada. Se o runtime do PHP não usar os Drivers Microsoft para PHP para SQL Server, você poderá remover a seguinte linha do script mostrado na próxima etapa:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Defina uma tarefa de inicialização que configure [serviços de informações da Internet (IIS)][iis.net] para usar o tempo de execução do PHP para lidar com solicitações de `.php` páginas. Para fazer isso, abra o arquivo `setup_web.cmd` (no arquivo `bin` do diretório raiz da função web) em um editor de texto e substitua seu conteúdo pelo script a seguir:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Adicione os arquivos do aplicativo ao diretório raiz da função Web. Esse será o diretório raiz do servidor web.
6. Publique seu aplicativo como descrito na seção abaixo, [Publicar seu aplicativo](#publish-your-application).

> [!NOTE]
> O script `download.ps1` (na pasta `bin` do diretório raiz da função web) pode ser excluído após a realização das etapas descritas acima para usar seu próprio runtime do PHP.
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a>Configurar uma função de trabalho para usar o seu próprio runtime do PHP

Para configurar uma função de trabalho para usar um runtime do PHP fornecido por você, siga as etapas a seguir:

1. Crie um projeto de Serviço do Azure e adicione uma função de trabalho do PHP conforme descrito anteriormente neste tópico.
2. Crie uma pasta `php` no diretório raiz de sua função de trabalho e adicione o runtime do PHP (todos os binários, arquivos de configuração, subpastas etc.) para a pasta `php`.
3. ADICIONAL Se o tempo de execução do PHP usar [drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], será necessário configurar sua função de trabalho para instalar o [SQL Server Native Client 2012][sql native client] quando ele for provisionado. Para fazer isso, adicione o [instalador sqlncli.msi x64] ao diretório raiz da função de trabalho. O script de inicialização descrito na próxima etapa executará o instalador silenciosamente quando a função for provisionada. Se o runtime do PHP não usar os Drivers Microsoft para PHP para SQL Server, você poderá remover a seguinte linha do script mostrado na próxima etapa:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Defina uma tarefa de inicialização que adiciona o executável `php.exe` à variável de ambiente PATH da função de trabalho quando a função é configurada. Para fazer isso, abra o arquivo `setup_worker.cmd` (no diretório raiz da função de trabalho) em um editor de texto e substitua seu conteúdo pelo script a seguir:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Adicione os arquivos do aplicativo ao diretório raiz da função de trabalho.
6. Publique seu aplicativo como descrito na seção abaixo, [Publicar seu aplicativo](#publish-your-application).

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a>Executar seu aplicativo nos emuladores de computação e de armazenamento

Os emuladores do Azure fornecem um ambiente local no qual você pode testar seu aplicativo do Azure antes de implantá-lo na nuvem. Existem algumas diferenças entre os emuladores e o ambiente do Azure. Para entender isso melhor, consulte [Usar o emulador de armazenamento do Azure para desenvolvimento e teste](storage/common/storage-use-emulator.md).

Observe que você deve ter instalado o PHP localmente para usar o emulador de computação. O emulador de computação usará sua instalação local do PHP para executar o aplicativo.

Para executar seu projeto nos emuladores, execute o seguinte comando no diretório raiz do projeto:

    PS C:\MyProject> Start-AzureEmulator

Você verá uma saída semelhante a essa:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Você pode ver o aplicativo em execução no emulador abrindo um navegador da Web e navegando até o endereço local mostrado na saída (`http://127.0.0.1:81` na saída de exemplo acima).

Para parar os emuladores, execute este comando:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Publicar seu aplicativo

Para publicar seu aplicativo, você precisa primeiro importar suas configurações de publicação usando o cmdlet [Import-AzurePublishSettingsFile](https://docs.microsoft.com/powershell/module/servicemanagement/azure/import-azurepublishsettingsfile) . Em seguida, você pode publicar o aplicativo usando o cmdlet [Publish-AzureServiceProject](https://docs.microsoft.com/powershell/module/servicemanagement/azure/publish-azureserviceproject) . Para obter informações sobre como entrar, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte o [Centro de Desenvolvimento PHP](https://azure.microsoft.com/develop/php/).

[install ps and emulators]: https://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definição do serviço (.csdef)]: https://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuração do serviço (.cscfg)]: https://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: https://www.iis.net/
[sql native client]: https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation
[sqlsrv drivers]: https://php.net/sqlsrv
[instalador sqlncli.msi x64]: https://go.microsoft.com/fwlink/?LinkID=239648
