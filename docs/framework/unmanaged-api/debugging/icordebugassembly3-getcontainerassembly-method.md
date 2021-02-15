---
description: 'Saiba mais sobre o método: ICorDebugAssembly3:: GetContainerAssembly'
title: Método ICorDebugAssembly3::GetContainerAssembly
ms.date: 03/30/2017
ms.assetid: f5fddeb6-b82e-4ebb-b432-849ce8513c77
ms.openlocfilehash: 5a6bc6dfb1c8403137a9444ff1cc4f64e75da65d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791511"
---
# <a name="icordebugassembly3getcontainerassembly-method"></a>Método ICorDebugAssembly3::GetContainerAssembly

Retorna o assembly do contêiner desse objeto `ICorDebugAssembly3`.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetContainerAssembly(  
    ICorDebugAssembly **ppAssembly  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppAssembly`  
 Um ponteiro para o endereço de um objeto ICorDebugAssembly que representa o assembly do contêiner ou **nulo** se a chamada do método falhar.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` se a chamada do método for concluída com sucesso; caso contrário, `S_FALSE` , e `ppAssembly` será **nulo**.  
  
## <a name="remarks"></a>Comentários  

 Se esse assembly foi mesclado com outros dentro de um assembly de contêiner único, esse método retorna o assembly do contêiner. Para obter mais informações e terminologia, consulte o tópico [ICorDebugProcess6:: EnableVirtualModuleSplitting](icordebugprocess6-enablevirtualmodulesplitting-method.md) .  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugAssembly3](icordebugassembly3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
