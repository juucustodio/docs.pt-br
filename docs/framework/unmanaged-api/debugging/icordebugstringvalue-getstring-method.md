---
description: 'Saiba mais sobre o método: ICorDebugStringValue:: GetString'
title: Método ICorDebugStringValue::GetString
ms.date: 03/30/2017
api_name:
- ICorDebugStringValue.GetString
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStringValue::GetString
helpviewer_keywords:
- ICorDebugStringValue::GetString method [.NET Framework debugging]
- GetString method, ICorDebugStringValue interface [.NET Framework debugging]
ms.assetid: 2b94bda7-09ee-435d-91b9-c4e31af1896c
topic_type:
- apiref
ms.openlocfilehash: 06e8e039c8b0afb7753a398302a9b32eb3ba7213
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717333"
---
# <a name="icordebugstringvaluegetstring-method"></a>Método ICorDebugStringValue::GetString

Obtém a cadeia de caracteres referenciada por este ICorDebugStringValue.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetString (  
    [in] ULONG32    cchString,  
    [out] ULONG32   *pcchString,  
    [out, size_is(cchString), length_is(*pcchString)]
        WCHAR       szString[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchString`  
 no O tamanho da `szString` matriz.  
  
 `pcchString`  
 fora Um ponteiro para o número de caracteres retornados na `szString` matriz.  
  
 `szString`  
 fora Uma matriz que armazena a cadeia de caracteres recuperada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
