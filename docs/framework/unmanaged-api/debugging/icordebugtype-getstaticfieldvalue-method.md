---
description: 'Saiba mais sobre o método: ICorDebugType:: GetStaticFieldValue'
title: Método ICorDebugType::GetStaticFieldValue
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 62eb5d55-53ee-4fb3-8d47-7b6c96808f9e
topic_type:
- apiref
ms.openlocfilehash: 378c72f24fedd76f40704ff684781bed124055bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658224"
---
# <a name="icordebugtypegetstaticfieldvalue-method"></a>Método ICorDebugType::GetStaticFieldValue

Obtém um ponteiro de interface para um objeto ICorDebugValue que contém o valor do campo estático referenciado pelo token de campo especificado no quadro de ativação especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef        fieldDef,  
    [in]  ICorDebugFrame    *pFrame,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fieldDef`  
 no Um `mdFieldDef` token que especifica o campo estático.  
  
 `pFrame`  
 no Um ponteiro para um ICorDebugFrame que representa o quadro de pilha.  
  
 `ppValue`  
 fora Um ponteiro para o endereço de um `ICorDebugValue` que contém o valor do campo estático.  
  
## <a name="remarks"></a>Comentários  

 O `GetStaticFieldValue` método poderá ser usado somente se o tipo for ELEMENT_TYPE_CLASS ou ELEMENT_TYPE_VALUETYPE, conforme indicado pelo método [ICorDebugType:: GetType](icordebugtype-gettype-method.md) .  
  
 Para tipos não genéricos, a operação executada pelo `GetStaticFieldValue` é idêntica à chamada de [ICorDebugClass:: GetStaticFieldValue](icordebugclass-getstaticfieldvalue-method.md) no objeto ICorDebugClass retornado por [ICorDebugType:: GetClass](icordebugtype-getclass-method.md).  
  
 Para tipos genéricos, um valor de campo estático será relativo a uma instanciação específica. Além disso, se o campo estático puder ser relativo a um thread, um contexto ou um domínio de aplicativo, o quadro de pilha ajudará o depurador a determinar o valor adequado.  
  
## <a name="remarks"></a>Comentários  

 `GetStaticFieldValue` pode ser usado somente quando uma chamada para `ICorDebugType::GetType` retorna um valor de ELEMENT_TYPE_CLASS ou ELEMENT_TYPE_VALUETYPE.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
