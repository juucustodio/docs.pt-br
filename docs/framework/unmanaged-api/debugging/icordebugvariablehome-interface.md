---
description: 'Saiba mais sobre: interface ICorDebugVariableHome'
title: Interface ICorDebugVariableHome
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugVariableHome
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome
helpviewer_keywords:
- ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: 76f2bf3b-759f-4eed-bce7-119415b25915
topic_type:
- apiref
ms.openlocfilehash: a1dcc959ba9aeffc0e511dcd2f5bb15f58445139
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790627"
---
# <a name="icordebugvariablehome-interface"></a>Interface ICorDebugVariableHome

Representa uma variável local ou um argumento de uma função.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetArgumentIndex](icordebugvariablehome-getargumentindex-method.md)|Obtém o índice de um argumento de função.|  
|[Método GetCode](icordebugvariablehome-getcode-method.md)|Obtém a instância "ICorDebugCode" que contém este `ICorDebugVariableHome` objeto.|  
|[Método GetLiveRange](icordebugvariablehome-getliverange-method.md)|Obtém o intervalo nativo no qual essa variável está ativa.|  
|[Método GetLocationType](icordebugvariablehome-getlocationtype-method.md)|Obtém o tipo do local nativo da variável.|  
|[Método GetOffset](icordebugvariablehome-getoffset-method.md)|Obtém o deslocamento do registro base de uma variável.|  
|[Método GetRegister](icordebugvariablehome-getregister-method.md)|Obtém o registro que contém uma variável com um tipo de local de `VLT_REGISTER` e o registro base para uma variável com um tipo de local de `VLT_REGISTER_RELATIVE` .|  
|[Método GetSlotIndex](icordebugvariablehome-getslotindex-method.md)|Obtém o índice de slot gerenciado de uma variável local.|  
  
## <a name="example"></a>Exemplo  

 O fragmento de código a seguir usa o objeto [ICorDebugCode4](icordebugcode4-interface.md) chamado `pCode4` .  
  
```cpp  
ICorDebugCode4 *pCode4 = NULL;  
pCode->QueryInterface(IID_ICorDebugCode4, &pCode4);  
  
ICorDebugVariableEnum *pVarLocEnum = NULL;  
pCode4->EnumerateVariableHomes(&pVarLocEnum);  
  
// retrieve local variables and arguments  
ULONG celt = 0;  
pVarLocEnum->GetCount(&celt);  
ICorDebugVariableHome **homes = new ICorDebugVariableHome *[celt];  
ULONG celtFetched = 0;  
pVarLocEnum->Next(celt, homes, &celtFetched);  
  
for (int i = 0; i < celtFetched; i++)  
{  
    VariableLocationType locType = VLT_INVALID;  
    homes[i].GetLocationType(&locType);  
    switch (locType)  
    {  
    case VLT_REGISTER:  
        CorDebugRegister register = 0;  
        locals[i].GetRegister(&register);  
        // now we know which register it is in  
        break;  
    case VLT_REGISTER_RELATIVE:  
        CorDebugRegister baseRegister = 0;  
        LONG offset = 0;  
        locals[i].GetRegister(&register);  
        locals[i].GetOffset(&offset);  
        // now we know the register-relative offset  
        break;  
    case VLT_INVALID:  
        // handle case where we can't access the location  
        break;  
    }  
}  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Interface ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md)
