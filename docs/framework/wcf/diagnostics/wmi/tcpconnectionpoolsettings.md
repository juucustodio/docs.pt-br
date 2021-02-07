---
description: 'Saiba mais sobre: TcpConnectionPoolSettings'
title: TcpConnectionPoolSettings
ms.date: 03/30/2017
ms.assetid: 19acfba3-c057-4dbc-bac7-8674d7844d83
ms.openlocfilehash: 927fcba7f94bcbfa80e06479e79bf20986a661e3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715191"
---
# <a name="tcpconnectionpoolsettings"></a>TcpConnectionPoolSettings

TcpConnectionPoolSettings  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class TcpConnectionPoolSettings  
{  
  string GroupName;  
  datetime IdleTimeout;  
  datetime LeaseTimeout;  
  sint32 MaxOutboundConnectionsPerEndpoint;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe TcpConnectionPoolSettings não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe TcpConnectionPoolSettings tem as seguintes propriedades:  
  
### <a name="groupname"></a>GroupName  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome do grupo do pool de conexão usado pelo elemento de associação.  
  
### <a name="idletimeout"></a>IdleTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O tempo máximo que a conexão pode ficar ociosa antes de ser desconectada.  
  
### <a name="leasetimeout"></a>LeaseTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O tempo máximo para que a operação de concessão seja concluída antes de atingir o tempo limite.  
  
### <a name="maxoutboundconnectionsperendpoint"></a>MaxOutboundConnectionsPerEndpoint  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de conexões de saída para cada ponto de extremidade.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings>
