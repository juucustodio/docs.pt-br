---
description: 'Saiba mais sobre: interface ICorDebugMutableDataTarget'
title: Interface ICorDebugMutableDataTarget
ms.date: 03/30/2017
ms.assetid: 14aad5b3-84ab-4bbc-94e3-1eb92e258d10
ms.openlocfilehash: 387c5317bea015459e306994c36761571b427628
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790692"
---
# <a name="icordebugmutabledatatarget-interface"></a>Interface ICorDebugMutableDataTarget

Estende a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) para dar suporte a destinos de dados mutáveis.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ContinueStatusChanged](icordebugmutabledatatarget-continuestatuschanged-method.md)|Altera o status de continuação para o evento de depuração pendente no thread especificado.|  
|[Método SetThreadContext](icordebugmutabledatatarget-setthreadcontext-method.md)|Define o contexto (valores de registro) para um thread.|  
|[Método WriteVirtual](icordebugmutabledatatarget-writevirtual-method.md)|Grava a memória no espaço de endereço do processo de destino.|  
  
## <a name="remarks"></a>Comentários  

 Essa extensão para a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) pode ser implementada por ferramentas de depuração que desejam modificar o processo de destino (por exemplo, para executar a depuração de invasor ao vivo).  
  
 Todos esses métodos são opcionais no sentido de que nenhuma funcionalidade de depuração baseada em inspeção principal é perdida não implementando essa interface ou pela falha de chamadas para esses métodos.  Qualquer falha `HRESULT` desses métodos será propagada como a `HRESULT` partir da chamada do método ICorDebug.  
  
 Observe que uma única chamada de método ICorDebug pode resultar em várias mutações e que não há nenhum mecanismo para garantir que as mutações relacionadas sejam aplicadas transacionalmente (All-ou-None).  Isso significa que, se uma mutação falhar depois que outras (para a mesma chamada ICorDebug) tiverem sido bem-sucedidas, o processo de destino poderá ser deixado em um estado inconsistente e a depuração poderá se tornar não confiável.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
