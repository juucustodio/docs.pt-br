---
description: 'Saiba mais sobre: MsmqBindingElementBase'
title: MsmqBindingElementBase
ms.date: 03/30/2017
ms.assetid: 210d41ab-a2a4-4d7a-afd2-0916c08a4015
ms.openlocfilehash: 3aa5ec2343d73798f1cf5e3c7d4b5a8282f97ac9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803172"
---
# <a name="msmqbindingelementbase"></a>MsmqBindingElementBase

MsmqBindingElementBase  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
class MsmqBindingElementBase : TransportBindingElement  
{  
  string CustomDeadLetterQueue;  
  string DeadLetterQueue;  
  boolean Durable;  
  boolean ExactlyOnce;  
  sint32 MaxRetryCycles;  
  string ReceiveErrorHandling;  
  sint32 ReceiveRetryCount;  
  datetime RetryCycleDelay;  
  datetime TimeToLive;  
  boolean UseMsmqTracing;  
  boolean UseSourceJournal;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe MsmqBindingElementBase não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe MsmqBindingElementBase tem as seguintes propriedades:  
  
### <a name="customdeadletterqueue"></a>CustomDeadLetterQueue  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um URI que contém o local da fila de mensagens mortas para cada aplicativo, onde as mensagens que expiraram ou que têm a transferência ou entrega com falha são colocadas.  
  
### <a name="deadletterqueue"></a>DeadLetterQueue  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um valor de enumeração que indica o tipo de fila de mensagens mortas a ser usado.  
  
### <a name="durable"></a>Durável  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se as mensagens processadas por essa associação são duráveis ou voláteis.  
  
### <a name="exactlyonce"></a>ExactlyOnce  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que indica se as mensagens processadas por essa associação são recebidas exatamente uma vez.  
  
### <a name="maxretrycycles"></a>MaxRetryCycles  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de ciclos de repetição para tentar a entrega de mensagens para o aplicativo de recebimento.  
  
### <a name="receiveerrorhandling"></a>ReceiveErrorHandling  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de manipulação de mensagens suspeitas.  
  
### <a name="receiveretrycount"></a>ReceiveRetryCount  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de tentativas de repetição imediatas em uma mensagem que é lida da fila do aplicativo.  
  
### <a name="retrycycledelay"></a>RetryCycleDelay  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica o tempo de espera entre os ciclos de repetição ao tentar entregar uma mensagem que não pôde ser entregue imediatamente.  
  
### <a name="timetolive"></a>timeToLive  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo que indica por quanto tempo as mensagens processadas por essa associação podem estar na fila antes de expirarem.  
  
### <a name="usemsmqtracing"></a>UseMsmqTracing  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que indica se as mensagens processadas por essa associação devem ser rastreadas.  
  
### <a name="usesourcejournal"></a>UseSourceJournal  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que indica se cópias de mensagens processadas por essa associação devem ser armazenadas na fila do diário de origem.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.NetMsmqBinding>
- <xref:System.ServiceModel.MsmqBindingBase>
