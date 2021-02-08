---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback2:: FunctionRemapOpportunity'
title: Método ICorDebugManagedCallback2::FunctionRemapOpportunity
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.FunctionRemapOpportunity
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::FunctionRemapOpportunity
helpviewer_keywords:
- FunctionRemapOpportunity method [.NET Framework debugging]
- ICorDebugManagedCallback2::FunctionRemapOpportunity method [.NET Framework debugging]
ms.assetid: 0d6471bc-ad9b-4b1d-a307-c10443918863
topic_type:
- apiref
ms.openlocfilehash: 901a9432ddf17efabd96153581b816f653ff501d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790861"
---
# <a name="icordebugmanagedcallback2functionremapopportunity-method"></a>Método ICorDebugManagedCallback2::FunctionRemapOpportunity

Notifica o depurador de que a execução de código atingiu um ponto de sequência em uma versão mais antiga de uma função editada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FunctionRemapOpportunity (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFunction    *pOldFunction,  
    [in] ICorDebugFunction    *pNewFunction,  
    [in] ULONG32              oldILOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo que contém a função editada.  
  
 `pThread`  
 no Um ponteiro para um objeto ICorDebugThread que representa o thread no qual o ponto de interrupção do remapeamento foi encontrado.  
  
 `pOldFunction`  
 no Um ponteiro para um objeto ICorDebugFunction que representa a versão da função que está sendo executada no momento no thread.  
  
 `pNewFunction`  
 no Um ponteiro para um objeto ICorDebugFunction que representa a versão mais recente da função.  
  
 `oldILOffset`  
 no O deslocamento da MSIL (Microsoft Intermediate Language) do ponteiro de instrução na versão antiga da função.  
  
## <a name="remarks"></a>Comentários  

 Esse retorno de chamada dá ao depurador uma oportunidade de remapear o ponteiro de instrução para seu local apropriado na nova versão da função especificada chamando o método [ICorDebugILFrame2:: RemapFunction](icordebugilframe2-remapfunction-method.md) . Se o depurador não chamar `RemapFunction` antes de chamar o método [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) , o tempo de execução continuará a executar o código antigo e acionará outro `FunctionRemapOpportunity` retorno de chamada no próximo ponto de sequência.  
  
 Esse retorno de chamada será invocado para cada quadro que está executando uma versão mais antiga da função fornecida até que o depurador retorne S_OK.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
