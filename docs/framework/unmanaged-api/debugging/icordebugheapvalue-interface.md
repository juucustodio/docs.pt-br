---
description: 'Saiba mais sobre: interface ICorDebugHeapValue'
title: Interface ICorDebugHeapValue
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue
helpviewer_keywords:
- ICorDebugHeapValue interface [.NET Framework debugging]
ms.assetid: 1bca66db-0359-4ae8-846e-e35f7e547e8b
topic_type:
- apiref
ms.openlocfilehash: 7c65cbce530f0d1f00d8610031fb604a0118ee29
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803666"
---
# <a name="icordebugheapvalue-interface"></a>Interface ICorDebugHeapValue

Uma subclasse de "ICorDebugValue" que representa um objeto que foi coletado pelo coletor de lixo Common Language Runtime (CLR).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateRelocBreakpoint](icordebugheapvalue-createrelocbreakpoint-method.md)|Não implementado.|  
|[Método IsValid](icordebugheapvalue-isvalid-method.md)|Obtém um valor que indica se o objeto representado por ele `ICorDebugHeapValue` é válido ou se foi recuperado pelo coletor de lixo. Esse método foi preterido no .NET Framework versão 2,0.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
