---
description: 'Saiba mais sobre: Enumeração CorDebugCodeInvokeKind'
title: Enumeração CorDebugCodeInvokeKind
ms.date: 03/30/2017
api_name:
- CorDebugCodeInvokeKind
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: e795e6a2-1008-4a81-af88-d777888e942e
topic_type:
- apiref
ms.openlocfilehash: d3fc3fe6f7568adcb2d1bbbe18c98d9d84bac337
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747082"
---
# <a name="cordebugcodeinvokekind-enumeration"></a>Enumeração CorDebugCodeInvokeKind

Descreve como uma função exportada invoca código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorDebugCodeInvokeKind  
{  
    CODE_INVOKE_KIND_NONE,
    CODE_INVOKE_KIND_RETURN,
    CODE_INVOKE_KIND_TAILCALL,
} CorDebugCodeInvokeKind;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`CODE_INVOKE_KIND_NONE`|Se algum código gerenciado for invocado por este método, precisará ser localizadas por eventos explícitos ou pontos de interrupção posteriormente.<br /><br /> --ou--<br /><br /> Podemos perder parte do código gerenciado que este método chama porque não há nenhuma maneira fácil de pará-lo.<br /><br /> --ou--<br /><br /> O método nunca pode invocar um código gerenciado.|  
|`CODE_INVOKE_KIND_RETURN`|Esse método invocará o código gerenciado por meio de uma instrução de retorno. Sair deve dar no próximo código gerenciado.|  
|`CODE_INVOKE_KIND_TAILCALL`|Esse método invocará o código gerenciado por meio de chamada tail. Seguir uma etapa única e ignorar quaisquer instruções de chamada devem dar no código gerenciado.|  
  
## <a name="remarks"></a>Comentários  

 Essa enumeração é usada pelo método [ICorDebugProcess6:: GetExportStepInfo](icordebugprocess6-getexportstepinfo-method.md) para fornecer informações sobre como percorrer código gerenciado.  
  
> [!NOTE]
> Essa enumeração destina-se ao uso em cenários de depuração .NET Native apenas.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
- [Depuração](index.md)
