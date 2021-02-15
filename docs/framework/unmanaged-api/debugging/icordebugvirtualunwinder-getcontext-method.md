---
description: 'Saiba mais sobre o método: ICorDebugVirtualUnwinder:: GetContext'
title: 'Método ICorDebugVirtualUnwinder:: GetContext'
ms.date: 03/30/2017
ms.assetid: fe502a76-3068-47e5-a0a0-85ccb72dfac3
ms.openlocfilehash: 864f32ce82149658b2d4a617b08e8d7aa41fe642
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790523"
---
# <a name="icordebugvirtualunwindergetcontext-method"></a>Método ICorDebugVirtualUnwinder:: GetContext

Obtém o contexto atual deste desenrolador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetContext(  
   [in] ULONG32 contextFlags,  
   [in] ULONG32 cbContextBuf,  
   [out] ULONG32* contextSize,  
   [out, size_is(cbContextBuf)] BYTE contextBuf[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `contextFlags`  
 no Sinalizadores que especificam quais partes do contexto retornar (definido em WinNT. h).  
  
 `cbContextBuf`  
 no O número de bytes em `contextBuf` .  
  
 `contextSize`  
 fora Um ponteiro para o número de bytes realmente gravados no `contextBuf` .  
  
 `contextBuf`  
 fora Uma matriz de bytes que contém o contexto atual deste desenrolador.  
  
## <a name="return-value"></a>Valor retornado  

 Qualquer valor HRESULT com falha recebido por MSCorDbi é considerado fatal e fará com que as APIs do ICorDebug sejam retornadas `CORDBG_E_DATA_TARGET_ERROR` .  
  
## <a name="remarks"></a>Comentários  

 Você define o valor inicial do `contextBuf` argumento para o buffer de contexto retornado chamando o método [ICorDebugStackWalk:: GetContext](icordebugstackwalk-getcontext-method.md) .  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
 Como o desenrolamento só pode restaurar um subconjunto dos registros, como somente os registros não voláteis, o contexto pode não corresponder exatamente ao estado de registro no momento da chamada de método real.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMemoryBuffer](icordebugmemorybuffer-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
