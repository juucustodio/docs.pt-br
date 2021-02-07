---
description: 'Saiba mais sobre: segurança de integração CLR no SQL Server'
title: Segurança da integração CLR no SQL Server
ms.date: 03/30/2017
ms.assetid: 489fe096-fd1d-42de-8438-bf7aed46aea2
ms.openlocfilehash: 5de552c0f5b869712d2038b53abd50b8ded04747
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718532"
---
# <a name="clr-integration-security-in-sql-server"></a>Segurança da integração CLR no SQL Server

Microsoft SQL Server fornece a integração do componente Common Language Runtime (CLR) do .NET Framework. A integração CLR permite que você escreva procedimentos armazenados, gatilhos, tipos definidos pelo usuário, funções definidas pelo usuário, agregações definidas pelo usuário e funções com valor de tabela de streaming, usando qualquer linguagem de .NET Framework, como o Microsoft Visual Basic .NET ou o Microsoft Visual C#.  
  
 O CLR dá suporte a um modelo de segurança chamado CAS (segurança de acesso do código) para código gerenciado. Nesse modelo, as permissões são concedidas a assemblies com base nas evidências fornecidas pelo código nos metadados. SQL Server integra o modelo de segurança baseado no usuário do SQL Server com o modelo de segurança baseado em acesso ao código do CLR.  
  
## <a name="external-resources"></a>Recursos externos  

 Para obter mais informações sobre a integração CLR com o SQL Server, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Segurança de acesso do código](../../../misc/code-access-security.md)|Contém tópicos que descrevem CAS no .NET Framework.|  
|[Segurança da integração CLR](/sql/relational-databases/clr-integration/security/clr-integration-security)|Discute o modelo de segurança para execução de código gerenciado dentro de SQL Server.|  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)
- [Integração do Common Language Runtime do SQL](sql-server-common-language-runtime-integration.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
