---
description: 'Saiba mais sobre o método: ICLRRuntimeHost:: ExecuteApplication'
title: Método ICLRRuntimeHost::ExecuteApplication
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteApplication
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteApplication
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteApplication method [.NET Framework hosting]
- ExecuteApplication method [.NET Framework hosting]
ms.assetid: 5f28cc4e-7176-4e00-aa1f-58ae6ee52fe4
topic_type:
- apiref
ms.openlocfilehash: 1511cc3dcf05c3f2243f4080143789e456c39167
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688969"
---
# <a name="iclrruntimehostexecuteapplication-method"></a>Método ICLRRuntimeHost::ExecuteApplication

Usado em cenários de implantação ClickOnce baseados em manifesto para especificar o aplicativo a ser ativado em um novo domínio. Para obter mais informações sobre esses cenários, consulte [segurança e implantação do ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExecuteApplication(  
    [in] LPCWSTR   pwzAppFullName,  
    [in] DWORD     dwManifestPaths,  
    [in] LPCWSTR   *ppwzManifestPaths,  
    [in] DWORD     dwActivationData,  
    [in] LPCWSTR   *ppwzActivationData,  
    [out] int      *pReturnValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzAppFullName`  
 no O nome completo do aplicativo, conforme definido para <xref:System.ApplicationIdentity> .  
  
 `dwManifestPaths`  
 no O número de cadeias de caracteres contidas na `ppwzManifestPaths` matriz.  
  
 `ppwzManifestPaths`  
 [in] Opcional. Uma matriz de cadeia de caracteres que contém caminhos de manifesto para o aplicativo.  
  
 `dwActivationData`  
 no O número de cadeias de caracteres contidas na `ppwzActivationData` matriz.  
  
 `ppwzActivationData`  
 [in] Opcional. Uma matriz de cadeia de caracteres que contém os dados de ativação do aplicativo, como a parte da cadeia de caracteres de consulta da URL para aplicativos implantados na Web.  
  
 `pReturnValue`  
 fora O valor retornado do ponto de entrada do aplicativo.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`ExecuteApplication` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o CLR não poderá mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 `ExecuteApplication` é usado para ativar aplicativos ClickOnce em um domínio de aplicativo recém-criado.  
  
 O `pReturnValue` parâmetro de saída é definido como o valor retornado pelo aplicativo. Se você fornecer um valor de NULL para `pReturnValue` , `ExecuteApplication` o não falhará, mas não retornará um valor.  
  
> [!IMPORTANT]
> Não chame o método [Start Method](iclrruntimehost-start-method.md) antes de chamar o `ExecuteApplication` método para ativar um aplicativo baseado em manifesto. Se o `Start` método for chamado primeiro, a `ExecuteApplication` chamada do método falhará.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ActivationContext>
- <xref:System.AppDomainManager>
- <xref:System.ApplicationIdentity>
- [Interface ICLRRuntimeHost](iclrruntimehost-interface.md)
- [Método SetAppDomainManager](ihostcontrol-setappdomainmanager-method.md)
- [Walkthrough: baixando assemblies sob demanda com a API de implantação do ClickOnce usando o designer](/visualstudio/deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer)
