---
title: Método ICorDebugHeapValue2::CreateHandle
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue2.CreateHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type:
- apiref
ms.openlocfilehash: cbc056e9a3cc00178b32dee4011da4403dff508a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212770"
---
# <a name="icordebugheapvalue2createhandle-method"></a>Método ICorDebugHeapValue2::CreateHandle
Cria um identificador do tipo especificado para o valor de heap representado por esse objeto ICorDebugHeapValue2.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `type`  
 no Um valor da Enumeração CorDebugHandleType que especifica o tipo de identificador a ser criado.  
  
 `ppHandle`  
 fora Um ponteiro para o endereço de um objeto ICorDebugHandleValue que representa o novo identificador para esse valor de heap.  
  
## <a name="remarks"></a>Comentários  
 O identificador será criado no domínio do aplicativo que está associado ao valor de heap e se tornará inválido se o domínio do aplicativo for descarregado.  
  
 Várias chamadas para essa função para o mesmo valor de heap criarão vários identificadores. Como os identificadores afetam o desempenho do coletor de lixo, o depurador deve se limitar a um número relativamente pequeno de identificadores (cerca de 256) que estejam ativos por vez.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
