---
description: 'Saiba mais sobre o método: ICorDebugObjectValue:: GetFieldValue'
title: Método ICorDebugObjectValue::GetFieldValue
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetFieldValue
helpviewer_keywords:
- ICorDebugObjectValue::GetFieldValue method [.NET Framework debugging]
- GetFieldValue method [.NET Framework debugging]
ms.assetid: c96770b0-3e09-47bb-bd29-20353b043459
topic_type:
- apiref
ms.openlocfilehash: 38dac36747b286ab16ae3310b6b59695480a6ff1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722185"
---
# <a name="icordebugobjectvaluegetfieldvalue-method"></a>Método ICorDebugObjectValue::GetFieldValue

Obtém o valor do campo especificado da classe especificada para esse valor de objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFieldValue (  
    [in]  ICorDebugClass     *pClass,  
    [in]  mdFieldDef         fieldDef,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pClass`  
 no Um ponteiro para um objeto "ICorDebugClass" que representa a classe para a qual obter o valor do campo.  
  
 `fieldDef`  
 no Um `mdFieldDef` token que faz referência aos metadados que descrevem o campo.  
  
 `ppValue`  
 fora Um ponteiro para um objeto "ICorDebugValue" que representa o valor do campo especificado.  
  
## <a name="remarks"></a>Comentários  

 A classe, especificada no `pClass` parâmetro, deve estar na hierarquia da classe do valor do objeto e o campo deve ser um campo dessa classe.  
  
 O `GetFieldValue` método ainda terá sucesso para objetos genéricos e classes genéricas. Por exemplo, se MyDictionary \<V> herda de Dictionary \<string,V> e o valor Object for do tipo MyDictionary \<int32> , passar o `ICorDebugClass` objeto para Dictionary \<K,V> obterá com êxito um campo de Dictionary \<string,int32> .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
