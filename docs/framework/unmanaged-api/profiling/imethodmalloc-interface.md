---
description: 'Saiba mais sobre: interface IMethodMalloc'
title: Interface IMethodMalloc
ms.date: 03/30/2017
api_name:
- IMethodMalloc
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- IMethodMalloc
helpviewer_keywords:
- IMethodMalloc interface [.NET Framework profiling]
ms.assetid: 8c8ab5dc-557c-473a-82f2-6e403eca7dac
topic_type:
- apiref
ms.openlocfilehash: 6b84ac0ddb49718d24b2cad174613bc311dc509b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736942"
---
# <a name="imethodmalloc-interface"></a>Interface IMethodMalloc

Fornece um método para alocar memória para um novo corpo de função da MSIL (Microsoft Intermediate Language).  
  
> [!NOTE]
> A `IMethodMalloc` interface é um alocador de memória simples. Ele permite que você aloque memória, mas não a libere.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Alloc](imethodmalloc-alloc-method.md)|Tenta alocar uma quantidade especificada de memória para um novo corpo de função MSIL.|  
  
## <a name="remarks"></a>Comentários  

 Cada alocador é específico do módulo e garante que o corpo da função estará em um deslocamento positivo da base do módulo. A memória acima da base de um módulo pode ser preciosa, portanto, o alocador deve ser usado para alocar memória apenas para um corpo de função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criação de perfil de interfaces](profiling-interfaces.md)
