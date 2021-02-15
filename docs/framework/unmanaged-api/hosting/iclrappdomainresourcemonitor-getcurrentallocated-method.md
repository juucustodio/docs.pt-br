---
description: 'Saiba mais sobre o método: ICLRAppDomainResourceMonitor:: GetCurrentAllocated'
title: Método ICLRAppDomainResourceMonitor::GetCurrentAllocated
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentAllocated
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentAllocated
helpviewer_keywords:
- GetCurrentAllocated method [.NET Framework hosting]
- ICLRAppDomainResourceMonitor::GetCurrentAllocated method [.NET Framework hosting]
ms.assetid: 7bab209c-efd4-44c2-af30-61abab0ae2fc
topic_type:
- apiref
ms.openlocfilehash: d7aaf31f775a9d6e2af95cf1a832c78587a85fe1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753946"
---
# <a name="iclrappdomainresourcemonitorgetcurrentallocated-method"></a>Método ICLRAppDomainResourceMonitor::GetCurrentAllocated

Obtém o tamanho total, em bytes, de todas as alocações de memória que foram feitas pelo domínio do aplicativo desde que ele foi criado, sem subtrair a memória que foi coletada por lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCurrentAllocated([in]  DWORD dwAppDomainId,  
                            [out] ULONGLONG* pBytesAllocated);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwAppDomainId`  
 no A ID do domínio do aplicativo solicitado.  
  
 `pBytesAllocated`  
 fora Um ponteiro para o tamanho total de todas as alocações de memória.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|COR_E_APPDOMAINUNLOADED|O domínio do aplicativo foi descarregado ou não existe.|  
  
## <a name="remarks"></a>Comentários  

 Esse método é o equivalente não gerenciado da propriedade gerenciada <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType> .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAppDomainResourceMonitor](iclrappdomainresourcemonitor-interface.md)
- [Monitoramento de recursos de domínio do aplicativo](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
