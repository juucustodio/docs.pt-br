---
description: 'Saiba mais sobre o método: ICorDebugAppDomain3:: GetCachedWinRTTypesForIIDs'
title: Método ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3.GetCachedWinRTTypesForIIDs
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs method, [.NET Framework debugging]
- GetCachedWinRTTypesForIIDs method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 23682ca0-1bcf-48e6-996e-69f7ba337682
topic_type:
- apiref
ms.openlocfilehash: 76b93cdb8c465935a4aaf36090ee44f2b6253a3b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754167"
---
# <a name="icordebugappdomain3getcachedwinrttypesforiids-method"></a>Método ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs

Obtém um enumerador para tipos de Windows Runtime em cache em um domínio de aplicativo com base em seus identificadores de interface.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCachedWinRTTypesForIIDs (
    [in]  ULONG32            cReqTypes,  
    [in]  GUID                *iidsToResolve,  
    [out] ICorDebugTypeEnum   **ppTypesEnum  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cReqTypes`  
 no O número de tipos necessários.  
  
 `iidsToResolve`  
 no Um ponteiro para uma matriz que contém os identificadores de interface correspondentes às representações gerenciadas dos tipos de Windows Runtime a serem recuperados.  
  
 `ppTypesEnum`  
 fora Um ponteiro para o endereço de um objeto de interface "ICorDebugTypeEnum" que permite a enumeração das representações gerenciadas em cache dos tipos de Windows Runtime recuperados, com base nos identificadores de interface no `iidsToResolve` .  
  
## <a name="remarks"></a>Comentários  

 Se o método não conseguir recuperar informações para um identificador de interface específico, a entrada correspondente na coleção "ICorDebugTypeEnum" terá um tipo de `ELEMENT_TYPE_END` erros devido a problemas de recuperação de dados ou `ELEMENT_TYPE_VOID` para identificadores de interface desconhecidos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** Windows Runtime  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugAppDomain3](icordebugappdomain3-interface.md)
