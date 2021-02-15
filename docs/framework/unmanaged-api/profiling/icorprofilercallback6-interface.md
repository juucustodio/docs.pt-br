---
description: 'Saiba mais sobre: interface ICorProfilerCallback6'
title: Interface ICorProfilerCallback6
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback6
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: edc420b7-96d1-4dec-ace0-36d907f644bc
topic_type:
- apiref
ms.openlocfilehash: 12eaafff8bd9ab8d4d58eac8f2d62415531bc898
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781747"
---
# <a name="icorprofilercallback6-interface"></a>Interface ICorProfilerCallback6

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Uma subclasse de [ICorProfilerCallback5](icorprofilercallback5-interface.md) que fornece um método de retorno de chamada que o Common Language Runtime usa para notificar um criador de perfil que um assembly está carregando.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)|Notifica o criador de perfis de que um assembly está em um estágio inicial de carregamento, quando o Common Language Runtime realiza um exame de fechamento da referência do assembly.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
