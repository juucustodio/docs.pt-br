---
description: 'Saiba mais sobre: aplicativos cliente seguros'
title: Aplicativos cliente seguros
ms.date: 03/30/2017
ms.assetid: 6239592e-fa7d-4dea-9f00-d296d0048b01
ms.openlocfilehash: a40a6444c2e317b03f03688ca46de157ded6f0ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718948"
---
# <a name="secure-client-applications"></a>Aplicativos cliente seguros

Normalmente, os aplicativos consistem em muitas partes que devem ser protegidas contra vulnerabilidades que podem resultar em perda de dados ou comprometer o sistema. A criação de interfaces de usuário seguras pode evitar muitos problemas bloqueando os invasores antes que eles possam acessar dados ou recursos do sistema.  
  
## <a name="validate-user-input"></a>Validar entrada do usuário  

 Ao construir um aplicativo que acesse dados, você deve pressupor que toda a entrada do usuário seja mal-intencionada até comprovada caso contrário. Não fazer isso pode deixar seu aplicativo vulnerável a ataques. O .NET Framework contém classes para ajudá-lo a impor um domínio de valores para controles de entrada, como limitar o número de caracteres que podem ser inseridos. Os ganchos de evento permitem que você escreva procedimentos para verificar a validade dos valores. Os dados de entrada do usuário podem ser validados e fortemente tipados, limitando a exposição de um aplicativo a explorações de script e de injeção de SQL.  
  
> [!IMPORTANT]
> Você também deve validar a entrada do usuário na fonte de dados, bem como no aplicativo cliente. Um invasor pode optar por burlar seu aplicativo e atacar a fonte de dados diretamente.  
  
 [Segurança e entrada do usuário](../../../standard/security/security-and-user-input.md)  
 Descreve como lidar com bugs sutis e potencialmente perigosos que envolvem a entrada do usuário.  
  
 [Validando entrada do usuário no Páginas da Web do ASP.NET](/previous-versions/aspnet/7kh55542(v=vs.100))  
 Visão geral da validação da entrada do usuário usando controles de validação ASP.NET.  
  
 [Entrada do usuário no Windows Forms](/dotnet/desktop/winforms/user-input-in-windows-forms)  
 Fornece links e informações para validar a entrada do mouse e do teclado em um aplicativo Windows Forms.  
  
 [Expressões regulares do .NET Framework](../../../standard/base-types/regular-expressions.md)  
 Descreve como usar a <xref:System.Text.RegularExpressions.Regex> classe para verificar a validade da entrada do usuário.  
  
## <a name="windows-applications"></a>Aplicativos do Windows  

 No passado, os aplicativos do Windows geralmente eram executados com permissões completas. O .NET Framework fornece a infraestrutura para restringir a execução de código em um aplicativo do Windows usando a CAS (segurança de acesso ao código). No entanto, o CAS sozinho não é suficiente para proteger seu aplicativo.  
  
 [Segurança do Windows Forms](/dotnet/desktop/winforms/windows-forms-security)  
 Discute como proteger Windows Forms aplicativos e fornece links para tópicos relacionados.  
  
 [Windows Forms e aplicativos não gerenciados](/dotnet/desktop/winforms/advanced/windows-forms-and-unmanaged-applications)  
 Descreve como interagir com aplicativos não gerenciados em um aplicativo Windows Forms.  
  
 [Implantação do ClickOnce para o Windows Forms](/dotnet/desktop/winforms/clickonce-deployment-for-windows-forms)  
 Descreve como usar a `ClickOnce` implantação em um aplicativo Windows Forms e discute as implicações de segurança.  
  
## <a name="aspnet-and-xml-web-services"></a>Serviços Web ASP.NET e XML  

 Os aplicativos ASP.NET geralmente precisam restringir o acesso a algumas partes do site e fornecer outros mecanismos de proteção de dados e segurança de site. Esses links fornecem informações úteis para proteger seu aplicativo ASP.NET.  
  
 Um serviço Web XML fornece dados que podem ser consumidos por um aplicativo ASP.NET, um aplicativo Windows Forms ou outro serviço Web. Você precisa gerenciar a segurança para o próprio serviço Web, bem como a segurança para o aplicativo cliente.  
  
 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Protegendo sites da ASP.NET](/previous-versions/aspnet/91f66yxt(v=vs.100))|Discute como proteger aplicativos ASP.NET.|  
|[Protegendo Web Services XML criados usando ASP.NET](/previous-versions/dotnet/netframework-4.0/w67h0dw7(v=vs.100))|Discute como implementar a segurança para um serviço Web ASP.NET.|  
|[Visão geral de scripts maliciosos](/previous-versions/aspnet/w1sw53ds(v=vs.100))|Discute como proteger contra um ataque de exploração de script, que tenta inserir caracteres mal-intencionados em uma página da Web.|  
|[Práticas básicas de segurança para aplicativos Web](/previous-versions/aspnet/zdh19h94(v=vs.100))|Informações gerais de segurança e links para uma discussão adicional,|  
  
## <a name="remoting"></a>Comunicação remota  

 O .NET Remoting permite que você crie aplicativos amplamente distribuídos facilmente, se os componentes do aplicativo estão todos em um computador ou se espalham em todo o mundo. Você pode criar aplicativos cliente que usam objetos em outros processos no mesmo computador ou em qualquer outro computador que possa ser acessado pela rede. Você também pode usar o .NET Remoting para se comunicar com outros domínios de aplicativo no mesmo processo.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Configuração de aplicativos remotos](/previous-versions/dotnet/netframework-4.0/b8tysty8(v=vs.100))|Discute como configurar aplicativos de comunicação remota para evitar problemas comuns.|  
|[Segurança em comunicação remota](/previous-versions/dotnet/netframework-4.0/9hwst9th(v=vs.100))|Descreve a autenticação e a criptografia, bem como tópicos adicionais de segurança relevantes para comunicação remota.|  
|[Considerações sobre segurança e comunicação remota](../../misc/security-and-remoting-considerations.md)|Descreve problemas de segurança com objetos protegidos e cruzamento de domínio de aplicativo.|  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](securing-ado-net-applications.md)
- [Recomendações para estratégias de acesso a dados](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))
- [Protegendo aplicativos](/visualstudio/ide/securing-applications)
- [Protegendo informações de conexão](protecting-connection-information.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
