---
description: 'Saiba mais sobre: como usar o provedor de função do Gerenciador de autorização ASP.NET com um serviço'
title: 'Como: usar o provedor de função do gerenciador de autorização ASP.NET com um serviço'
ms.date: 03/30/2017
ms.assetid: f21deb81-91ef-49ef-94d6-494785143271
ms.openlocfilehash: 24d6bbbf2181189104fb0df0068130c402fd2f68
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734120"
---
# <a name="how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service"></a>Como: usar o provedor de função do gerenciador de autorização ASP.NET com um serviço

Quando o ASP.NET hospeda um serviço Web, você pode integrar o Gerenciador de autorização ao aplicativo para fornecer autorização ao serviço. O Gerenciador de autorização permite que um desenvolvedor de aplicativo defina operações individuais, que podem ser agrupadas para tarefas de formulário. Um administrador pode então autorizar funções para executar tarefas específicas ou operações individuais. O Gerenciador de autorização fornece uma ferramenta de administração como um snap-in do MMC (console de gerenciamento Microsoft) para gerenciar funções, tarefas, operações e usuários. Os administradores configuram um repositório de políticas do Gerenciador de autorização em um arquivo XML, Active Directory ou em um repositório do ADAM (Active Directory Application Mode).  
  
 O Gerenciador de autorização é integrado ao aplicativo Configurando o provedor de função ASP.NET do Gerenciador de autorização para o aplicativo ASP.NET que está hospedando o serviço Web. Assim como outros provedores de função ASP.NET, o provedor de função ASP.NET do Gerenciador de autorização é configurado usando o `providers` elemento <>.  
  
 O exemplo de código a seguir é uma parte de um arquivo de configuração para um serviço Web que está integrando o Gerenciador de autorização no aplicativo.  
  
```xml  
<system.web>  
    <roleManager enabled="true" defaultProvider="AzManRoleProvider">  
      <providers>  
        <add name="AzManRoleProvider"  
             type="System.Web.Security.AuthorizationStoreRoleProvider, System.Web, Version=2.0.0.0, Culture=neutral, publicKeyToken=b03f5f7f11d50a3a"  
             connectionStringName="AzManPolicyStoreConnectionString"
             applicationName="SecureService"/>  
      </providers>  
    </roleManager>  
</system.web>  
```  
  
 Para obter mais informações sobre como integrar um provedor de função ASP.NET a um aplicativo WCF, consulte [como: usar o provedor de função ASP.NET com um serviço](how-to-use-the-aspnet-role-provider-with-a-service.md). Para obter mais informações sobre como usar o Gerenciador de autorização com ASP.NET, consulte [como: usar o Gerenciador de autorização (AzMan) com o ASP.NET 2,0](/previous-versions/msp-n-p/ff649313(v=pandp.10)).  
  
## <a name="see-also"></a>Consulte também

- [Como: usar o provedor de função do ASP.NET com um serviço](how-to-use-the-aspnet-role-provider-with-a-service.md)
