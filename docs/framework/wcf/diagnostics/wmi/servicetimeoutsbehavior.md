---
description: 'Saiba mais sobre: ServiceTimeoutsBehavior'
title: ServiceTimeoutsBehavior
ms.date: 03/30/2017
ms.assetid: 4412525d-a3cc-4eae-b3e8-a50ce766d09d
ms.openlocfilehash: 147d249af0e87bc41da93a4a31355da7053caaf6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715412"
---
# <a name="servicetimeoutsbehavior"></a>ServiceTimeoutsBehavior

ServiceTimeoutsBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceTimeoutsBehavior : Behavior  
{  
  datetime TransactionTimeout;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceTimeoutsBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceTimeoutsBehavior tem a seguinte propriedade:  
  
### <a name="transactiontimeout"></a>TransactionTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O período no qual uma transação deve ser concluída.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Configuration.ServiceTimeoutsElement>
