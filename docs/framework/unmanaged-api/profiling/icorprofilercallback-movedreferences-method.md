---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: MovedReferences'
title: Método ICorProfilerCallback::MovedReferences
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.MovedReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::MovedReferences
helpviewer_keywords:
- MovedReferences method [.NET Framework profiling]
- ICorProfilerCallback::MovedReferences method [.NET Framework profiling]
ms.assetid: 996c71ae-0676-4616-a085-84ebf507649d
topic_type:
- apiref
ms.openlocfilehash: da77ace52e19540e30488d3304d2822500c90391
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745184"
---
# <a name="icorprofilercallbackmovedreferences-method"></a>Método ICorProfilerCallback::MovedReferences

Chamado para relatar o novo layout de objetos no heap como resultado de uma coleta de lixo de compactação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT MovedReferences(  
    [in]  ULONG  cMovedObjectIDRanges,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID oldObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID newObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] ULONG    cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cMovedObjectIDRanges`  
 no O número de blocos de objetos contíguos que foram movidos como resultado da coleta de lixo de compactação. Ou seja, o valor de `cMovedObjectIDRanges` é o tamanho total das `oldObjectIDRangeStart` `newObjectIDRangeStart` matrizes, e `cObjectIDRangeLength` .  
  
 Os próximos três argumentos de `MovedReferences` são matrizes paralelas. Em outras palavras,,, `oldObjectIDRangeStart[i]` `newObjectIDRangeStart[i]` e `cObjectIDRangeLength[i]` todos se preocupam com um único bloco de objetos contíguos.  
  
 `oldObjectIDRangeStart`  
 no Uma matriz de `ObjectID` valores, cada um dos quais é o endereço inicial (coleta antes de lixo) de um bloco de objetos dinâmicos contíguos na memória.  
  
 `newObjectIDRangeStart`  
 no Uma matriz de `ObjectID` valores, cada um dos quais é o novo endereço inicial (coleta de lixo) de um bloco de objetos dinâmicos contíguos na memória.  
  
 `cObjectIDRangeLength`  
 no Uma matriz de inteiros, cada qual é o tamanho de um bloco de objetos contíguos na memória.  
  
 Um tamanho é especificado para cada bloco que é referenciado nas `oldObjectIDRangeStart` `newObjectIDRangeStart` matrizes e.  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]
> Esse método relata tamanhos `MAX_ULONG` para objetos que são maiores que 4 GB em plataformas de 64 bits. Para obter o tamanho dos objetos com mais de 4 GB, use o método [ICorProfilerCallback4:: MovedReferences2](icorprofilercallback4-movedreferences2-method.md) em vez disso.  
  
 Um coletor de lixo de compactação recupera a memória ocupada por objetos inativos e compacta o espaço livre. Como resultado, os objetos dinâmicos podem ser movidos dentro do heap, e `ObjectID` os valores distribuídos pelas notificações anteriores podem ser alterados.  
  
 Suponha que um `ObjectID` valor existente ( `oldObjectID` ) está dentro do seguinte intervalo:  
  
 `oldObjectIDRangeStart[i]` <= `oldObjectID` < `oldObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 Nesse caso, o deslocamento do início do intervalo até o início do objeto é o seguinte:  
  
 `oldObjectID` - `oldObjectRangeStart[i]`  
  
 Para qualquer valor `i` que esteja no seguinte intervalo:  
  
 0 <= `i` < `cMovedObjectIDRanges`  
  
 Você pode calcular o novo da `ObjectID` seguinte maneira:  
  
 `newObjectID` = `newObjectIDRangeStart[i]` + ( `oldObjectID` – `oldObjectIDRangeStart[i]` )  
  
 Nenhum dos `ObjectID` valores passados por `MovedReferences` são válidos durante o próprio retorno de chamada, pois a coleta de lixo pode estar no meio da movimentação de objetos de locais antigos para novos locais. Portanto, os criadores de perfis não devem tentar inspecionar objetos durante uma chamada `MovedReferences`. Um retorno de chamada [ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md) indica que todos os objetos foram movidos para seus novos locais e a inspeção pode ser executada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método MovedReferences2](icorprofilercallback4-movedreferences2-method.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
