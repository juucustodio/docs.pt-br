---
description: 'Saiba mais sobre o método: ICorDebugCode:: GetILToNativeMapping'
title: Método ICorDebugCode::GetILToNativeMapping
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetILToNativeMapping
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetILToNativeMapping method [.NET Framework debugging]
ms.assetid: a8ecd8c8-9627-4356-9c6f-bd05e24637c0
topic_type:
- apiref
ms.openlocfilehash: 808ed450fced8afecc2b637a3b990a894897b350
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711187"
---
# <a name="icordebugcodegetiltonativemapping-method"></a>Método ICorDebugCode::GetILToNativeMapping

Obtém uma matriz de instâncias "COR_DEBUG_IL_TO_NATIVE_MAP" que representam mapeamentos de deslocamentos de MSIL (Microsoft Intermediate Language) para deslocamentos nativos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetILToNativeMapping (  
    [in]  ULONG32    cMap,  
    [out] ULONG32    *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cMap`  
 no O tamanho da `map` matriz.  
  
 `pcMap`  
 fora Um ponteiro para o número real de elementos retornados na `map` matriz.  
  
 `map`  
 fora Uma matriz de `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas, cada uma representando um mapeamento de um deslocamento de MSIL para um deslocamento nativo.  
  
 Não há nenhuma ordem para a matriz de elementos retornada.  
  
## <a name="remarks"></a>Comentários  

 O `GetILToNativeMapping` método retornará resultados significativos somente se essa instância "ICorDebugCode" representar o código nativo que era JIT (just-in-time) compilado do código MSIL.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugCode](icordebugcode-interface1.md)
