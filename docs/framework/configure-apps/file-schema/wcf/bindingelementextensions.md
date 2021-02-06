---
description: 'Saiba mais sobre: <bindingElementExtensions>'
title: <bindingElementExtensions>
ms.date: 03/30/2017
ms.assetid: bb597fc0-c947-451c-afda-bf23d42f4f4d
ms.openlocfilehash: 4c1b4b924906b1a6dc143588a057129ca5ce8f40
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99639413"
---
# \<bindingElementExtensions>

Esta seção habilita o uso de um elemento de associação personalizado de um computador ou arquivo de configuração de aplicativo. Você pode adicionar um elemento de associação personalizado a essa coleção usando a `add` palavra-chave e definindo o `type` atributo do elemento como uma extensão de elemento de associação, bem como o `name` atributo para o elemento de associação personalizado.  
  
 As extensões de associação permitem que o usuário crie elementos de associação definidos pelo usuário para uso como parte de associações personalizadas. Programaticamente, uma extensão de associação é um tipo que implementa a classe abstrata <xref:System.ServiceModel.Channels.BindingElement> . No arquivo de configuração, a `bindingElementExtensions` seção é usada para definir um elemento de extensão.  
  
 O exemplo a seguir usa o `add` elemento, bem como o `name` atributo para adicionar uma extensão de associação à `bindingElementExtensions` seção do arquivo de configuração.  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingElementExtensions>
      <add name="udpTransport"
           type="Microsoft.ServiceModel.Samples.UdpTransportSection, UdpTransport,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </bindingElementExtensions>
  </extensions>
</system.serviceModel>
```  
  
 Para adicionar habilidades de configuração ao elemento, o usuário precisa escrever e registrar um `bindingElementExtensionSection` elemento. Para obter mais informações sobre isso, consulte a <xref:System.Configuration> documentação.  
  
 Depois que o elemento e seu tipo de configuração são definidos, a extensão pode ser usada como parte de uma associação personalizada, conforme mostrado no exemplo a seguir.  
  
```xml  
<customBinding>
  <binding name="test2">
    <udpTransport />
    <binaryMessageEncoding maxReadPoolSize="211"
                           maxWritePoolSize="2132"
                           maxSessionSize="3141" />
  </binding>
</customBinding>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>
- [Estendendo associações](../../../wcf/extending/extending-bindings.md)
