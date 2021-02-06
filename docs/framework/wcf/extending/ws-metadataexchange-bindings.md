---
description: 'Saiba mais sobre: associações de WS-MetadataExchange'
title: WS-MetadataExchange Bindings
ms.date: 03/30/2017
ms.assetid: 10f8de5d-b81d-4ea7-b37e-7f2c00c39714
ms.openlocfilehash: 3bcea573ad436a85285fab5657e58defa9113d9c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643937"
---
# <a name="ws-metadataexchange-bindings"></a>WS-MetadataExchange Bindings

Este tópico descreve como as associações de troca de metadados padrão são construídas para vários transportes.  
  
## <a name="the-default-bindings"></a>As associações padrão  
  
|Nome de associação padrão|Como a associação é construída|  
|--------------------------|------------------------------------|  
|mexHttpBinding|A <xref:System.ServiceModel.WSHttpBinding> com segurança em nível de transporte desabilitada.|  
|mexHttpsBinding|Um <xref:System.ServiceModel.WSHttpBinding> que dá suporte à segurança em nível de transporte.|  
|mexNamedPipeBinding|Um  <xref:System.ServiceModel.Channels.CustomBinding> com um <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement> usando os valores padrão.|  
|mexTcpBinding|Um <xref:System.ServiceModel.Channels.CustomBinding> com um <xref:System.ServiceModel.Channels.TcpTransportBindingElement> usando valores padrão.|
