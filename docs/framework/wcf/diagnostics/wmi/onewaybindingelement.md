---
description: 'Saiba mais sobre: OneWayBindingElement'
title: OneWayBindingElement
ms.date: 03/30/2017
ms.assetid: 5c7e17c3-39b9-4214-ae08-9e6141734305
ms.openlocfilehash: 9c2ccc301bd854c7b85fcc53551ed6def329a8fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803081"
---
# <a name="onewaybindingelement"></a>OneWayBindingElement

OneWayBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class OneWayBindingElement : BindingElement  
{  
  ChannelPoolSettings ChannelPoolSettings;  
  sint32 MaxAcceptedChannels;  
  boolean PacketRoutable;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe OneWayBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe OneWayBindingElement tem as seguintes propriedades:  
  
### <a name="channelpoolsettings"></a>ChannelPoolSettings  

 Tipo de dados: ChannelPoolSettings  
  
 Tipo de acesso: Somente leitura  
  
 As configurações do pool de canais.  
  
### <a name="maxacceptedchannels"></a>MaxAcceptedChannels  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de canais aceitos.  
  
### <a name="packetroutable"></a>PacketRoutable  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se o pacote é roteável.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.OneWayBindingElement>
