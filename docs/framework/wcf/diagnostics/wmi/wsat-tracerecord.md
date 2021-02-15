---
description: 'Saiba mais sobre: WSAT_TraceRecord'
title: WSAT_TraceRecord
ms.date: 03/30/2017
ms.assetid: 99bc7f66-1335-40d8-aa68-e754d569dc0d
ms.openlocfilehash: 67202c5d2910783c40b934d2da6108e6b514a728
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756871"
---
# <a name="wsat_tracerecord"></a>WSAT_TraceRecord

WSAT_TraceRecord  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class WSAT_TraceRecord : WSAT_TraceEvent  
{  
  object ActivityID;  
  sint32 EventID;  
  string TraceRecord;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe WSAT_TraceRecord não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe WSAT_TraceRecord tem as seguintes propriedades:  
  
### <a name="activityid"></a>ActivityID  

 Tipo de dados: objeto  
Tipo de acesso: Somente leitura  
  
 A ID da atividade do registro de rastreamento.  
  
### <a name="eventid"></a>EventID  

 Tipo de dados: sint32  
Tipo de acesso: Somente leitura  
  
 A ID de evento do registro de rastreamento.  
  
### <a name="tracerecord"></a>TraceRecord  

 Tipo de dados: cadeia de caracteres  
Tipo de acesso: Somente leitura  
  
 Registro de rastreamento  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|
