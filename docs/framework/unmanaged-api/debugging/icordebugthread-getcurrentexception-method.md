---
description: 'Saiba mais sobre: método ICorDebugThread:: GetCurrentException'
title: Método ICorDebugThread::GetCurrentException
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetCurrentException
helpviewer_keywords:
- ICorDebugThread::GetCurrentException method [.NET Framework debugging]
- GetCurrentException method [.NET Framework debugging]
ms.assetid: 331ed465-a195-4359-8584-b82c6098b29b
topic_type:
- apiref
ms.openlocfilehash: cb241995520f26ca0e35f2b9e3b3187c2a2906a2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659160"
---
# <a name="icordebugthreadgetcurrentexception-method"></a>Método ICorDebugThread::GetCurrentException

Obtém um ponteiro de interface para um objeto ICorDebugValue que representa uma exceção que está sendo lançada atualmente pelo código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCurrentException (  
    [out] ICorDebugValue **ppExceptionObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppExceptionObject`  
 fora Um ponteiro para o endereço de um `ICorDebugValue` objeto que representa a exceção que está sendo lançada atualmente pelo código gerenciado.  
  
## <a name="remarks"></a>Comentários  

 O objeto de exceção existirá a partir do momento em que a exceção é lançada até o final do `catch` bloco. Uma avaliação de função, que é executada pelos métodos ICorDebugEval, limpará o objeto de exceção na instalação e o restaurará na conclusão.  
  
 Exceções podem ser aninhadas (por exemplo, se uma exceção for lançada em um filtro ou em uma avaliação de função), portanto pode haver várias exceções pendentes em um único thread. `GetCurrentException` Retorna a exceção mais recente.  
  
 O tipo e o objeto de exceção podem ser alterados durante a vida útil da exceção. Por exemplo, após uma exceção do tipo x ser lançada, o Common Language Runtime (CLR) pode ficar sem memória e promovê-lo para uma exceção de memória insuficiente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
