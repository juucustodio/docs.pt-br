---
description: 'Saiba mais sobre o método: ICorDebugAssembly:: GetName'
title: Método ICorDebugAssembly::GetName
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly::GetName
helpviewer_keywords:
- ICorDebugAssembly::GetName method [.NET Framework debugging]
- GetName method, ICorDebugAssembly interface [.NET Framework debugging]
ms.assetid: cdeda721-b214-4503-a291-c70b68b5f36b
topic_type:
- apiref
ms.openlocfilehash: c2ffa910eaf97c5539a33dbcd3486b7dfb117b51
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711980"
---
# <a name="icordebugassemblygetname-method"></a>Método ICorDebugAssembly::GetName

Obtém o nome do assembly que esta `ICorDebugAssembly` instância representa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetName (  
    [in] ULONG32  cchName,  
    [out] ULONG32 *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)] WCHAR szName[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O tamanho da `szName` matriz.  
  
 `pcchName`  
 fora Um ponteiro para um inteiro que especifica o comprimento real do nome.  
  
 `szName`  
 fora Uma matriz que armazena o nome.  
  
## <a name="remarks"></a>Comentários  

 O `GetName` método retorna o caminho completo e o nome do arquivo do assembly.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
