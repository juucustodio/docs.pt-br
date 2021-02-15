---
description: 'Saiba mais sobre o método: ICorDebugType:: GetFirstTypeParameter'
title: Método ICorDebugType::GetFirstTypeParameter
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetFirstTypeParameter
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetFirstTypeParameter
helpviewer_keywords:
- ICorDebugType::GetFirstTypeParameter method [.NET Framework debugging]
- GetFirstTypeParameter method [.NET Framework debugging]
ms.assetid: 35bb594f-af6a-4349-83fe-e98702674e03
topic_type:
- apiref
ms.openlocfilehash: 4c37217f34f80c916d618d88e4917eab794a1d90
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658263"
---
# <a name="icordebugtypegetfirsttypeparameter-method"></a>Método ICorDebugType::GetFirstTypeParameter

Obtém um ponteiro de interface para um ICorDebugType que representa o primeiro <xref:System.Type> parâmetro do tipo representado por isso `ICorDebugType` .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFirstTypeParameter (  
    [out] ICorDebugType   **value  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `value`  
 fora Um ponteiro para o endereço de um `ICorDebugType` objeto que representa o primeiro parâmetro.  
  
## <a name="remarks"></a>Comentários  

 `GetFirstTypeParameter` pode ser chamado em casos em que as informações adicionais sobre o tipo envolvam, no máximo, um parâmetro de tipo. Em particular, ele pode ser usado se o tipo for um ELEMENT_TYPE_ARRAY, ELEMENT_TYPE_SZARRAY, ELEMENT_TYPE_BYREF ou ELEMENT_TYPE_PTR, conforme indicado pelo método [ICorDebugType:: GetType](icordebugtype-gettype-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
