---
description: 'Saiba mais sobre: comparando transações em COM+ e ServiceModel'
title: Comparando transações em COM+ e ServiceModel
ms.date: 03/30/2017
ms.assetid: e493bcdd-b91a-4486-853f-83dbcd1931b7
ms.openlocfilehash: 9b4e8e0940297e887ec9a3085ebe521afe4d000d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743415"
---
# <a name="comparing-transactions-in-com-and-servicemodel"></a>Comparando transações em COM+ e ServiceModel

Este tópico discute como simular o comportamento de um serviço COM+ transacional usando os atributos de Windows Communication Foundation (WCF) que o <xref:System.ServiceModel> namespace fornece.  
  
## <a name="emulating-com-using-servicemodel-attributes"></a>Emulando COM+ usando atributos de ServiceModel  

 A tabela a seguir compara a <xref:System.EnterpriseServices.TransactionOption> enumeração usada para criar uma `EnterpriseServices` transação e como elas se correlacionam aos atributos do WCF que o <xref:System.ServiceModel> namespace fornece.  
  
|Atributo COM+|Atributos do WCF|  
|---------------------|------------------------------------------------------------------------|  
|RequiresNew|<xref:System.ServiceModel.TransactionFlowAttribute> é definido como <xref:System.ServiceModel.TransactionFlowOption.NotAllowed>.<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> é `true`.<br /><br /> O `TransactionFlow` atributo no elemento de associação é `false` .|  
|Obrigatório|<xref:System.ServiceModel.TransactionFlowAttribute> é definido como <xref:System.ServiceModel.TransactionFlowOption.Allowed>.<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> é `true`.<br /><br /> O `TransactionFlow` atributo no elemento de associação é `true` .|  
|Com suporte|Não há equivalente direto. Em geral, você deve adotar o comportamento especificado para `Required` , em vez disso.|  
|NotSupported|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> é `false`.<br /><br /> O `TransactionFlow` atributo no elemento de associação é `false` .|  
|Desabilitado|Não há equivalente direto. Em geral, você deve adotar o comportamento especificado para `NotSupported` , em vez disso.|
