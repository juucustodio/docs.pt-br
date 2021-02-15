---
description: 'Saiba mais sobre: interface ICorProfilerInfo10'
title: Interface ICorProfilerInfo10
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: fd24491cb1ca55ad48137522c63e78e6387d33e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753283"
---
# <a name="icorprofilerinfo10-interface"></a>Interface ICorProfilerInfo10

Uma subclasse de [ICorProfilerInfo9](icorprofilerinfo9-interface.md) que fornece métodos para modificar o Il da função, consultar informações do tempo de execução e suspender e retomar o tempo de execução.

## <a name="methods"></a>Métodos  

| Método|Descrição|  
| ------------|-----------------|  
|[Método EnumerateObjectReferences](icorprofilerinfo10-enumerateobjectreferences-method.md)|Dado um ObjectID, retorno de chamada e clientData, enumera cada referência de objeto (se houver). |
|[Método IsFrozenObject](icorprofilerinfo10-isfrozenobject-method.md)|Dado um ObjectID, determina se o objeto está em um segmento somente leitura. |
|[Método GetLOHObjectSizeThreshold](icorprofilerinfo10-getlohobjectsizethreshold-method.md)|Obtém o valor do limite de LOH configurado. |
|[Método RequestReJITWithInliners](icorprofilerinfo10-requestrejitwithinliners-method.md)| ReJITs os métodos solicitados, bem como quaisquer inlineers dos métodos solicitados.  |
|[Método SuspendRuntime](icorprofilerinfo10-suspendruntime-method.md)| Suspende o tempo de execução sem executar um GC. |
|[Método ResumeRuntime](icorprofilerinfo10-resumeruntime-method.md)| Retoma o tempo de execução sem executar um GC. |

## <a name="requirements"></a>Requisitos  

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).  
**Cabeçalho:** CorProf. idl, CorProf. h  
**Versões do .net:**[!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
