---
description: 'Saiba mais sobre o método: ICorDebugFunction:: GetCurrentVersionNumber'
title: Método ICorDebugFunction::GetCurrentVersionNumber
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetCurrentVersionNumber
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetCurrentVersionNumber
helpviewer_keywords:
- GetCurrentVersionNumber method [.NET Framework debugging]
- ICorDebugFunction::GetCurrentVersionNumber method [.NET Framework debugging]
ms.assetid: c3af1575-cbe6-457a-bc08-c53460edcbc8
topic_type:
- apiref
ms.openlocfilehash: ccc96755ac74624a00b806e3f569f39f2d6059f5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692531"
---
# <a name="icordebugfunctiongetcurrentversionnumber-method"></a>Método ICorDebugFunction::GetCurrentVersionNumber

Obtém o número de versão da edição mais recente feita à função representada por esse objeto ICorDebugFunction.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCurrentVersionNumber (  
    [out] ULONG32 *pnCurrentVersion  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pnCurrentVersion`  
 fora Um ponteiro para um valor inteiro que é o número de versão da edição mais recente feita nessa função.  
  
## <a name="remarks"></a>Comentários  

 O número de versão da edição mais recente feita a essa função pode ser maior que o número de versão da própria função. Use o método [ICorDebugFunction2:: GetVersionNumber](icordebugfunction2-getversionnumber-method.md) ou o método [ICorDebugCode:: GetVersionNumber](icordebugcode-getversionnumber-method.md) para recuperar o número de versão da função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
