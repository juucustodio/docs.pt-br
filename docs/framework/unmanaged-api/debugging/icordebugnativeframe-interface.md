---
description: 'Saiba mais sobre: interface ICorDebugNativeFrame'
title: Interface ICorDebugNativeFrame
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame
helpviewer_keywords:
- ICorDebugNativeFrame interface [.NET Framework debugging]
ms.assetid: 04819c58-7246-4b32-befb-680cf1dbc436
topic_type:
- apiref
ms.openlocfilehash: e417184c9f1ca5136e1b4dba07820fd8242ae932
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729127"
---
# <a name="icordebugnativeframe-interface"></a>Interface ICorDebugNativeFrame

Uma implementação especializada de ICorDebugFrame usada para quadros nativos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CanSetIP](icordebugnativeframe-cansetip-method.md)|Obtém um valor que indica se é seguro definir o ponteiro de instrução para o local de deslocamento especificado no código nativo.|  
|[Método GetIP](icordebugnativeframe-getip-method.md)|Obtém o deslocamento do quadro de pilha no código nativo.|  
|[Método GetLocalDoubleRegisterValue](icordebugnativeframe-getlocaldoubleregistervalue-method.md)|Obtém um ponteiro para um ICorDebugValue que representa o valor de um argumento ou variável local armazenado em dois registros de memória de um quadro nativo.|  
|[Método GetLocalMemoryRegisterValue](icordebugnativeframe-getlocalmemoryregistervalue-method.md)|Obtém um ponteiro para um `ICorDebugValue` que representa o valor de uma variável local, da qual os bits baixos são armazenados no registro especificado e os bits altos são armazenados no endereço de memória especificado.|  
|[Método GetLocalMemoryValue](icordebugnativeframe-getlocalmemoryvalue-method.md)|Obtém um ponteiro para um `ICorDebugValue` que representa o valor de uma variável local armazenada no endereço de memória especificado.|  
|[Método GetLocalRegisterMemoryValue](icordebugnativeframe-getlocalregistermemoryvalue-method.md)|Obtém um ponteiro para um `ICorDebugValue` que representa o valor de uma variável local, da qual os bits altos são armazenados no registro especificado e os bits baixos são armazenados no endereço de memória especificado|  
|[Método GetLocalRegisterValue](icordebugnativeframe-getlocalregistervalue-method.md)|Obtém um ponteiro para um `ICorDebugValue` que representa o valor de um argumento ou uma variável local armazenada no registro nativo especificado.|  
|[Método GetRegisterSet](icordebugnativeframe-getregisterset-method.md)|Obtém um ponteiro para um [ICorDebugRegisterSet](icordebugregisterset-interface.md) que representa o conjunto de registros para isso `ICorDebugNativeFrame` .|  
|[Método SetIP](icordebugnativeframe-setip-method.md)|Define o ponteiro de instrução para o local de deslocamento especificado no código nativo.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
