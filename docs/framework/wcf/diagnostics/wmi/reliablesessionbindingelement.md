---
description: 'Saiba mais sobre: ReliableSessionBindingElement'
title: ReliableSessionBindingElement
ms.date: 03/30/2017
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
ms.openlocfilehash: 582fd62a8751a31c2834b7d81219a237c9887236
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743857"
---
# <a name="reliablesessionbindingelement"></a>ReliableSessionBindingElement

ReliableSessionBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ReliableSessionBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ReliableSessionBindingElement tem as seguintes propriedades:  
  
### <a name="acknowledgementinterval"></a>AcknowledgementInterval  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo que um destino aguarda antes de enviar uma confirmação para a origem da mensagem em canais confiáveis que são criados pela fábrica.  
  
### <a name="flowcontrolenabled"></a>FlowControlEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se o controle de fluxo está habilitado.  
  
### <a name="inactivitytimeout"></a>InactivityTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Especifica a duração máxima que o canal irá permitir que a outra parte de comunicação não envie nenhuma mensagem antes de falhar o canal.  
  
### <a name="maxpendingchannels"></a>MaxPendingChannels  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de canais que podem aguardar para serem aceitos no ouvinte.  
  
### <a name="maxretrycount"></a>MaxRetryCount  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de vezes que um canal confiável tenta retransmitir uma mensagem para a qual não recebeu uma confirmação, chamando `Send` em seu canal subjacente.  
  
### <a name="maxtransferwindowsize"></a>MaxTransferWindowSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O tamanho máximo da janela de transferência para a sessão confiável.  
  
### <a name="ordered"></a>Encomendado  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se as mensagens são garantidas de chegar na ordem em que foram enviadas.  
  
### <a name="reliablemessagingversion"></a>ReliableMessagingVersion  

 Tipo de dados: inteiro  
  
 Tipo de acesso: Somente leitura  
  
 Um inteiro que especifica a versão do protocolo WS-ReliableMessaging usada na sessão confiável.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>
