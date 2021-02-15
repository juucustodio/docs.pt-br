---
description: 'Saiba mais sobre o método: ICorDebugFunction:: GetLocalVarSigToken'
title: Método ICorDebugFunction::GetLocalVarSigToken
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetLocalVarSigToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetLocalVarSigToken
helpviewer_keywords:
- ICorDebugFunction::GetLocalVarSigToken method [.NET Framework debugging]
- GetLocalVarSigToken method [.NET Framework debugging]
ms.assetid: 31e53494-bcc9-4981-91a4-f7e0f02cad48
topic_type:
- apiref
ms.openlocfilehash: cd7fb03829285ddcb1da2f1a93985fa1f98d3d39
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692492"
---
# <a name="icordebugfunctiongetlocalvarsigtoken-method"></a>Método ICorDebugFunction::GetLocalVarSigToken

Obtém o token de metadados para a assinatura de variável local da função que é representada por essa instância de ICorDebugFunction.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalVarSigToken (  
    [out] mdSignature *pmdSig  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pmdSig`  
 fora Um ponteiro para o `mdSignature` token para a assinatura de variável local dessa função ou `mdSignatureNil` , se essa função não tiver nenhuma variável local.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
