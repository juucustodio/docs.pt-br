---
description: 'Saiba mais sobre: TcpTransportBindingElement'
title: TcpTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 33bbc1e5-44e4-4ee3-b7b5-801dc78956e4
ms.openlocfilehash: b52bb2eb4b40648808459f76e068a6f72f9476a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715139"
---
# <a name="tcptransportbindingelement"></a>TcpTransportBindingElement

TcpTransportBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class TcpTransportBindingElement : ConnectionOrientedTransportBindingElement  
{  
  TcpConnectionPoolSettings ConnectionPoolSettings;  
  sint32 ListenBacklog;  
  boolean PortSharingEnabled;  
  boolean TeredoEnabled;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe TcpTransportBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe TcpTransportBindingElement tem as seguintes propriedades:  
  
### <a name="connectionpoolsettings"></a>ConnectionPoolSettings  

 Tipo de dados: TcpConnectionPoolSettings  
  
 Tipo de acesso: Somente leitura  
  
 As configurações do pool de conexões.  
  
### <a name="listenbacklog"></a>ListenBacklog  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de solicitações de conexão em fila que podem estar pendentes.  
  
### <a name="portsharingenabled"></a>PortSharingEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se o compartilhamento de porta TCP está habilitado para esta conexão.  
  
### <a name="teredoenabled"></a>TeredoEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se Teredo (uma tecnologia para endereçar clientes que estão atrás de firewalls) está habilitado.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
