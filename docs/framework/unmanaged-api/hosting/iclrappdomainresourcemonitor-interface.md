---
description: 'Saiba mais sobre: interface ICLRAppDomainResourceMonitor'
title: Interface ICLRAppDomainResourceMonitor
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor
helpviewer_keywords:
- ICLRAppDomainResourceMonitor interface [.NET Framework hosting]
ms.assetid: 72fa83a1-8997-41d7-b355-ab177a24a303
topic_type:
- apiref
ms.openlocfilehash: 85321eabedb6912efabe57553732f8c6a4063155
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753894"
---
# <a name="iclrappdomainresourcemonitor-interface"></a>Interface ICLRAppDomainResourceMonitor

Fornece métodos que inspecionam o uso de memória e CPU de um domínio de aplicativo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetCurrentAllocated](iclrappdomainresourcemonitor-getcurrentallocated-method.md)|Obtém o tamanho total, em bytes, de todas as alocações de memória que foram feitas pelo domínio do aplicativo desde que ele foi criado, sem subtrair a memória que foi coletada por lixo.|  
|[Método GetCurrentSurvived](iclrappdomainresourcemonitor-getcurrentsurvived-method.md)|Obtém o número de bytes que sobreviveram o último total, bloqueando a coleta de lixo e que são referenciados pelo domínio do aplicativo atual.|  
|[Método GetCurrentCpuTime](iclrappdomainresourcemonitor-getcurrentcputime-method.md)|Obtém o tempo total do processador que foi usado por todos os threads durante a execução no domínio do aplicativo atual, desde que o domínio do aplicativo foi criado.|  
  
## <a name="remarks"></a>Comentários  

 A `ICLRAppDomainResourceMonitor` interface fornece funcionalidade semelhante às seguintes propriedades gerenciadas:  
  
- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType>  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [\<appDomainResourceMonitoring> Elementos](../../configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)
- [Monitoramento de recursos de domínio do aplicativo](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
