---
description: 'Saiba mais sobre: ICorDebugVirtualUnwinder:: Next Method'
title: 'Método ICorDebugVirtualUnwinder:: Next'
ms.date: 03/30/2017
ms.assetid: 790e0426-e5cd-49fd-a792-f8c8635d72fe
ms.openlocfilehash: b509e8e4fb24c66764999e67ba7e36299ce7f570
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790510"
---
# <a name="icordebugvirtualunwindernext-method"></a>Método ICorDebugVirtualUnwinder:: Next

Avança para o contexto do chamador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next();  
```  
  
## <a name="parameters"></a>Parâmetros  

 Nenhum.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o desenrolar tiver ocorrido com êxito ou `CORDBG_S_AT_END_OF_STACK` se o desenrolamento não puder ser concluído porque não há mais quadros.  
  
 Se um HRESULT com falha for retornado, as APIs do ICorDebug serão retornadas `CORDBG_E_DATA_TARGET_ERROR` .  
  
## <a name="remarks"></a>Comentários  

 O Stack Walker deve garantir que ele faça o andamento do encaminhamento, de modo que, eventualmente, uma chamada para retornará `Next` um HRESULT com falha ou `CORDBG_S_AT_END_OF_STACK` . Retornar `S_OK` indefinidamente pode causar um loop infinito.  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMemoryBuffer](icordebugmemorybuffer-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
