---
description: 'Saiba mais sobre: interface ICorDebugMDA'
title: Interface ICorDebugMDA
ms.date: 03/30/2017
api_name:
- ICorDebugMDA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA
helpviewer_keywords:
- ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 8ecbb854-295c-4dd4-b9fc-01ebeac46e06
topic_type:
- apiref
ms.openlocfilehash: 8e6e779c58d71b07edc9b63dff72aef728ebe050
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801118"
---
# <a name="icordebugmda-interface"></a>Interface ICorDebugMDA

Representa uma mensagem do assistente de depuração gerenciado (MDA).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetDescription](icordebugmda-getdescription-method.md)|Obtém uma cadeia de caracteres que contém uma descrição deste MDA.|  
|[Método GetFlags](icordebugmda-getflags-method.md)|Obtém os sinalizadores associados a este MDA.|  
|[Método GetName](icordebugmda-getname-method.md)|Obtém uma cadeia de caracteres que contém o nome deste MDA.|  
|[Método GetOSThreadId](icordebugmda-getosthreadid-method.md)|Obtém o identificador de thread do sistema operacional no qual este MDA está sendo executado.|  
|[Método GetXML](icordebugmda-getxml-method.md)|Obtém o fluxo XML completo associado a este MDA.|  
  
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
- [Diagnosticando erros com assistentes de depuração gerenciados](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
