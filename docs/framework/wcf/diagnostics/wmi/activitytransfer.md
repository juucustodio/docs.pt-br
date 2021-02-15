---
description: 'Saiba mais sobre: ActivityTransfer'
title: ActivityTransfer
ms.date: 03/30/2017
ms.assetid: fc40ef17-2a92-4ce2-853c-6ba8e5d571f3
ms.openlocfilehash: 28f7d1c0d1056327313e7aa6be293eb325d8f265
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99758002"
---
# <a name="activitytransfer"></a>ActivityTransfer

Evento de transferência de atividade  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ActivityTransfer : WSAT_TraceEvent  
{  
  object ActivityID;  
  object RelatedActivityID;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ActivityTransfer não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ActivityTransfer tem as seguintes propriedades:  
  
### <a name="activityid"></a>ActivityID  
  
- Tipo de dados: objeto  
    Tipo de acesso: Somente leitura  
  
- ID da atividade  
  
### <a name="relatedactivityid"></a>RelatedActivityID  
  
- Tipo de dados: objeto  
    Tipo de acesso: Somente leitura  
  
- ID da atividade relacionada  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel.|
