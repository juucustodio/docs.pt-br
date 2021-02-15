---
description: 'Saiba mais sobre o método: ICorDebugEval:: NewObject'
title: Método ICorDebugEval::NewObject
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewObject
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewObject
helpviewer_keywords:
- NewObject method [.NET Framework debugging]
- ICorDebugEval::NewObject method [.NET Framework debugging]
ms.assetid: ce3025e8-defa-4c5e-8298-f49d71fa5736
topic_type:
- apiref
ms.openlocfilehash: 0f7feb53d061e5dbc453015772b97f2a5a59bbb3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693948"
---
# <a name="icordebugevalnewobject-method"></a>Método ICorDebugEval::NewObject

Aloca uma nova instância de objeto e chama o método de Construtor especificado.  
  
 Esse método é obsoleto no .NET Framework versão 2,0. Use [ICorDebugEval2:: NewParameterizedObject](icordebugeval2-newparameterizedobject-method.md) em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT NewObject (  
    [in] ICorDebugFunction  *pConstructor,  
    [in] ULONG32            nArgs,  
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pConstructor`  
 no O Construtor a ser chamado.  
  
 `nArgs`  
 no O tamanho da `ppArgs` matriz.  
  
 `ppArgs`  
 no Uma matriz de objetos ICorDebugValue, cada um dos quais representa um argumento a ser passado para o construtor.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Consulte também

- [Método NewParameterizedObject](icordebugeval2-newparameterizedobject-method.md)
