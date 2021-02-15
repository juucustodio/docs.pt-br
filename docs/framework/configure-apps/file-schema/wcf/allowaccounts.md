---
description: 'Saiba mais sobre: <allowAccounts>'
title: <allowAccounts>
ms.date: 03/30/2017
ms.assetid: 166923a9-a8ac-478f-92f9-529d9667f3a6
ms.openlocfilehash: 5211d694e5318faf0cfc31b404764acb405bd096
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99749981"
---
# \<allowAccounts>

Contém uma coleção de elementos de configuração que especificam contas de usuário para processos que hospedam serviços Windows Communication Foundation (WCF) e recebem acesso de conexão ao serviço de compartilhamento.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel.activation>**](system-servicemodel-activation.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<net.pipe>**](net-pipe.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<allowAccounts>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<allowAccounts>
  <add securityIdentifier="String" />
</allowAccounts>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|[\<add>](add-of-allowaccounts.md)|Adiciona uma conta de usuário para processos que hospedam serviços WCF e recebem acesso de conexão ao serviço de compartilhamento|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<net.pipe>](net-pipe.md) ou [\<net.tcp>](net-tcp.md)|Especifica as definições de configuração para o pipe de rede ou para os serviços de compartilhamento de TCP.|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Activation.Configuration.NetTcpSection.AllowAccounts%2A>
- <xref:System.ServiceModel.Activation.Configuration.NetPipeSection.AllowAccounts%2A>
- <xref:System.ServiceModel.Activation.Configuration.SecurityIdentifierElementCollection>
- <xref:System.ServiceModel.Activation.Configuration.SecurityIdentifierElement>
