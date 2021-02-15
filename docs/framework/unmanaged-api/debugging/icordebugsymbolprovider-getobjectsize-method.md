---
description: 'Saiba mais sobre o método: ICorDebugSymbolProvider:: GetObjects'
title: 'Método ICorDebugSymbolProvider:: getobjectize'
ms.date: 03/30/2017
ms.assetid: 3c564396-ac64-4ef3-b4f6-df96f1d46fc7
ms.openlocfilehash: 72720a1af9958fd0ab91276b3967733cec77fee7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659694"
---
# <a name="icordebugsymbolprovidergetobjectsize-method"></a>Método ICorDebugSymbolProvider:: getobjectize

Retorna o tamanho do objeto de um objeto com base em sua assinatura de TypeSpec.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetObjectSize(  
   [in] ULONG32 cbSignature,  
   [in, size_is(cbSignature)]  BYTE typeSig[],  
   [out] ULONG32 *pObjectSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cbSignature`  
 no O número de bytes na assinatura TypeSpec.  
  
 typeSig  
 no A assinatura TypeSpec.  
  
 `pObjectSize`  
 fora Um ponteiro para o tamanho do objeto.  
  
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
