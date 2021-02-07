---
description: 'Saiba mais sobre: interface ICorDebugProcess6'
title: Interface ICorDebugProcess6
ms.date: 03/30/2017
ms.assetid: 34a10ac2-882c-4797-8369-f120e8e640c7
ms.openlocfilehash: f303670d0667a80507bc623f9af037759fdde463
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99691452"
---
# <a name="icordebugprocess6-interface"></a>Interface ICorDebugProcess6

Estende logicamente a interface ICorDebugProcess para habilitar recursos como eventos de depuração gerenciados que são codificados em eventos de depuração de exceção nativa e divisão de módulo virtual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método DecodeEvent](icordebugprocess6-decodeevent-method.md)|Decodifica eventos de depuração gerenciados que foram encapsulados na carga de eventos de depuração de exceção nativo especialmente criado.|  
|[Método EnableVirtualModuleSplitting](icordebugprocess6-enablevirtualmodulesplitting-method.md)|Habilita ou desabilita a divisão de módulo virtual.|  
|[Método GetCode](icordebugprocess6-getcode-method.md)|Obtém informações sobre o código gerenciado em um endereço de código em particular.|  
|[Método GetExportStepInfo](icordebugprocess6-getexportstepinfo-method.md)|Fornece informações sobre funções exportadas de runtime para ajudar a percorrer o código gerenciado.|  
|[Método MarkDebuggerAttached](icordebugprocess6-markdebuggerattached-method.md)|Altera o estado interno do depurado para que o método <xref:System.Diagnostics.Debugger.IsAttached%2A?displayProperty=nameWithType> na biblioteca de classes .NET Framework retorne `true`.|  
|[Método ProcessStateChanged](icordebugprocess6-processstatechanged-method.md)|Notifica o [ICorDebug](icordebug-interface.md) de que o processo está em execução.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> A interface está disponível somente com .NET Native. A tentativa de chamar `QueryInterface` para recuperar um ponteiro de interface retorna `E_NOINTERFACE` para cenários ICorDebug fora do .net Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
