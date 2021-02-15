---
description: 'Saiba mais sobre o método: ICorRuntimeHost:: CreateDomainEx'
title: Método ICorRuntimeHost::CreateDomainEx
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateDomainEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateDomainEx
helpviewer_keywords:
- ICorRuntimeHost::CreateDomainEx method [.NET Framework hosting]
- CreateDomainEx method [.NET Framework hosting]
ms.assetid: 1bdde382-f8ba-4cc8-94b2-d1ac919c585e
topic_type:
- apiref
ms.openlocfilehash: aec759cec4fd68fff4bdfaaf3403a0da026fb9ee
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789691"
---
# <a name="icorruntimehostcreatedomainex-method"></a>Método ICorRuntimeHost::CreateDomainEx

Cria um domínio de aplicativo. O chamador recebe um ponteiro de interface, do tipo <xref:System._AppDomain> , para uma instância do tipo <xref:System.AppDomain?displayProperty=nameWithType> . Esse método permite que o chamador passe uma instância de IAppDomainSetup para configurar recursos adicionais da <xref:System._AppDomain> instância retornada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateDomainEx (  
    [in] LPCWSTR     pwzFriendlyName,  
    [in] IUnknown*   pSetup,  
    [in] IUnknown*   pIdentityArray,  
    [out] IUnknown** pAppDomain  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzFriendlyName`  
 no Um parâmetro opcional usado para fornecer um nome amigável ao domínio. Esse nome amigável pode ser exibido em interfaces do usuário, como depuradores, para identificar o domínio.  
  
 `pSetup`  
 no Um ponteiro de interface opcional do tipo `IAppDomainSetup` , obtido por uma chamada para o método [ICorRuntimeHost:: CreateDomainSetup](icorruntimehost-createdomainsetup-method.md) .  
  
 `pIdentityArray`  
 no Uma matriz opcional de ponteiros para `IIdentity` instâncias que representam evidências mapeadas pela política de segurança para estabelecer um conjunto de permissões. Um `IIdentity` objeto pode ser obtido chamando o método [CreateEvidence](icorruntimehost-createevidence-method.md) .  
  
 `pAppDomain`  
 fora Um ponteiro de interface do tipo <xref:System._AppDomain> para uma instância do <xref:System.AppDomain?displayProperty=nameWithType> que pode ser usado para controlar ainda mais o domínio.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A operação foi bem-sucedida.|  
|S_FALSE|Falha ao concluir a operação.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o Common Language Runtime (CLR) não poderá mais ser usado no processo. As chamadas subsequentes para qualquer API de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
  
## <a name="remarks"></a>Comentários  

 `CreateDomainEx` estende os recursos do [CreateDomain](icorruntimehost-createdomain-method.md) permitindo que o chamador passe em uma `IAppDomainSetup` instância com valores de propriedade para configurar o domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **Versão do .NET Framework:** 1,0, 1,1  
  
## <a name="see-also"></a>Consulte também

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- <xref:System.IAppDomainSetup?displayProperty=nameWithType>
- [Método CreateDomain](icorruntimehost-createdomain-method.md)
- [Interface ICorRuntimeHost](icorruntimehost-interface.md)
