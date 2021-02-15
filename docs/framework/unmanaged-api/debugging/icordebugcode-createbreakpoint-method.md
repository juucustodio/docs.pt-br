---
description: 'Saiba mais sobre o método: ICorDebugCode:: CreateBreakpoint'
title: Método ICorDebugCode::CreateBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugCode.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::CreateBreakpoint
helpviewer_keywords:
- ICorDebugCode::CreateBreakpoint method [.NET Framework debugging]
- CreateBreakpoint method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 46842618-0fe4-480b-871c-82fba82d23d9
topic_type:
- apiref
ms.openlocfilehash: a9285d59da3e3f34ea303413fca67bc39aff9e32
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711369"
---
# <a name="icordebugcodecreatebreakpoint-method"></a>Método ICorDebugCode::CreateBreakpoint

Cria um ponto de interrupção neste segmento de código no deslocamento especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateBreakpoint (  
    [in] ULONG32     offset,  
    [out] ICorDebugFunctionBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `offset`  
 no O deslocamento no qual criar o ponto de interrupção.  
  
 `ppBreakpoint`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugFunctionBreakpoint" que representa o ponto de interrupção.  
  
## <a name="remarks"></a>Comentários  

 Antes que o ponto de interrupção esteja ativo, ele deve ser adicionado ao objeto de processo.  
  
 Se esse código for um código MSIL (Microsoft Intermediate Language) e houver uma versão nativa compilada JIT (just-in-time) do código, o ponto de interrupção será aplicado também no código compilado por JIT. (O mesmo será verdadeiro se o código for compilado em JIT posteriormente.)  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
