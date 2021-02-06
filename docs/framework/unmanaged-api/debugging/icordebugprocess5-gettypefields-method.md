---
description: 'Saiba mais sobre o método: ICorDebugProcess5:: GetTypeFields'
title: Método ICorDebugProcess5::GetTypeFields
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.GetTypeFields
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetTypeFields
helpviewer_keywords:
- GetTypeFields method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::GetTypeFields method [.NET Framework debugging]
ms.assetid: 6a0ad3ee-dacb-47e9-abae-4536bcc4804b
topic_type:
- apiref
ms.openlocfilehash: bdbb0be76400262d83876b9fc37cc4f00eb34e43
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649810"
---
# <a name="icordebugprocess5gettypefields-method"></a>Método ICorDebugProcess5::GetTypeFields

Fornece informações sobre os campos que pertencem a um tipo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetTypeFields(  
    [in] COR_TYPEID id,  
    [in] ULONG32 celt,  
    [out] COR_FIELD fields[],
    [out] ULONG32 *pceltNeeded  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `id`  
 no O identificador do tipo cujas informações de campo são recuperadas.  
  
 `celt`  
 no O número de objetos [COR_FIELD](cor-field-structure.md) cujas informações de campo serão recuperadas.  
  
 `fields`  
 fora Uma matriz de objetos [COR_FIELD](cor-field-structure.md) que fornece informações sobre os campos que pertencem ao tipo.  
  
 `pceltNeeded`  
 fora Um ponteiro para o número de objetos [COR_FIELD](cor-field-structure.md) incluídos no `fields` .  
  
## <a name="remarks"></a>Comentários  

 O `celt` parâmetro, que especifica o número de campos cujas informações de campo o método usa para preencher `fields` , deve corresponder ao valor do `COR_TYPE_LAYOUT::numFields` campo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugProcess5](icordebugprocess5-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
