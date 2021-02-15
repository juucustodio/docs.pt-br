---
description: 'Saiba mais sobre o método: ICorDebugSymbolProvider:: GetMergedAssemblyRecords'
title: 'Método ICorDebugSymbolProvider:: GetMergedAssemblyRecords'
ms.date: 03/30/2017
ms.assetid: cc4c510d-550d-4941-af34-81987caf3425
ms.openlocfilehash: f12bb3a49d7b49f9f8916c9d04417340502d44ba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659875"
---
# <a name="icordebugsymbolprovidergetmergedassemblyrecords-method"></a>Método ICorDebugSymbolProvider:: GetMergedAssemblyRecords

Obtém os registros de símbolo de todos os assemblies mesclados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMergedAssemblyRecords(  
   [in] ULONG32 cRequestedRecords,  
   [out] ULONG32 *pcFetchedRecords,  
   [out, size_is(cRequestedRecords), length_is(*pcFetchedRecords)] ICorDebugMergedAssemblyRecord *pRecords[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cRequestedRecords`  
 no O número de registros de símbolo solicitado.  
  
 `pcFetchedRecords`  
 fora Um ponteiro para o número de registros de símbolo recuperados pelo método.  
  
 `pRecords`  
 Um ponteiro para uma matriz de objetos [ICorDebugMergedAssemblyRecord](icordebugmergedassemblyrecord-interface.md) .  
  
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
