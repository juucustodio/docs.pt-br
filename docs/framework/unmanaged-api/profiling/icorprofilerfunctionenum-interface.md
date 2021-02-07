---
description: 'Saiba mais sobre: interface ICorProfilerFunctionEnum'
title: Interface ICorProfilerFunctionEnum
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum
helpviewer_keywords:
- ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 0a1d4a38-cd0b-4231-91df-13646218ae72
topic_type:
- apiref
ms.openlocfilehash: 0a9437ee1f5c481c2c2d1fd46361da6e938dd179
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737591"
---
# <a name="icorprofilerfunctionenum-interface"></a>Interface ICorProfilerFunctionEnum

Fornece métodos para iterar em sequência por meio de uma coleção de funções no Common Language Runtime.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Clone](icorprofilerfunctionenum-clone-method.md)|Obtém um ponteiro de interface para uma cópia desta `ICorProfilerFunctionEnum` interface.|  
|[Método GetCount](icorprofilerfunctionenum-getcount-method.md)|Obtém o número de funções que foram carregadas pelo aplicativo ou carregadas de modo forçado pelo criador de perfil.|  
|[Método Next](icorprofilerfunctionenum-next-method.md)|Obtém o número especificado de funções contíguas de uma coleção sequencial de funções, começando na posição atual do enumerador na sequência.|  
|[Método Reset](icorprofilerfunctionenum-reset-method.md)|Move o cursor do enumerador para a posição inicial da sequência.|  
|[Método Skip](icorprofilerfunctionenum-skip-method.md)|Avança o cursor do enumerador de sua posição atual para que o número especificado de elementos seja ignorado.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorProfilerFunctionEnum` interface é um enumerador. Ele permite que o destinatário de uma matriz Extraia elementos do remetente a uma taxa apropriada para o destinatário. Em outras palavras, o receptor é capaz de controlar explicitamente o fluxo de elementos de matriz, evitando, assim, os problemas associados à passagem de matrizes grandes como parâmetros de método.  
  
 `ICorProfilerFunctionEnum` enumera em funções que já foram compiladas por JIT, mas não inclui funções que são carregadas de imagens nativas geradas com Ngen.exe.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Método EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md)
