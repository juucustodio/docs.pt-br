---
description: 'Saiba mais sobre: ICorDebugAssemblyEnum:: Next Method'
title: Método ICorDebugAssemblyEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugAssemblyEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssemblyEnum::Next method
helpviewer_keywords:
- ICorDebugAssemblyEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugAssemblyEnum interface [.NET Framework debugging]
ms.assetid: b3e7d0c2-3baa-4ef8-8e3f-b865cf252940
topic_type:
- apiref
ms.openlocfilehash: feb77f22ec59fcc0e1b3f5590b7aee4efba13d01
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772218"
---
# <a name="icordebugassemblyenumnext-method"></a>Método ICorDebugAssemblyEnum::Next

Obtém o número especificado de assemblies da coleção, começando na posição atual do cursor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugAssembly *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de assemblies a serem recuperados.  
  
 `values`  
 fora Uma matriz de ponteiros, cada um dos quais aponta para um objeto ICorDebugAssembly que representa um assembly.  
  
 `pceltFetched`  
 fora Um ponteiro para o número de assemblies realmente retornados. Esse valor pode ser nulo se `celt` for um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
