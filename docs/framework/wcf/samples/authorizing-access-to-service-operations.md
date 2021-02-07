---
description: 'Saiba mais sobre: autorizar o acesso às operações de serviço'
title: Autorizando o acesso às operações de serviço
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, authorizing access sample
- Authorizing Access To Service Operations Sample [Windows Communication Foundation]
- authorization, Windows Communication Foundation sample
ms.assetid: ddcfdaa5-8b2e-4e13-bd85-887209dc6328
ms.openlocfilehash: 052adc6104b75884c90c266e2e0e7a045032c457
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732690"
---
# <a name="authorizing-access-to-service-operations"></a>Autorizando o acesso às operações de serviço

Este exemplo demonstra como usar o [\<serviceAuthorization>](../../configure-apps/file-schema/wcf/serviceauthorization-element.md) para habilitar o uso do <xref:System.Security.Permissions.PrincipalPermissionAttribute> atributo para autorizar o acesso a operações de serviço. Este exemplo é baseado no exemplo de [introdução](getting-started-sample.md) . O serviço e o cliente são configurados usando o [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) . O `mode` atributo de [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) foi definido como e foi `Message` `clientCredentialType` definido como `Windows` . O <xref:System.Security.Permissions.PrincipalPermissionAttribute> é aplicado a cada método de serviço e usado para restringir o acesso a cada operação. O chamador deve ser um administrador do Windows para acessar cada operação.  
  
 Neste exemplo, o cliente é um aplicativo de console (. exe) e o serviço é hospedado pelo Serviços de Informações da Internet (IIS).  
  
> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.  
  
 O arquivo de configuração de serviço usa o [\<serviceAuthorization>](../../configure-apps/file-schema/wcf/serviceauthorization-element.md) para definir o `principalPermissionMode` atributo:  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior>
      <!-- The serviceAuthorization behavior sets the  
           principalPermissionMode to UseWindowsGroups.  
           This puts a WindowsPrincipal on the current thread when a   
           service is invoked. -->  
      <serviceAuthorization principalPermissionMode="UseWindowsGroups" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Definir o `principalPermissionMode` para `UseWindowsGroups` permite o uso do <xref:System.Security.Permissions.PrincipalPermissionAttribute> com base em nomes de grupo do Windows.  
  
 O <xref:System.Security.Permissions.PrincipalPermissionAttribute> é aplicado a cada operação para exigir que o chamador faça parte do grupo de administradores do Windows, conforme mostrado no código de exemplo a seguir.  
  
```csharp
[PrincipalPermission(SecurityAction.Demand,
                             Role = "Builtin\\Administrators")]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    return result;  
}  
```  
  
 Quando você executa o exemplo, as solicitações de operação e as respostas são exibidas na janela do console do cliente. O cliente se comunicará com êxito com cada operação se estiver sendo executado sob uma conta que faz parte do grupo de administradores; caso contrário, o acesso será negado. Para experimentar a falha de autorização, execute o cliente em uma conta que não faça parte do grupo de administradores. Pressione ENTER na janela do console para desligar o cliente.  
  
 Um serviço pode ser notificado de falhas de autorização implementando um <xref:System.ServiceModel.Dispatcher.IErrorHandler> . Consulte [ampliando o controle sobre tratamento de erros e relatórios](extending-control-over-error-handling-and-reporting.md) para obter informações sobre como implementar o `IErrorHandler` .  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para criar a edição C# ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).  
  
3. Para executar o exemplo em uma configuração de computador único ou entre computadores, siga as instruções em [executando os exemplos de Windows Communication Foundation](running-the-samples.md).  
