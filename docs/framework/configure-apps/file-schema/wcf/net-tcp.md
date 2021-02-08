---
description: 'Saiba mais sobre: <net. TCP>'
title: <net.tcp>
ms.date: 03/30/2017
ms.assetid: 8bc2f2be-11c1-4bab-9018-1d21ae568d94
ms.openlocfilehash: b7b36e0309139508011e5abceab97cc6f6f9a53d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786935"
---
# \<net.tcp>

Especifica as definições de configuração para a rede. O serviço de compartilhamento de porta TCP, que permite que vários processos compartilhem a mesma porta TCP.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel.activation>**](system-servicemodel-activation.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<net.tcp>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<configuration>
  <system.serviceModel.activation>
    <net.tcp listenBacklog="Integer"
             maxPendingAccepts="Integer"
             maxPendingConnections="Integer"
             receiveTimeout="TimeSpan"
             teredoEnabled="Boolean">
      <allowAccounts>
        <!-- LocalSystem account -->
        <add securityIdentifier="S-1-5-18"/>
        <!-- LocalService account -->
        <add securityIdentifier="S-1-5-19"/>
        <!-- Administrators account -->
        <add securityIdentifier="S-1-5-20"/>
        <!-- Network Service account -->
        <add securityIdentifier="S-1-5-32-544" />
        <!-- IIS_IUSRS account (Vista only)-->
        <add securityIdentifier="S-1-5-32-568"/>
      </allowAccounts>
    </net.tcp>
  </system.serviceModel.activation>
</configuration>
```  
  
## <a name="type"></a>Tipo  

 `Type`  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`listenBacklog`|Um inteiro que especifica o máximo de conexões pendentes que são aceitas da conexão compartilhada, mas que ainda não foram expedidas para serviços de Windows Communication Foundation (WCF). O padrão é 10.|  
|`maxPendingAccepts`|Um inteiro que especifica o máximo de threads de aceitação simultâneas pendentes no ponto de extremidade de escuta para o serviço de compartilhamento. O padrão é 2.|  
|`MaxPendingConnections`|O número máximo de conexões que o ouvinte pode ter aguardando para ser aceito pelo aplicativo. Quando esse valor de cota é excedido, novas conexões de entrada são removidas em vez de aguardar para serem aceitas. Recursos de conexão, como segurança de mensagem, podem fazer com que um cliente Abra mais de uma conexão. Os administradores de serviço devem considerar essas conexões adicionais ao definir esse valor de cota. O padrão é 10.|  
|`receiveTimeout`|Um <xref:System.TimeSpan> que especifica o tempo limite para ler os dados de enquadramento e executar a distribuição de conexão das conexões de sublinhado. O padrão é "00:00:10".|  
|`teredoEnabled`|Um valor booliano que indica se o serviço de compartilhamento de porta usa o serviço Microsoft Teredo para escutar portas TCP em nome dos serviços WCF. O padrão é `false`.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<allowAccounts>](allowaccounts.md)|Uma coleção de elementos de configuração que contêm um `securityIdentifier` atributo para especificar contas de usuário para processos que hospedam serviços WCF e recebem acesso de conexão ao serviço de compartilhamento.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<system.serviceModel.activation>](system-servicemodel-activation.md)|Contém definições de configuração para o processo de ouvinte SMSvcHost.exe.|  
  
## <a name="remarks"></a>Comentários  

 Para obter mais informações sobre compartilhamento de porta, consulte [net. TCP Port Sharing](../../../wcf/feature-details/net-tcp-port-sharing.md). Para entender como configurar o serviço de compartilhamento de porta, consulte [Configurando o serviço de compartilhamento de porta Net. TCP](../../../wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Activation.Configuration.NetTcpSection>
- [Compartilhamento de porta Net.TCP](../../../wcf/feature-details/net-tcp-port-sharing.md)
- [Configurando o serviço de compartilhamento de porta Net.TCP](../../../wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)
