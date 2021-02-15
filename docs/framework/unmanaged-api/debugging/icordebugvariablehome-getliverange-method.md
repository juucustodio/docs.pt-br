---
description: 'Saiba mais sobre o método: IcorDebugVariableHome:: GetLiveRange'
title: 'Método IcorDebugVariableHome:: GetLiveRange'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetLiveRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetLiveRange
helpviewer_keywords:
- ICorDebugVariableHome::GetLiveRange method [.NET Framework debugging]
- GetLiveRange method, ICorDebugVariableFrame interface [.NET Framework debugging]
ms.assetid: 87277e1a-1595-4729-9e25-d1c3ac18ce5f
topic_type:
- apiref
ms.openlocfilehash: daa53a164c7660826d44285ce21ecea1b649a727
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800832"
---
# <a name="icordebugvariablehomegetliverange-method"></a>Método IcorDebugVariableHome:: GetLiveRange

Obtém o intervalo nativo no qual essa variável está ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLiveRange(  
    [out] ULONG32* pStartOffset,  
    [out] ULONG32 *pEndOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pStartOffset`  
 fora O deslocamento lógico no qual a variável é ativada pela primeira vez.  
  
 `pEndOffset`  
 fora O deslocamento lógico imediatamente após o ponto em que a variável é o último Live.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugVariableHome](icordebugvariablehome-interface.md)
