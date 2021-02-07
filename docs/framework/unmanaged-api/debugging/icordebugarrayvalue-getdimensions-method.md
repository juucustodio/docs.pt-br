---
description: 'Saiba mais sobre o método: ICorDebugArrayValue:: GetDimensions'
title: Método ICorDebugArrayValue::GetDimensions
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetDimensions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetDimensions
helpviewer_keywords:
- ICorDebugArrayValue::GetDimensions method [.NET Framework debugging]
- GetDimensions method [.NET Framework debugging]
ms.assetid: 6c116592-134b-4ef2-a319-680e92d013aa
topic_type:
- apiref
ms.openlocfilehash: 007a48891a01e5779e3f9ef10cec720d6647c8f3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723095"
---
# <a name="icordebugarrayvaluegetdimensions-method"></a>Método ICorDebugArrayValue::GetDimensions

Obtém o número de elementos em cada dimensão dessa matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDimensions (  
    [in] ULONG32         cdim,  
    [out, size_is(cdim), length_is(cdim)]
        ULONG32          dims[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cdim`  
 no O número de dimensões deste objeto ICorDebugArrayValue.  
  
 Esse valor também é o tamanho da `dims` matriz porque seu tamanho é igual ao número de dimensões do `ICorDebugArrayValue` objeto.  
  
 `dims`  
 fora Uma matriz de inteiros, cada um dos quais Especifica o número de elementos em uma dimensão neste `ICorDebugArrayValue` objeto.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
