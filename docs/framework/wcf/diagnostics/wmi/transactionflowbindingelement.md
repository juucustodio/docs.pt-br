---
description: 'Saiba mais sobre: TransactionFlowBindingElement'
title: TransactionFlowBindingElement
ms.date: 03/30/2017
ms.assetid: 0a9656fe-2400-45ca-ad79-92715c8cf190
ms.openlocfilehash: 6a96a83c563affdaef01a12d64bc1c13ab2f719e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757131"
---
# <a name="transactionflowbindingelement"></a>TransactionFlowBindingElement

TransactionFlowBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class TransactionFlowBindingElement : BindingElement  
{  
  string IssuedTokens;  
  string TransactionProtocol;  
  boolean Transactions;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe TransactionFlowBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe TransactionFlowBindingElement tem as seguintes propriedades:  
  
### <a name="issuedtokens"></a>IssuedTokens  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Especifica o requisito para um cabeçalho de tokens de segurança emitidos (IssuedTokens de WS-Trust).  
  
### <a name="transactionprotocol"></a>TransactionProtocol  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O protocolo de transações usado pelo serviço para o fluxo de transações.  
  
### <a name="transactions"></a>Transactions  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se há suporte para a transação de entrada.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>
