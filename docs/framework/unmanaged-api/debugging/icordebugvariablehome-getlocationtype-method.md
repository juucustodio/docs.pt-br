---
description: 'Saiba mais sobre o método: ICorDebugVariableHome:: getlocationtype'
title: 'Método ICorDebugVariableHome:: getlocationtype'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetLocationType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetLocationType
helpviewer_keywords:
- ICorDebugVariableHome::GetLocationType method [.NET Framework debugging]
- GetLocationType method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: 88027c55-8ec6-4f1e-a55b-7eefdbbc3515
topic_type:
- apiref
ms.openlocfilehash: 6efe9c045641d162be820961ca75c21a2b8fc14b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728789"
---
# <a name="icordebugvariablehomegetlocationtype-method"></a>Método ICorDebugVariableHome:: getlocationtype

Obtém o tipo do local nativo da variável.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocationType(  
    [out] VariableLocationType *pLocationType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pLocationType`  
 fora Um ponteiro para o tipo do local nativo da variável.  Consulte a enumeração [VariableLocationType](variablelocationtype-enumeration.md) para obter mais informações.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugVariableHome](icordebugvariablehome-interface.md)
- [Enumeração VariableLocationType](variablelocationtype-enumeration.md)
