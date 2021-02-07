---
description: 'Saiba mais sobre: interface ICorDebugFrame'
title: Interface ICorDebugFrame
ms.date: 03/30/2017
api_name:
- ICorDebugFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame
helpviewer_keywords:
- ICorDebugFrame interface [.NET Framework debugging]
ms.assetid: 0c48f764-3c64-4602-b2f4-4ffc60eb2c65
topic_type:
- apiref
ms.openlocfilehash: d0fd629672d535f89fe78c178032937443d9dfbd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692843"
---
# <a name="icordebugframe-interface"></a>Interface ICorDebugFrame

Representa um quadro na pilha atual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateStepper](icordebugframe-createstepper-method.md)|Obtém um ICorDebugStepper para executar operações de depuração relativas a isso `ICorDebugFrame` .|  
|[Método GetCallee](icordebugframe-getcallee-method.md)|Obtém um ponteiro para o `ICorDebugFrame` na cadeia atual que este quadro chamou ou retorna NULL se esse for o quadro interno na cadeia.|  
|[Método GetCaller](icordebugframe-getcaller-method.md)|Obtém um ponteiro para o `ICorDebugFrame` na cadeia atual que chamou esse quadro ou retorna NULL se esse for o quadro mais externo na cadeia.|  
|[Método GetChain](icordebugframe-getchain-method.md)|Obtém um ponteiro para o ICorDebugChain que `ICorDebugFrame` faz parte de.|  
|[Método GetCode](icordebugframe-getcode-method.md)|Obtém um ponteiro para o ICorDebugCode associado a este quadro de pilhas.|  
|[Método GetFunction](icordebugframe-getfunction-method.md)|Obtém um ponteiro para o ICorDebugFunction que contém o código associado a esse quadro de pilhas.|  
|[Método GetFunctionToken](icordebugframe-getfunctiontoken-method.md)|Obtém o token de metadados para a função que contém o código associado a esse quadro de pilha.|  
|[Método GetStackRange](icordebugframe-getstackrange-method.md)|Obtém o intervalo de endereços absolutos do quadro de pilha representado por isso `ICorDebugFrame` .|  
  
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
