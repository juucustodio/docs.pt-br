---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback:: LoadClass'
title: Método ICorDebugManagedCallback::LoadClass
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LoadClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LoadClass
helpviewer_keywords:
- ICorDebugManagedCallback::LoadClass method [.NET Framework debugging]
- LoadClass method [.NET Framework debugging]
ms.assetid: e58dac7b-85c3-41ca-b9aa-3a7fc9ae6680
topic_type:
- apiref
ms.openlocfilehash: 6f670a2f0798c7edfdc4292334cf9534e59a3007
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660598"
---
# <a name="icordebugmanagedcallbackloadclass-method"></a>Método ICorDebugManagedCallback::LoadClass

Notifica o depurador de que uma classe foi carregada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT LoadClass (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugClass     *c  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo no qual a classe foi carregada.  
  
 `c`  
 no Um ponteiro para um objeto ICorDebugClass que representa a classe.  
  
## <a name="remarks"></a>Comentários  

 Esse retorno de chamada ocorrerá somente se o carregamento da classe tiver sido habilitado para o módulo que contém a classe. O carregamento de classe é sempre habilitado para módulos dinâmicos.  
  
 O `LoadClass` retorno de chamada fornece um tempo apropriado para associar pontos de interrupção a classes recém-gerado em módulos dinâmicos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método UnloadClass](icordebugmanagedcallback-unloadclass-method.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
