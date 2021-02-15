---
description: 'Saiba mais sobre: interface ICorProfilerInfo9'
title: Interface ICorProfilerInfo9
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 954cb16d2b789359693f6a8fa3e0f6e19ad19b3e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736902"
---
# <a name="icorprofilerinfo9-interface"></a>Interface ICorProfilerInfo9

Uma subclasse de [ICorProfilerInfo8](icorprofilerinfo8-interface.md) que fornece métodos para consultar informações sobre funções com várias versões de código nativo.  

## <a name="methods"></a>Métodos  

| Método|Descrição|  
| ------------|-----------------|  
|[Método GetNativeCodeStartAddresses](icorprofilerinfo9-getnativecodestartaddresses-method.md)| Dada uma FunctionID e rejitId, enumera o endereço inicial do código de início de todas as versões com compilação JIT desse código que existem atualmente. |
|[Método GetILToNativeMapping3](icorprofilerinfo9-getiltonativemapping3-method.md)| Dado o endereço de início do código nativo, retorna as informações de mapeamento nativo para IL para essa versão JIT do código. |
|[Método GetCodeInfo4](icorprofilerinfo9-getcodeinfo4-method.md)| Dado o endereço de início do código nativo, retorna os blocos de memória virtual que armazenam esse código. |

## <a name="requirements"></a>Requisitos  

**Plataformas:** Consulte [sistemas operacionais com suporte do .NET Core](../../../core/install/windows.md?pivots=os-windows).  
**Cabeçalho:** CorProf. idl, CorProf. h  
**Versões do .net:**[!INCLUDE[net_core](../../../../includes/net-core-22-md.md)]  

## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
