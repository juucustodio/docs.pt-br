---
description: 'Saiba mais sobre: classe de canal'
title: Classe de canal
ms.date: 03/30/2017
ms.assetid: d9fae2ca-209c-4341-a0f5-6b79d1a67776
ms.openlocfilehash: dcc92f78f09e9a73a24134c6c0685949f46f38dd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757716"
---
# <a name="channel-class"></a>Classe de canal

Canal  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class Channel  
{  
  string LocalAddress;  
  Endpoint ref;  
  string RemoteAddress;  
  string SessionId;  
  string Type;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe Channel não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe Channel tem as propriedades a seguir.  
  
### <a name="localaddress"></a>LocalAddress  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O ponto de extremidade local para o canal.  
  
### <a name="ref"></a>ref  

 Tipo de dados: ponto de extremidade  
  
 Tipo de acesso: Somente leitura  
  
 Uma referência ao ponto de extremidade ao qual o canal se conecta.  
  
### <a name="remoteaddress"></a>RemoteAddress  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O endereço remoto associado ao canal.  
  
### <a name="sessionid"></a>SessionId  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A ID da sessão atual, se houver.  
  
### <a name="type"></a>Tipo  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O tipo do canal.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.ChannelBase>
