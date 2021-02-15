---
description: 'Saiba mais sobre: Interface ICLRControl'
title: Interface ICLRControl
ms.date: 03/30/2017
api_name:
- ICLRControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRControl
helpviewer_keywords:
- ICLRControl interface [.NET Framework hosting]
ms.assetid: a24fd905-1fa6-45a0-ad65-e9e2ee58861e
topic_type:
- apiref
ms.openlocfilehash: e108506d06b746d631f4c15c37d467399de30aba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637658"
---
# <a name="iclrcontrol-interface"></a>Interface ICLRControl

Fornece métodos que permitem que um host obtenha referências e configure aspectos do, o Common Language Runtime (CLR).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetCLRManager](iclrcontrol-getclrmanager-method.md)|Obtém um ponteiro de interface para uma instância de qualquer um dos tipos de Gerenciador que o host pode usar para configurar o CLR.|  
|[Método SetAppDomainManagerType](iclrcontrol-setappdomainmanagertype-method.md)|Define um tipo derivado de <xref:System.AppDomainManager> como o tipo para gerenciadores de domínio de aplicativo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRDebugManager](iclrdebugmanager-interface.md)
- [Interface ICLRGCManager](iclrgcmanager-interface.md)
- [Interface ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md)
- [Interface ICLRHostProtectionManager](iclrhostprotectionmanager-interface.md)
- [Interface ICLROnEventManager](iclroneventmanager-interface.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Interface IHostControl](ihostcontrol-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
