---
description: 'Saiba mais sobre: MsmqTransportBindingElement'
title: MsmqTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 1c89f073-9ed3-4025-a8c5-13535a0f526b
ms.openlocfilehash: 4b6f363d979972c6ff0a2a378906feeece2ff6b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803146"
---
# <a name="msmqtransportbindingelement"></a>MsmqTransportBindingElement

MsmqTransportBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class MsmqTransportBindingElement : MsmqBindingElementBase  
{  
  sint32 MaxPoolSize;  
  string QueueTransferProtocol;  
  boolean UseActiveDirectory;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe MsmqTransportBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe MsmqTransportBindingElement tem as seguintes propriedades:  
  
### <a name="maxpoolsize"></a>MaxPoolSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O tamanho máximo do pool que contém objetos de mensagem MSMQ internos.  
  
### <a name="queuetransferprotocol"></a>QueueTransferProtocol  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um valor de enumeração que indica o transporte de canal de comunicação na fila que essa associação usa.  
  
### <a name="useactivedirectory"></a>UseActiveDirectory  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Retorna um valor booliano que indica se os endereços da fila devem ser convertidos usando o Active Directory.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>
