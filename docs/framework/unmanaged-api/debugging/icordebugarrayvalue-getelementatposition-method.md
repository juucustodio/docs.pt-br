---
description: 'Saiba mais sobre o método: ICorDebugArrayValue:: GetElementAtPosition'
title: Método ICorDebugArrayValue::GetElementAtPosition
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetElementAtPosition
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetElementAtPosition
helpviewer_keywords:
- GetElementAtPosition method [.NET Framework debugging]
- ICorDebugArrayValue::GetElementAtPosition method [.NET Framework debugging]
ms.assetid: 6fd5eaa4-1997-4910-82f5-3887480db764
topic_type:
- apiref
ms.openlocfilehash: ef8e4a39f5fe4088b1883803aee037c51f410241
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723019"
---
# <a name="icordebugarrayvaluegetelementatposition-method"></a>Método ICorDebugArrayValue::GetElementAtPosition

Obtém o elemento na posição fornecida, tratando a matriz como uma matriz unidimensional com base em zero.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetElementAtPosition (  
    [in]  ULONG32          nPosition,  
    [out] ICorDebugValue   **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `nPosition`  
 no A posição do elemento a ser recuperado.  
  
 `ppValue`  
 fora Um ponteiro para o endereço de um objeto ICorDebugValue que representa o valor do elemento.  
  
## <a name="remarks"></a>Comentários  

 O layout de uma matriz de várias dimensões segue o estilo C++ de layout de matriz.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
