---
description: 'Saiba mais sobre: interface ICorProfilerAssemblyReferenceProvider'
title: Interface ICorProfilerAssemblyReferenceProvider
ms.date: 03/30/2017
api_name:
- ICorProfilerAssemblyReferenceProvider
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 17205116-66e1-4acc-8f01-532fb3867028
topic_type:
- apiref
ms.openlocfilehash: 0f16bad95dba46452ce5cc8ad1bbe6ca1bfeb7c8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648344"
---
# <a name="icorprofilerassemblyreferenceprovider-interface"></a>Interface ICorProfilerAssemblyReferenceProvider

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Permite que o criador de perfil informe o Common Language Runtime (CLR) de referências de assembly que o criador de perfil adicionará ao retorno de chamada [ICorProfilerCallback:: ModuleLoadFinished](icorprofilercallback-moduleloadfinished-method.md) .  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)|Informa o CLR de uma referência de assembly que o criador de perfil planeja adicionar ao retorno de chamada [ModuleLoadFinished](icorprofilercallback-moduleloadfinished-method.md) .|  
  
## <a name="remarks"></a>Comentários  

 O CLR passa o criador de perfil de um `ICorProfilerAssemblyReferenceProvider` objeto de interface no retorno de chamada [ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) . Isso permite que o criador de perfil informe o CLR de referências de assembly que o criador de perfil planeja adicionar posteriormente no [ICorProfilerCallback:: ModuleLoadFinished](icorprofilercallback-moduleloadfinished-method.md). . Isso melhora a precisão do caminhador de fechamento de referência do assembly do CLR e de seus algoritmos para determinar se os assemblies podem ser compartilhados.  
  
 Essa interface pode ser usada somente no retorno de chamada [ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) que passa esse objeto de interface para o criador de perfil.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
