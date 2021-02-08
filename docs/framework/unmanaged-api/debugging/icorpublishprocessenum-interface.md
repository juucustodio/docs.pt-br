---
description: 'Saiba mais sobre: interface ICorPublishProcessEnum'
title: Interface ICorPublishProcessEnum
ms.date: 03/30/2017
api_name:
- ICorPublishProcessEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcessEnum
helpviewer_keywords:
- ICorPublishProcessEnum interface [.NET Framework debugging]
ms.assetid: aac8fcf9-ac09-437c-bd5c-2fda14ae1007
topic_type:
- apiref
ms.openlocfilehash: 87d80d066995dbeca67f461e01652dd3deb3bf1b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790484"
---
# <a name="icorpublishprocessenum-interface"></a>Interface ICorPublishProcessEnum

Uma subclasse da interface [ICorPublishEnum](icorpublishenum-interface.md) que fornece métodos para atravessar uma coleção de objetos [ICorPublishProcess](icorpublishprocess-interface.md) .  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icorpublishprocessenum-next-method.md)|Obtém o número especificado de `ICorPublishProcess` instâncias da coleção, começando na posição atual.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorPublishProcessEnum` interface implementa os métodos da interface abstrata, [ICorPublishEnum](icorpublishenum-interface.md).  
  
 Uma `ICorPublishProcessEnum` instância é criada pelo método [ICorPublish:: EnumProcesses](icorpublish-enumprocesses-method.md) . A passagem da coleção de `ICorPublishProcess` objetos é baseada nos critérios de filtro fornecidos no momento em que a `ICorPublishProcessEnum` instância foi criada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Coclass CorpubPublish](corpubpublish-coclass.md)
