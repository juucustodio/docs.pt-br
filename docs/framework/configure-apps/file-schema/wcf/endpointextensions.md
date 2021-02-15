---
description: 'Saiba mais sobre: <endpointExtensions>'
title: <endpointExtensions>
ms.date: 03/30/2017
ms.assetid: 33396e0a-1fae-4616-b822-923584eebfd1
ms.openlocfilehash: d9684ccfab868b1b0d5fe9e054a3a97912712324
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664750"
---
# \<endpointExtensions>

Esta seção registra um novo ponto de extremidade padrão na seção extensões em um computador ou arquivo de configuração de aplicativo. Você pode adicionar um ponto de extremidade padrão a essa coleção usando a `add` palavra-chave e definindo o `type` atributo do elemento como o tipo de ponto de extremidade, bem como o `name` atributo para o nome do ponto de extremidade padrão.  
  
 O exemplo a seguir usa o `add` elemento, bem como o `name` atributo para adicionar um ponto de extremidade padrão à `<endpointExtensions>` seção do arquivo de configuração.  
  
```xml  
<system.serviceModel>
  <extensions>
    <endpointExtensions>
      <add name="udpDiscoveryEndpoint"
           type="System.Discovery.UdpEndpointCollectionElement, System.Discovery.dll, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
 Depois que o ponto de extremidade padrão tiver sido registrado, você poderá usá-lo conforme mostrado no exemplo a seguir. No [\<endpoint>](endpoint-element.md) elemento, o `kind` atributo especifica o tipo de ponto de extremidade padrão que foi registrado na `<endpointExtensions>` seção. O `endpointConfiguration` atributo será idêntico ao `name` atributo do elemento de configuração do ponto de extremidade padrão na `<standardEndpoints>` seção.  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Service1">
      <endpoint kind="udpDiscoveryEndpoint"
                endpointConfiguration="udpConfig" />
    </service>
  </services>
  <standardEndpoints>
    <udpDiscoveryEndpoint>
      <standardEndpoint name="udpConfig"
                        multicastAddress="soap.udp://239.255.255.250:3703"
                        ... />
    </udpDiscoveryEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
