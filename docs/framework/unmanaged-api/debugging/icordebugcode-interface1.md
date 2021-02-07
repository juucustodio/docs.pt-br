---
description: 'Saiba mais sobre: interface ICorDebugCode'
title: Interface ICorDebugCode
ms.date: 03/30/2017
api_name:
- ICorDebugCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode
helpviewer_keywords:
- ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7bd14fb6-8b54-4484-a891-e3c21859c019
topic_type:
- apiref
ms.openlocfilehash: ce67c48501783bbe00152f0ba2c224e6e7dde6d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711135"
---
# <a name="icordebugcode-interface"></a>Interface ICorDebugCode

Representa um segmento de código MSIL (Microsoft Intermediate Language) ou código nativo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateBreakpoint](icordebugcode-createbreakpoint-method.md)|Cria um ponto de interrupção no deslocamento especificado.|  
|[Método GetAddress](icordebugcode-getaddress-method.md)|Obtém o endereço virtual relativo (RVA) do segmento de código que isso `ICorDebugCode` representa.|  
|[Método GetCode](icordebugcode-getcode-method.md)|Obtém todo o código para a função especificada, formatado para desmontagem. Esse método foi preterido; Use [ICorDebugCode2:: GetCodeChunks](icordebugcode2-getcodechunks-method.md) em vez disso.|  
|[Método GetEnCRemapSequencePoints](icordebugcode-getencremapsequencepoints-method.md)|Não implementado.|  
|[Método GetFunction](icordebugcode-getfunction-method.md)|Obtém o "ICorDebugFunction" associado a isso `ICorDebugCode` .|  
|[Método GetILToNativeMapping](icordebugcode-getiltonativemapping-method.md)|Obtém uma matriz de instâncias "COR_DEBUG_IL_TO_NATIVE_MAP" que representam mapeamentos de deslocamentos MSIL para deslocamentos nativos.|  
|[Método GetSize](icordebugcode-getsize-method.md)|Obtém o tamanho, em bytes, do código binário representado por isso `ICorDebugCode` .|  
|[Método GetVersionNumber](icordebugcode-getversionnumber-method.md)|Obtém o número baseado em um que identifica a versão do código que `ICorDebugCode` representa.|  
|[Método IsIL](icordebugcode-isil-method.md)|Obtém um valor que indica se isso `ICorDebugCode` é compilado em MSIL.|  
  
## <a name="remarks"></a>Comentários  

 `ICorDebugCode` pode representar o MSIL ou código nativo. Um objeto "ICorDebugFunction" que representa o código MSIL pode ter zero ou um `ICorDebugCode` objetos associados a ele. Um objeto "ICorDebugFunction" que representa o código nativo pode ter qualquer número de `ICorDebugCode` objetos associados a ele.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugCode3](icordebugcode3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
