---
description: 'Saiba mais sobre o método: ICorDebugVariableHome:: getregister'
title: 'Método ICorDebugVariableHome:: getregister'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetRegister
helpviewer_keywords:
- ICorDebugVariableHome::GetRegister method [.NET Framework debugging]
- GetRegister method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: a5eecd7b-b04c-4266-bff2-7c8771d519a8
topic_type:
- apiref
ms.openlocfilehash: c394d455048cf7451b8320ed72a6aa7adfb3518e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790653"
---
# <a name="icordebugvariablehomegetregister-method"></a>Método ICorDebugVariableHome:: getregister

Obtém o registro que contém uma variável com um tipo de local de `VLT_REGISTER` e o registro base para uma variável com um tipo de local de `VLT_REGISTER_RELATIVE` .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegister(  
    [out] CorDebugRegister *pRegister  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRegister`  
 fora Um valor de enumeração CorDebugRegister que indica o registro para uma variável com um tipo de local de `VLT_REGISTER` e o registro base para uma variável com um tipo de local de `VLT_REGISTER_RELATIVE` .  
  
## <a name="return-value"></a>Valor retornado  

 O método retorna os seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|A variável está no registro indicado pelo `pRegister` argumento.|  
|`E_FAIL`|A variável não está em um local de registro ou relativo ao registro.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração VariableLocationType](variablelocationtype-enumeration.md)
- [Interface ICorDebugVariableHome](icordebugvariablehome-interface.md)
