---
description: 'Saiba mais sobre: ICorProfilerObjectEnum:: Next Method'
title: Método ICorProfilerObjectEnum::Next
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::Next
helpviewer_keywords:
- Next method, ICorProfilerObjectEnum interface [.NET Framework profiling]
- ICorProfilerObjectEnum::Next method [.NET Framework profiling]
ms.assetid: b420433c-5ebe-4986-bba1-97902e6db819
topic_type:
- apiref
ms.openlocfilehash: 7f61fa1d4e28043bf5eda95f67dde0d8e87d8c0d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781396"
---
# <a name="icorprofilerobjectenumnext-method"></a>Método ICorProfilerObjectEnum::Next

Obtém o número especificado de objetos contíguos de uma coleção sequencial de objetos, começando na posição atual do enumerador na sequência.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Next (  
    [in] ULONG                    celt,  
    [out, size_is(celt), length_is(*pceltFetched)]
        ObjectID                  objects[],  
    [out] ULONG                   *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de objetos a serem recuperados.  
  
 `objects`  
 fora Uma matriz de `ObjectID` valores, cada um representando um objeto recuperado.  
  
 `pceltFetched`  
 fora Um ponteiro para o número de elementos realmente retornados na `objects` matriz.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerObjectEnum](icorprofilerobjectenum-interface.md)
