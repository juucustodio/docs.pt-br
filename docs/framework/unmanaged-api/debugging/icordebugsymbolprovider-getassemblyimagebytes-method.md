---
description: 'Saiba mais sobre o método: ICorDebugSymbolProvider:: GetAssemblyImageBytes'
title: 'Método ICorDebugSymbolProvider:: GetAssemblyImageBytes'
ms.date: 03/30/2017
ms.assetid: 3db215aa-e180-4f70-8d23-6d5a0ffbc8e5
ms.openlocfilehash: 2e08b23e35913e8767135d75d28ff66efc890565
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717271"
---
# <a name="icordebugsymbolprovidergetassemblyimagebytes-method"></a>Método ICorDebugSymbolProvider:: GetAssemblyImageBytes

Lê dados de um assembly mesclado, dado um endereço virtual relativo (RVA) no assembly mesclado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAssemblyImageBytes(  
   [in] CORDB_ADDRESS rva,
   [in] ULONG32 length,
   [out] ICorDebugMemoryBuffer** ppMemoryBuffer  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `rva`  
 no Um RVA (endereço virtual relativo) em um assembly mesclado.  
  
 `length`  
 O número de bytes a serem lidos do assembly mesclado.  
  
 `ppMemoryBuffer`  
 Um ponteiro para o endereço de um objeto [ICorDebugMemoryBuffer](icordebugmemorybuffer-interface.md) que contém informações sobre o buffer de memória com metadados de assembly mesclados.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
