---
description: 'Saiba mais sobre o método: ICorDebugDataTarget2:: EnumerateThreadIDs'
title: Método ICorDebugDataTarget2::EnumerateThreadIDs
ms.date: 03/30/2017
ms.assetid: af02460f-2a45-496e-bc4e-a1ac4f80fe11
ms.openlocfilehash: 5bbda67e6c6de81e9de566a68f772f324d79b92f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710550"
---
# <a name="icordebugdatatarget2enumeratethreadids-method"></a>Método ICorDebugDataTarget2::EnumerateThreadIDs

Retorna uma lista de IDs de thread ativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateThreadIDs(  
    [in] ULONG32 cThreadIds,
    [out] ULONG32 *pcThreadIds,
    [out, size_is(cThreadIds), length_is(*pcThreadIds)] ULONG32 pThreadIds[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 cThreadIDs  
 [in] O número máximo de threads cujos IDs podem ser retornados.  
  
 pcThreadIds  
 [out] Um ponteiro para um `ULONG32` que indica o número real de IDs de thread gravadas na matriz `pThreadIds`.  
  
 pThreadIDs  
 Uma matriz de identificadores de thread.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** Consulte [requisitos do sistema](../../get-started/system-requirements.md). **Cabeçalho:** CorDebug. idl, CorDebug. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugDataTarget2](icordebugdatatarget2-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
