---
description: 'Saiba mais sobre: interface ICorProfilerObjectEnum'
title: Interface ICorProfilerObjectEnum
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum
helpviewer_keywords:
- ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: 13e1651c-9523-40ef-bfd7-87fb94519f8b
topic_type:
- apiref
ms.openlocfilehash: a41900c104818566704af0070a8cd3c6cf1bba8a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781357"
---
# <a name="icorprofilerobjectenum-interface"></a>Interface ICorProfilerObjectEnum

Fornece métodos para iterar em sequência por meio de uma coleção de objetos congelados que são gerados pelo [Ngen.exe (gerador de imagem nativa)](../../tools/ngen-exe-native-image-generator.md).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Clone](icorprofilerobjectenum-clone-method.md)|Obtém um ponteiro de interface para uma cópia desta `ICorProfilerObjectEnum` interface.|  
|[Método GetCount](icorprofilerobjectenum-getcount-method.md)|Obtém o número total de objetos congelados na coleção.|  
|[Método Next](icorprofilerobjectenum-next-method.md)|Obtém o número especificado de objetos contíguos de uma coleção sequencial de objetos, começando na posição atual do enumerador na sequência.|  
|[Método Reset](icorprofilerobjectenum-reset-method.md)|Move o cursor deste enumerador para a posição inicial da sequência.|  
|[Método Skip](icorprofilerobjectenum-skip-method.md)|Avança o cursor deste enumerador de sua posição atual para que o número especificado de elementos seja ignorado.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorProfilerObjectEnum` interface é um enumerador. Ele permite que o destinatário de uma matriz Extraia elementos do remetente a uma taxa apropriada para o destinatário. Em outras palavras, o receptor é capaz de controlar explicitamente o fluxo de elementos de matriz, evitando assim os problemas relacionados à passagem de matrizes grandes como parâmetros de método.  
  
 Use [ICorProfilerInfo2:: EnumModuleFrozenObjects](icorprofilerinfo2-enummodulefrozenobjects-method.md) para obter um ponteiro para a `ICorProfilerObjectEnum` interface.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Método EnumModuleFrozenObjects](icorprofilerinfo2-enummodulefrozenobjects-method.md)
