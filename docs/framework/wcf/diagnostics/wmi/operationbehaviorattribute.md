---
description: 'Saiba mais sobre: OperationBehaviorAttribute'
title: OperationBehaviorAttribute
ms.date: 03/30/2017
ms.assetid: 8c9b0755-9e83-411f-bdcb-61a586022797
ms.openlocfilehash: c1f1b80134163ee65d5015e52017f5bb455aeac7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803055"
---
# <a name="operationbehaviorattribute"></a>OperationBehaviorAttribute

OperationBehaviorAttribute  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class OperationBehaviorAttribute : Behavior  
{  
  boolean AutoDisposeParameters;  
  string Impersonation;  
  string ReleaseInstanceMode;  
  boolean TransactionAutoComplete;  
  boolean TransactionScopeRequired;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe OperationBehaviorAttribute não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe OperationBehaviorAttribute tem as seguintes propriedades:  
  
### <a name="autodisposeparameters"></a>AutoDisposeParameters  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 O estado do recurso de disposição automática para parâmetros.  
  
### <a name="impersonation"></a>Representação  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Indica o nível de representação do chamador ao qual a operação dá suporte.  
  
### <a name="releaseinstancemode"></a>ReleaseInstanceMode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Indica quando no decorrer de uma invocação de operação para reciclar o objeto.  
  
### <a name="transactionautocomplete"></a>TransactionAutoComplete  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se a transação atual deve ser confirmada automaticamente se não ocorrer nenhuma exceção não tratada.  
  
### <a name="transactionscoperequired"></a>TransactionScopeRequired  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se a operação requer uma transação.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.OperationBehaviorAttribute>
