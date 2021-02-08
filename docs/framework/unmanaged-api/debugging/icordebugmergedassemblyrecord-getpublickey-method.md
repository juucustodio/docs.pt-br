---
description: 'Saiba mais sobre: ICorDebugMergedAssemblyRecord:: método GetPublicKey'
title: 'Método ICorDebugMergedAssemblyRecord:: GetPublicKey'
ms.date: 03/30/2017
ms.assetid: 6f4e78ba-082b-489d-8b58-4c35fbcc7a5b
ms.openlocfilehash: 15175b0d02773bcbce46bfaec9ce1de3021b7dde
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801092"
---
# <a name="icordebugmergedassemblyrecordgetpublickey-method"></a>Método ICorDebugMergedAssemblyRecord:: GetPublicKey

Obtém a chave pública do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetPublicKey(  
   [in] ULONG32 cbPublicKey,
   [out] ULONG32 *pcbPublicKey,
   [out, size_is(cbPublicKey), length_is(*pcbPublicKey)] BYTE pbPublicKey[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cbPublicKey`  
 no O número máximo de bytes na `pbPublicKey` matriz.  
  
 `pcbPublicKey`  
 fora Um ponteiro para o número real de bytes gravados na `pbPublicKey` matriz.  
  
 `pbPublicKey`  
 fora Um ponteiro para uma matriz de bytes que contém a chave pública do assembly.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMergedAssemblyRecord](icordebugmergedassemblyrecord-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
