---
description: 'Saiba mais sobre: interface ICLRHostProtectionManager'
title: Interface ICLRHostProtectionManager
ms.date: 03/30/2017
api_name:
- ICLRHostProtectionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostProtectionManager
helpviewer_keywords:
- ICLRHostProtectionManager interface [.NET Framework hosting]
ms.assetid: ce2770ae-23d0-45d9-8bcf-46504ac5020e
topic_type:
- apiref
ms.openlocfilehash: 60d27a8c1a24720bbfdcde52a5495425279d5ac4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689221"
---
# <a name="iclrhostprotectionmanager-interface"></a>Interface ICLRHostProtectionManager

Permite que o host bloqueie classes gerenciadas, métodos, propriedades e campos específicos da execução em código parcialmente confiável.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[SetEagerSerializeGrantSets](iclrhostprotectionmanager-seteagerserializegrantsets-method.md)|Fornece uma garantia de que certas condições raras de corrida que podem causar erros fatais de Common Language Runtime (CLR) nunca surgirão.|  
|[Método SetProtectedCategories](iclrhostprotectionmanager-setprotectedcategories-method.md)|Especifica as categorias de tipos gerenciados e membros que devem ser impedidos de serem executados em código parcialmente confiável.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EApiCategories](eapicategories-enumeration.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
