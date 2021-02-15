---
description: 'Saiba mais sobre: interface ICorPublishEnum'
title: Interface ICorPublishEnum
ms.date: 03/30/2017
api_name:
- ICorPublishEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishEnum
helpviewer_keywords:
- ICorPublishEnum interface [.NET Framework debugging]
ms.assetid: 76a136b5-e444-417a-8ade-f1596d597dc7
topic_type:
- apiref
ms.openlocfilehash: c0d50f67bd61eecbade0b226f2f569ac26712faf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721589"
---
# <a name="icorpublishenum-interface"></a>Interface ICorPublishEnum

Serve como a interface base abstrata para os enumeradores que são usados na publicação de informações sobre processos e domínios de aplicativo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Clone](icorpublishenum-clone-method.md)|Cria uma cópia deste objeto `ICorPublishEnum`.|  
|[Método GetCount](icorpublishenum-getcount-method.md)|Obtém o número de itens na enumeração.|  
|[Método Reset](icorpublishenum-reset-method.md)|Move o cursor de para o início da enumeração.|  
|[Método Skip](icorpublishenum-skip-method.md)|Move o cursor para a frente na enumeração pelo número especificado de itens.|  
  
## <a name="remarks"></a>Comentários  

 Os seguintes enumeradores derivam de `ICorPublishEnum` :  
  
- [ICorPublishAppDomainEnum](icorpublishappdomainenum-interface.md)  
  
- [ICorPublishProcessEnum](icorpublishprocessenum-interface.md)  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Coclass CorpubPublish](corpubpublish-coclass.md)
- [Depurando interfaces](debugging-interfaces.md)
