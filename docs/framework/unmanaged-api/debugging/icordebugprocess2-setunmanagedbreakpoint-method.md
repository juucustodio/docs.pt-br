---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: SetUnmanagedBreakpoint'
title: Método ICorDebugProcess2::SetUnmanagedBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetUnmanagedBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint
helpviewer_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint method [.NET Framework debugging]
- SetUnmanagedBreakpoint method [.NET Framework debugging]
ms.assetid: 93829d15-d942-4e2d-b7a4-dfc9d7fb96be
topic_type:
- apiref
ms.openlocfilehash: 7989f0fc9908941513b7d099fde81c79cef82c5b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746536"
---
# <a name="icordebugprocess2setunmanagedbreakpoint-method"></a>Método ICorDebugProcess2::SetUnmanagedBreakpoint

Define um ponto de interrupção não gerenciado no deslocamento da imagem nativa especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetUnmanagedBreakpoint (  
    [in]  CORDB_ADDRESS    address,  
    [in]  ULONG32          bufsize,  
    [out, size_is(bufsize), length_is(*bufLen)]
        BYTE               buffer[],  
    [out] ULONG32          *bufLen  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no Um `CORDB_ADDRESS` objeto que especifica o deslocamento da imagem nativa.  
  
 `bufsize`  
 no O tamanho, em bytes, da `buffer` matriz.  
  
 `buffer`  
 fora Uma matriz que contém o opcode que é substituído pelo ponto de interrupção.  
  
 `bufLen`  
 fora Um ponteiro para o número de bytes retornados na `buffer` matriz.  
  
## <a name="remarks"></a>Comentários  

 Se o deslocamento da imagem nativa estiver dentro do Common Language Runtime (CLR), o ponto de interrupção será ignorado. Isso permite que o CLR Evite distribuir um ponto de interrupção fora de banda, quando o ponto de interrupção é definido pelo depurador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
