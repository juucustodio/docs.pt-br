---
description: 'Saiba mais sobre o método: ICorDebugAppDomain2:: GetFunctionPointerType'
title: Método ICorDebugAppDomain2::GetFunctionPointerType
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain2.GetFunctionPointerType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType
helpviewer_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType method [.NET Framework debugging]
- GetFunctionPointerType method [.NET Framework debugging]
ms.assetid: 0aba6096-5b38-435c-a72a-86d35db4daef
topic_type:
- apiref
ms.openlocfilehash: 2b9e10295df40b8e7db82e489fe8a6d28214ff38
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772379"
---
# <a name="icordebugappdomain2getfunctionpointertype-method"></a>Método ICorDebugAppDomain2::GetFunctionPointerType

Obtém um ponteiro para uma função que tem uma determinada assinatura.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFunctionPointerType (  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType   *ppTypeArgs[],  
    [out] ICorDebugType                      **ppType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `nTypeArgs`  
 no O número de argumentos de tipo para a função.  
  
 `ppTypeArgs`  
 no Uma matriz de ponteiros, cada um dos quais aponta para um objeto ICorDebugType que representa um argumento de tipo da função. O primeiro elemento é o tipo de retorno; cada um dos outros elementos é um tipo de parâmetro.  
  
 `ppType`  
 fora Um ponteiro para o endereço de um `ICorDebugType` objeto que representa o ponteiro para a função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
