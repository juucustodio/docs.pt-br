---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet2:: GetRegistersAvailable'
title: Método ICorDebugRegisterSet2::GetRegistersAvailable
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegistersAvailable
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegistersAvailable
helpviewer_keywords:
- GetRegistersAvailable method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegistersAvailable method [.NET Framework debugging]
ms.assetid: f3ed344b-0d3a-44e8-8000-2a97e0805a2c
topic_type:
- apiref
ms.openlocfilehash: 3839647e69efd63aefd1aa154c457f292e684336
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790715"
---
# <a name="icordebugregisterset2getregistersavailable-method"></a>Método ICorDebugRegisterSet2::GetRegistersAvailable

Obtém uma matriz de bytes que fornece um bitmap dos registros disponíveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegistersAvailable (  
    [in] ULONG32 numChunks,  
    [out, size_is(numChunks)] BYTE availableRegChunks[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `numChunks`  
 no O tamanho da `availableRegChunks` matriz.  
  
 `availableRegChunks`  
 fora Uma matriz de bytes, cada bit corresponde a um registro. Se um registro estiver disponível, o bit correspondente do registro será definido.  
  
## <a name="remarks"></a>Comentários  

 Os valores da enumeração CorDebugRegister especificam os registros de diferentes microprocessadores. Os cinco bits superiores de cada valor são o índice na `availableRegChunks` matriz de bytes. Os três bits inferiores de cada valor identificam a posição do bit dentro do byte indexado. Dado um `CorDebugRegister` valor que especifica um registro específico, a posição do registro na máscara é determinada da seguinte maneira:  
  
1. Extraia o índice necessário para acessar o byte correto na `availableRegChunks` matriz:  
  
     `CorDebugRegister` valor >> 3  
  
2. Extraia a posição do bit dentro do byte indexado, em que bit zero é o bit menos significativo:  
  
     `CorDebugRegister` valor & 7  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
