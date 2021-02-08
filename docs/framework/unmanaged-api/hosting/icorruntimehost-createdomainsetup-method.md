---
description: 'Saiba mais sobre o método: ICorRuntimeHost:: CreateDomainSetup'
title: Método ICorRuntimeHost::CreateDomainSetup
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateDomainSetup
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateDomainSetup
helpviewer_keywords:
- CreateDomainSetup method [.NET Framework hosting]
- ICorRuntimeHost::CreateDomainSetup method [.NET Framework hosting]
ms.assetid: c21dab60-fb65-47d9-8a94-7fd47ca53b48
topic_type:
- apiref
ms.openlocfilehash: b7c2dc55fa9f0d3d5a5c18e38c2c825048ae5f53
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789678"
---
# <a name="icorruntimehostcreatedomainsetup-method"></a>Método ICorRuntimeHost::CreateDomainSetup

Obtém um ponteiro de interface do tipo IAppDomainSetup para uma <xref:System.AppDomainSetup?displayProperty=nameWithType> instância. `IAppDomainSetup` fornece métodos para configurar aspectos de um domínio de aplicativo antes de sua criação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateDomainSetup (  
    [out] IUnknown** pAppDomainSetup  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAppDomainSetup`  
 fora Um ponteiro de interface para uma <xref:System.AppDomainSetup?displayProperty=nameWithType> instância. Esse parâmetro é digitado como `IUnknown` , de modo que os chamadores geralmente devem chamar `QueryInterface` esse ponteiro para obter um ponteiro de interface do tipo `IAppDomainSetup` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A operação foi bem-sucedida.|  
|S_FALSE|Falha ao concluir a operação.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o Common Language Runtime (CLR) não poderá mais ser usado no processo. As chamadas subsequentes para qualquer API de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
  
## <a name="remarks"></a>Comentários  

 O ponteiro retornado desse método normalmente é passado como um parâmetro para o método [CreateDomainEx](icorruntimehost-createdomainex-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **Versão do .NET Framework:** 1,0, 1,1  
  
## <a name="see-also"></a>Consulte também

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- <xref:System.AppDomainSetup>
- <xref:System.IAppDomainSetup?displayProperty=nameWithType>
- [Interface ICorRuntimeHost](icorruntimehost-interface.md)
