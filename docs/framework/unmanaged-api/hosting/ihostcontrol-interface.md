---
description: 'Saiba mais sobre: interface IHostControl'
title: Interface IHostControl
ms.date: 03/30/2017
api_name:
- IHostControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl
helpviewer_keywords:
- IHostControl interface [.NET Framework hosting]
ms.assetid: a4ae0d1f-ade9-4b0a-a122-93ed11a5e6b3
topic_type:
- apiref
ms.openlocfilehash: e7a242ed0fdaa734425bec9b48f01fe45cba5182
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789457"
---
# <a name="ihostcontrol-interface"></a>Interface IHostControl

Fornece métodos para configurar o carregamento de assemblies e para determinar a quais interfaces de hospedagem o host dá suporte.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetHostManager](ihostcontrol-gethostmanager-method.md)|Obtém um ponteiro de interface para a implementação do host da interface com o especificado `IID` .|  
|[Método SetAppDomainManager](ihostcontrol-setappdomainmanager-method.md)|Notifica o host de que um domínio de aplicativo foi criado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.AppDomainManager>
- [Interface ICLRRuntimeHost](iclrruntimehost-interface.md)
- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
