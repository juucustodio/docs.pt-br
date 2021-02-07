---
description: 'Saiba mais sobre: serviço'
title: Serviço
ms.date: 03/30/2017
ms.assetid: 999806e1-6376-409e-b998-b0af391adfe7
ms.openlocfilehash: e66f9a23f8c182327899904c26ff6a6368b9bdc6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715620"
---
# <a name="service"></a>Serviço

Serviço  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class Service  
{  
  string BaseAddresses[];  
  Behavior Behaviors[];  
  string ConfigurationName;  
  string CounterInstanceName;  
  string DistinguishedName;  
  string Extensions[];  
  string Metadata[];  
  string Name;  
  string Namespace;  
  datetime Opened;  
  Channel OutgoingChannels[];  
  sint32 ProcessId;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe de serviço não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe de serviço tem as seguintes propriedades:  
  
### <a name="baseaddresses"></a>BaseAddresses  

 Tipo de dados: matriz de cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Os endereços base usados pelo serviço.  
  
### <a name="behaviors"></a>Comportamentos  

 Tipo de dados: matriz de comportamento  
  
 Tipo de acesso: Somente leitura  
  
 Os comportamentos associados a esse serviço.  
  
### <a name="configurationname"></a>ConfigurationName  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 ServiceElement_BehaviorConfiguration  
  
### <a name="counterinstancename"></a>Monoinstancename  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome da instância dos contadores de desempenho do serviço.  
  
### <a name="distinguishedname"></a>DistinguishedName  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Nome do serviço no endereço.  
  
### <a name="extensions"></a>Extensões  

 Tipo de dados: matriz de cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Os contextos de instância para as extensões da instância de serviço.  
  
### <a name="metadata"></a>Metadados  

 Tipo de dados: matriz de cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de metadados de serviço.  
  
### <a name="name"></a>Nome  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome exclusivo deste serviço.  
  
### <a name="namespace"></a>Namespace  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O namespace do serviço.  
  
### <a name="opened"></a>Aberto  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 A hora em que o serviço foi aberto.  
  
### <a name="outgoingchannels"></a>OutgoingChannels  

 Tipo de dados: matriz de canal  
  
 Tipo de acesso: Somente leitura  
  
 Os canais que estão saindo da instância do serviço.  
  
### <a name="processid"></a>ProcessId  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 A ID do processo que hospeda o serviço.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|
