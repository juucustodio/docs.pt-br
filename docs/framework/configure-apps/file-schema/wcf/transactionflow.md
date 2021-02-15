---
description: 'Saiba mais sobre: <transactionFlow>'
title: <transactionFlow>
ms.date: 03/30/2017
ms.assetid: 8c7b4c5b-ace3-4fe3-89ff-7b13c9aacd13
ms.openlocfilehash: 8a853beaec1837606ecb96156b8ec9381fa3e07a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773544"
---
# \<transactionFlow>

Especifica o suporte do fluxo de transações para a associação personalizada.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<transactionFlow>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<transactionFlow transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004" />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|transactionProtocol|Especifica o protocolo de transação a ser usado. Os valores válidos incluem os seguintes:<br /><br /> -OleTransactions<br />- WSAtomicTransactionOctober2004<br /><br /> O padrão é OleTransactions.<br /><br /> Esse atributo é do tipo <xref:System.ServiceModel.TransactionProtocol> .|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|Define todos os recursos de associação da associação personalizada.|  
  
## <a name="remarks"></a>Comentários  

 Esse elemento permite habilitar ou desabilitar o fluxo de transações de entrada nas configurações de associação de um ponto de extremidade, bem como especificar o formato de protocolo desejado para as transações de entrada. Para obter mais informações sobre como usar esse elemento de configuração, consulte [configuração de transação ServiceModel](../../../wcf/feature-details/servicemodel-transaction-configuration.md) e [habilitação do fluxo de transações](../../../wcf/feature-details/enabling-transaction-flow.md).  
  
> [!CAUTION]
> Ao usar o `OleTransactions` protocolo para transmitir transações do ponto de extremidade para o ponto de extremidade, o tempo limite da transação poderá ser perdido se o ponto de extremidade de destino tentar fluir novamente usando qualquer protocolo diferente de `OleTransactions` . Isso pode causar todos os nós de nível inferior após o salto de OleTransactions para o tempo limite mais tarde do esperado.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.TransactionFlowElement>
- <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Configuração de transação de ServiceModel](../../../wcf/feature-details/servicemodel-transaction-configuration.md)
- [Ativando o fluxo de transações](../../../wcf/feature-details/enabling-transaction-flow.md)
- [Associações](../../../wcf/bindings.md)
- [Estendendo associações](../../../wcf/extending/extending-bindings.md)
- [Associações personalizadas](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
