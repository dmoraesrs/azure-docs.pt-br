---
title: Conectividade SSL-banco de dados do Azure para MariaDB
description: Informações para configurar o Banco de Dados do Azure para MariaDB e aplicativos associados a fim de usar as conexões SSL adequadamente
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.topic: conceptual
ms.date: 03/10/2020
ms.openlocfilehash: c03a56176a6e2cc995e74017b60747541fc843bb
ms.sourcegitcommit: 512d4d56660f37d5d4c896b2e9666ddcdbaf0c35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79371623"
---
# <a name="ssl-connectivity-in-azure-database-for-mariadb"></a>Conectividade SSL no Banco de Dados do Azure para MariaDB
O Banco de Dados do Azure para MariaDB dá suporte à conexão de seu servidor de banco de dados com aplicativos cliente usando o protocolo SSL. Impor conexões SSL entre seu servidor de banco de dados e os aplicativos cliente ajuda a proteger contra ataques de "intermediários" criptografando o fluxo de dados entre o servidor e seu aplicativo.

## <a name="default-settings"></a>Configurações padrão
Por padrão, o serviço de banco de dados deve ser configurado para exigir conexões SSL ao se conectar ao MariaDB.  Recomendamos evitar desabilitar a opção SSL sempre que possível.

Ao provisionar um novo servidor de Banco de Dados do Azure para MariaDB por meio do portal do Azure e da CLI do Azure, a imposição de conexões SSL está habilitada por padrão.

Cadeias de conexão para várias linguagens de programação são mostradas no Portal do Azure. Essas cadeias de conexão incluem os parâmetros SSL necessários para conectar-se ao banco de dados. No Portal do Azure, selecione seu servidor. No cabeçalho **Configurações**, selecione as **Cadeias de conexão**. O parâmetro SSL varia de acordo com o conector, por exemplo "ssl=true" ou "sslmode=require" ou "sslmode=required" e outras variações.

Para saber como habilitar ou desabilitar a conexão SSL durante o desenvolvimento de aplicativos, consulte [Como configurar o SSL](howto-configure-ssl.md).

## <a name="tls-connectivity-in-azure-database-for-mariadb"></a>Conectividade TLS no banco de dados do Azure para MariaDB

O banco de dados do Azure para MariaDB dá suporte à criptografia para clientes que se conectam ao servidor de banco de dados usando o protocolo TLS. O TLS é um protocolo padrão do setor que garante conexões de rede seguras entre o servidor de banco de dados e os aplicativos cliente, permitindo que você atenda aos requisitos de conformidade.

### <a name="tls-settings"></a>Configurações de protocolo TLS

O banco de dados do Azure para MariaDB fornece a capacidade de impor a versão de TLS para as conexões de cliente. Para usar a opção TLS, use a configuração de opção de **versão mínima do TLS** . Os valores a seguir são permitidos para esta configuração de opção:

|  Configuração de TLS mínima             | Versão de TLS com suporte                |
|:---------------------------------|-------------------------------------:|
| TLSEnforcementDisabled (padrão) | Não é necessário TLS                      |
| TLS1_0                           | TLS 1,0, TLS 1,1, TLS 1,2 e superior |
| TLS1_1                           | TLS 1,1, TLS 1,2 e superior          |
| TLS1_2                           | TLS versão 1,2 e superior           |


Por exemplo, definir essa versão de configuração de TLS mínima como TLS 1,0 significa que o servidor permitirá conexões de clientes usando TLS 1,0, 1,1 e 1.2 +. Como alternativa, definir isso como 1,2 significa que você só permite conexões de clientes que usam TLS 1,2 e todas as conexões com TLS 1,0 e TLS 1,1 serão rejeitadas.

> [!Note] 
> O banco de dados do Azure para MariaDB assume como padrão o TLS que está sendo desabilitado para todos os novos servidores.
>
> Atualmente, as versões do TLS com suporte para o banco de dados pelo para MariaDB são TLS 1,0, 1,1 e 1,2.

Para saber como definir a configuração de TLS para o banco de dados do Azure para MariaDB, consulte [como definir a configuração de TLS](howto-tls-configurations.md).

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre [regras de firewall de servidor](concepts-firewall-rules.md)
- Saiba como [configurar o SSL](howto-configure-ssl.md).
- Saiba como [Configurar o TLS](howto-tls-configurations.md).