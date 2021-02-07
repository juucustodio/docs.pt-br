---
description: 'Saiba mais sobre o método: ICorDebugAppDomain:: GetObject'
title: Método ICorDebugAppDomain::GetObject
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetObject
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetObject
helpviewer_keywords:
- ICorDebugAppDomain::GetObject method [.NET Framework debugging]
- GetObject method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 78232e6f-ae18-4cfa-a6cd-e79471cf9d76
topic_type:
- apiref
ms.openlocfilehash: 59389e2a4ca72f8dcdd7117213e968440d30aaa6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754204"
---
# <a name="icordebugappdomaingetobject-method"></a>Método ICorDebugAppDomain::GetObject

Obtém um ponteiro de interface para o domínio do aplicativo Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetObject (  
    [out] ICorDebugValue   **ppObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppObject`  
 fora Um ponteiro para o endereço de um objeto de interface ICorDebugValue que representa o domínio do aplicativo CLR.  
  
## <a name="return-value"></a>Valor retornado  

 Se um objeto gerenciado não <xref:System.AppDomain?displayProperty=nameWithType> tiver sido construído para esse domínio de aplicativo, o método retornará `S_FALSE` e colocará `NULL` em `*ppObject` .  
  
## <a name="remarks"></a>Comentários  

 Cada domínio de aplicativo em um processo pode ter um <xref:System.AppDomain?displayProperty=nameWithType> objeto gerenciado no tempo de execução que o representa. Essa função obtém um objeto de interface ICorDebugValue que corresponde a esse <xref:System.AppDomain?displayProperty=nameWithType> objeto gerenciado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]
