---
description: 'Saiba mais sobre o método: ICorDebugFunction:: GetClass'
title: Método ICorDebugFunction::GetClass
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetClass
helpviewer_keywords:
- GetClass method, ICorDebugFunction interface [.NET Framework debugging]
- ICorDebugFunction::GetClass method [.NET Framework debugging]
ms.assetid: 27967230-144f-40d3-9e23-961d0241abd9
topic_type:
- apiref
ms.openlocfilehash: 09049962082bc51cc47a56b0de591a26c2ef93fc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692583"
---
# <a name="icordebugfunctiongetclass-method"></a>Método ICorDebugFunction::GetClass

Obtém um objeto ICorDebugClass que representa a classe da qual essa função é membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetClass (  
    [out] ICorDebugClass **ppClass  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppClass`  
 fora Um ponteiro para o endereço do `ICorDebugClass` objeto que representa a classe, ou NULL, se essa função não for um membro de uma classe.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
