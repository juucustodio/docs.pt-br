---
description: 'Saiba mais sobre o método: ICorDebugModuleDebugEvent:: GetModule'
title: 'Método ICorDebugModuleDebugEvent:: GetModule'
ms.date: 03/30/2017
ms.assetid: b1141c35-4253-4e34-b3e4-ed406a9dea4f
ms.openlocfilehash: c6d7171da231576ff90f54aaefe4b473af0afd40
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790731"
---
# <a name="icordebugmoduledebugeventgetmodule-method"></a>Método ICorDebugModuleDebugEvent:: GetModule

Obtém o módulo mesclado que acabou de ser carregado ou descarregado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetModule(  
   [out]ICorDebugModule **ppModule  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppModule`  
 fora Um ponteiro para o endereço de um objeto ICorDebugModule que representa o módulo mesclado que acabou de ser carregado ou descarregado.  
  
## <a name="remarks"></a>Comentários  

 Você pode chamar o método [GetEventKind](icordebugdebugevent-geteventkind-method.md) para determinar se o módulo foi carregado ou descarregado.  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugModuleDebugEvent](icordebugmoduledebugevent-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
