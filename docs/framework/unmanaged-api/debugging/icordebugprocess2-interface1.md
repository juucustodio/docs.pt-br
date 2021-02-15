---
description: 'Saiba mais sobre: interface ICorDebugProcess2'
title: Interface ICorDebugProcess2
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2
helpviewer_keywords:
- ICorDebugProcess2 interface [.NET Framework debugging]
ms.assetid: 73332138-5fea-441f-b893-61af87d45a42
topic_type:
- apiref
ms.openlocfilehash: 47e94ee8ee4f45e365fa9efe888cb706f8bb1dfd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746588"
---
# <a name="icordebugprocess2-interface"></a>Interface ICorDebugProcess2

Uma extensão lógica da interface ICorDebugProcess, que representa um processo que executa código gerenciado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ClearUnmanagedBreakpoint](icordebugprocess2-clearunmanagedbreakpoint-method.md)|Remove um ponto de interrupção no deslocamento especificado que foi definido por uma chamada anterior para `ICorDebugProcess2::SetUnmanagedBreakpoint` .|  
|[Método GetDesiredNGENCompilerFlags](icordebugprocess2-getdesiredngencompilerflags-method.md)|Obtém os sinalizadores que devem ser definidos para o Common Language Runtime (CLR) para carregar a imagem no processo referenciado por isso `ICorDebugProcess2` .|  
|[Método GetReferenceValueFromGCHandle](icordebugprocess2-getreferencevaluefromgchandle-method.md)|Obtém um ponteiro de referência para o objeto gerenciado especificado que tem um identificador de coleta de lixo.|  
|[Método GetThreadForTaskID](icordebugprocess2-getthreadfortaskid-method.md)|Obtém o thread no qual a tarefa com o identificador especificado está em execução.|  
|[Método GetVersion](icordebugprocess2-getversion-method.md)|Obtém a versão do CLR no qual o processo que está sendo depurado está em execução.|  
|[Método SetDesiredNGENCompilerFlags](icordebugprocess2-setdesiredngencompilerflags-method.md)|Define os sinalizadores que são necessários para o compilador JIT (just-in-time) carregar uma imagem no processo que está sendo depurado.|  
|[Método SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md)|Define um ponto de interrupção não gerenciado no deslocamento da imagem nativa especificada.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
