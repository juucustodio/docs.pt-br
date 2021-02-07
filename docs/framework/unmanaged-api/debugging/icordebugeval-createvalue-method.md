---
description: 'Saiba mais sobre o método: ICorDebugEval:: CreateValue'
title: Método ICorDebugEval::CreateValue
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CreateValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CreateValue
helpviewer_keywords:
- ICorDebugEval::CreateValue method [.NET Framework debugging]
- CreateValue method [.NET Framework debugging]
ms.assetid: 9a1c0b47-6f10-4fcb-844a-4ab2d7990140
topic_type:
- apiref
ms.openlocfilehash: f5ea753b5b95c68136e7b799aad88eee5845ea82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99694156"
---
# <a name="icordebugevalcreatevalue-method"></a>Método ICorDebugEval::CreateValue

Cria um valor do tipo especificado, com um valor inicial de zero ou NULL.  
  
 Esse método é obsoleto no .NET Framework versão 2,0. Use [ICorDebugEval2:: CreateValueForType](icordebugeval2-createvaluefortype-method.md) em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateValue (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `elementType`  
 no Um valor da enumeração [CorElementType](../metadata/corelementtype-enumeration.md) que especifica o tipo do valor.  
  
 `pElementClass`  
 no Ponteiro para um objeto [ICorDebugClass](icordebugclass-interface.md) que especifica a classe do valor, se o tipo não for um tipo primitivo.  
  
 `ppValue`  
 fora Ponteiro para o endereço de um objeto "ICorDebugValue" que representa o valor.  
  
## <a name="remarks"></a>Comentários  

 `CreateValue` Cria um `ICorDebugValue` objeto do tipo fornecido para o único propósito de usá-lo em uma avaliação de função. Esse objeto de valor pode ser usado para passar constantes de usuário como parâmetros.  
  
 Se o tipo do valor for um tipo primitivo, seu valor inicial será zero ou NULL. Use [ICorDebugGenericValue:: SetValue](icordebuggenericvalue-setvalue-method.md) para definir o valor de um tipo primitivo.  
  
 Se o valor de `elementType` for ELEMENT_TYPE_CLASS, você obterá um "ICorDebugReferenceValue" (retornado em `ppValue` ) que representa a referência de objeto nulo. Você pode usar esse objeto para passar NULL para uma avaliação de função que tem parâmetros de referência de objeto. Você não pode definir `ICorDebugValue` como qualquer coisa; ela sempre permanece nula.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Consulte também

- [Método CreateValueForType](icordebugeval2-createvaluefortype-method.md)
- [Interface ICorDebugEval](icordebugeval-interface.md)
