---
description: 'Saiba mais sobre: interface ICorDebugModule2'
title: Interface ICorDebugModule2
ms.date: 03/30/2017
api_name:
- ICorDebugModule2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2
helpviewer_keywords:
- ICorDebugModule2 interface [.NET Framework debugging]
ms.assetid: 0847e64f-fdbe-4c96-8168-da20fdc84d80
topic_type:
- apiref
ms.openlocfilehash: 28de1f0d3411218ac92991d4fceda0612c8199bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659927"
---
# <a name="icordebugmodule2-interface"></a>Interface ICorDebugModule2

Serve como uma extensão lógica para a interface ICorDebugModule.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ApplyChanges](icordebugmodule2-applychanges-method.md)|Aplica as alterações nos metadados e as alterações no código MSIL (Microsoft Intermediate Language) para o processo em execução.|  
|[Método GetJITCompilerFlags](icordebugmodule2-getjitcompilerflags-method.md)|Obtém os sinalizadores que controlam a compilação JIT (just-in-time) para isso `ICorDebugModule2` .|  
|[Método ResolveAssembly](icordebugmodule2-resolveassembly-method.md)|Resolve o assembly referenciado pelo token de metadados especificado.|  
|[Método SetJITCompilerFlags](icordebugmodule2-setjitcompilerflags-method.md)|Define os sinalizadores que controlam a compilação JIT para isso `ICorDebugModule2` .|  
|[Método SetJMCStatus](icordebugmodule2-setjmcstatus-method.md)|Define o status de Apenas Meu Código (JMC) de todos os métodos de todas as classes neste `ICorDebugModule2` para o valor especificado, exceto aqueles na `pTokens` matriz, que ele define para o valor oposto.|  
  
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
