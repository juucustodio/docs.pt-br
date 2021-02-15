---
description: 'Saiba mais sobre o método: ICorDebugDataTarget:: ReadVirtual'
title: Método ICorDebugDataTarget::ReadVirtual
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.ReadVirtual Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::ReadVirtual
helpviewer_keywords:
- ICorDebugDataTarget::ReadVirtual method [.NET Framework debugging]
- ReadVirtual method, ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: 55e57640-b3d2-413d-b4f4-fbc27fb8e37c
topic_type:
- apiref
ms.openlocfilehash: 4525ba1e5dc685813d963dab96879b886987f38f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710589"
---
# <a name="icordebugdatatargetreadvirtual-method"></a>Método ICorDebugDataTarget::ReadVirtual

Obtém um bloco de memória contígua a partir do endereço especificado e a retorna no buffer fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ReadVirtual(  
    [in] CORDB_ADDRESS   address,  
    [out, size_is(bytesRequested), length_is(*pBytesRead)]  
          BYTE *     pBuffer,  
    [in]  ULONG32    bytesRequested,  
    [out] ULONG32 *  pBytesRead);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no O endereço inicial da memória solicitada.  
  
 `pbuffer`  
 fora O buffer em que a memória será armazenada.  
  
 `bytesRequested`  
 no O número de bytes a serem obtidos do endereço de destino.  
  
 `pBytesRead`  
 fora O número de bytes realmente lidos do endereço de destino. Isso pode ser menor que `bytesRequested` .  
  
## <a name="remarks"></a>Comentários  

 Se o primeiro byte (no endereço inicial especificado) puder ser lido, a chamada deverá retornar êxito (para dar suporte à leitura eficiente de estruturas de dados com comprimento autodescritivo, como cadeias de caracteres terminadas em nulo).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugDataTarget](icordebugdatatarget-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
