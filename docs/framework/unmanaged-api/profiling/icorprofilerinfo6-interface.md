---
description: 'Saiba mais sobre: interface ICorProfilerInfo6'
title: Interface ICorProfilerInfo6
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo6
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 6f2bb148-1e2b-4e45-a5a5-0ceddc40064b
ms.openlocfilehash: c093930b102ca99a8524e6d5d6129690f80a5353
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737149"
---
# <a name="icorprofilerinfo6-interface"></a>Interface ICorProfilerInfo6

[Com suporte no .NET Framework 4,6 e versões posteriores]  
  
 Uma subclasse de [ICorProfilerInfo5](icorprofilerinfo5-interface.md) que fornece um enumerador para todos os métodos que são definidos em um determinado módulo NGen e embutidos em um determinado método.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod](icorprofilerinfo6-enumngenmodulemethodsinliningthismethod-method.md)|Retorna um enumerador para todos os métodos que pertencem a um determinado módulo NGen e que são embutidos no corpo de um determinado método.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
