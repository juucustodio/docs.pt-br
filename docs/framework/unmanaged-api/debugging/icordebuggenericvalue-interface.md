---
description: 'Saiba mais sobre: interface ICorDebugGenericValue'
title: Interface ICorDebugGenericValue
ms.date: 03/30/2017
api_name:
- ICorDebugGenericValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGenericValue
helpviewer_keywords:
- ICorDebugGenericValue interface [.NET Framework debugging]
ms.assetid: bc14f408-b359-4c8c-ade2-888ccdf7261b
topic_type:
- apiref
ms.openlocfilehash: 7c81855849d7b72bc509d20072b96bb64f5d395a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692024"
---
# <a name="icordebuggenericvalue-interface"></a>Interface ICorDebugGenericValue

Uma subclasse de "ICorDebugValue" que se aplica a todos os valores. Essa interface fornece métodos Get e Set para o valor.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetValue](icordebuggenericvalue-getvalue-method.md)|Copia o valor no buffer especificado.|  
|[Método SetValue](icordebuggenericvalue-setvalue-method.md)|Copia um novo valor do buffer especificado.|  
  
## <a name="remarks"></a>Comentários  

 `ICorDebugGenericValue` é uma subinterface porque ela não é remota.  
  
 Para tipos de referência, o valor é a referência em vez do conteúdo da referência.  
  
 Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
