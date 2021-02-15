---
description: 'Saiba mais sobre: interface ICorProfilerInfo8'
title: Interface ICorProfilerInfo8
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 4538c9d314283c67ab0bfe6af3f3768062cffda4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646537"
---
# <a name="icorprofilerinfo8-interface"></a>Interface ICorProfilerInfo8

Uma subclasse de [ICorProfilerInfo7](icorprofilerinfo7-interface.md) que fornece métodos para consultar informações sobre métodos dinâmicos.

## <a name="methods"></a>Métodos  

| Método|Descrição|  
| ------------|-----------------|  
|[Método IsFunctionDynamic](icorprofilerinfo8-isfunctiondynamic-method.md)| Determina se uma função não tem metadados associados.|
|[Método GetFunctionFromIP3](icorprofilerinfo8-getfunctionfromip3-method.md)| Mapeia um ponteiro de instrução de código gerenciado para uma FunctionID. Esse método funciona para métodos dinâmicos e não dinâmicos. |
|[Método GetDynamicFunctionInfo](icorprofilerinfo8-getdynamicfunctioninfo-method.md)| Recupera informações sobre métodos dinâmicos. |

## <a name="requirements"></a>Requisitos  

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
**Cabeçalho:** CorProf. idl, CorProf. h  
**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  

## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
