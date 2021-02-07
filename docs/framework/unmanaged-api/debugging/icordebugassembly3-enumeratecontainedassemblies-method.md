---
description: 'Saiba mais sobre o método: ICorDebugAssembly3:: EnumerateContainedAssemblies'
title: Método ICorDebugAssembly3::EnumerateContainedAssemblies
ms.date: 03/30/2017
ms.assetid: 98f15b05-afad-4616-9e2a-1a9af31948b6
ms.openlocfilehash: 8933500713661ef785eb3ce5abc574e512580b6b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754076"
---
# <a name="icordebugassembly3enumeratecontainedassemblies-method"></a>Método ICorDebugAssembly3::EnumerateContainedAssemblies

Obtém um enumerador para os assemblies contidos neste assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateContainedAssemblies(  
    ICorDebugAssemblyEnum **ppAssemblies  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppAssemblies`  
 [out] Um ponteiro para o endereço de um objeto de interface ICorDebugAssemblyEnum que é o enumerador.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se este objeto `ICorDebugAssembly3` for um contêiner; caso contrário, `S_FALSE`, e a enumeração está vazia.  
  
## <a name="remarks"></a>Comentários  

 Símbolos são necessários para enumerar os assemblies contidos. Se eles não estiverem presentes, o método retorna `S_FALSE`, e nenhum enumerador válido é fornecido.  
  
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
