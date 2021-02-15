---
description: 'Saiba mais sobre o método: ICorDebugChain:: GetStackRange'
title: Método ICorDebugChain::GetStackRange
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetStackRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetStackRange
helpviewer_keywords:
- ICorDebugChain::GetStackRange method [.NET Framework debugging]
- GetStackRange method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 554284e7-3f6c-4d40-8da5-1c9317fbd484
topic_type:
- apiref
ms.openlocfilehash: 066dda06564655350d799dabb54acd622b828172
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99694915"
---
# <a name="icordebugchaingetstackrange-method"></a>Método ICorDebugChain::GetStackRange

Obtém o intervalo de endereços do segmento da pilha para esta cadeia.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStackRange (  
    [out] CORDB_ADDRESS      *pStart,
    [out] CORDB_ADDRESS      *pEnd  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pStart`  
 fora Um ponteiro para um `CORDB_ADDRESS` valor que é o endereço inicial do segmento da pilha.  
  
 `pEnd`  
 fora Um ponteiro para um `CORDB_ADDRESS` valor que é o endereço final do segmento da pilha.  
  
## <a name="remarks"></a>Comentários  

 O intervalo numérico é significativo apenas para comparação de locais de quadros de pilha. Você não pode fazer suposições sobre o que realmente está armazenado na pilha.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
