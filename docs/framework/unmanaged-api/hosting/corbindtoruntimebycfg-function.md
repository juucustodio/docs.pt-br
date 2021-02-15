---
description: 'Saiba mais sobre: Função CorBindToRuntimeByCfg'
title: Função CorBindToRuntimeByCfg
ms.date: 03/30/2017
api_name:
- CorBindToRuntimeByCfg
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntimeByCfg
helpviewer_keywords:
- CorBindToRuntimeByCfg function [.NET Framework hosting]
ms.assetid: ded1e492-a782-4185-9c66-709e421c1782
topic_type:
- apiref
ms.openlocfilehash: c1acf6a8f1d8637bc2d6cd180016ff51cf500107
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790068"
---
# <a name="corbindtoruntimebycfg-function"></a>Função CorBindToRuntimeByCfg

Carrega o Common Language Runtime (CLR) em um processo usando informações de versão lidas de um arquivo XML.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CorBindToRuntimeByCfg (  
    [in]  IStream     *pCfgStream,  
    [in]  DWORD        reserved,  
    [in]  DWORD        startupFlags,  
    [in]  REFCLSID     rclsid,  
    [in]  REFIID       riid,
    [out] LPVOID FAR*  ppv  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pCfgStream`  
 no Um ponteiro para um `IStream` objeto que lê o arquivo XML.  
  
 `reserved`  
 no Reservado para uso futuro. Use 0 (zero) como valor.  
  
 `startupFlags`  
 no Um valor da enumeração de [STARTUP_FLAGS](startup-flags-enumeration.md) que especifica o comportamento de inicialização do CLR.  
  
 `rclsid`  
 no O `CLSID` da coclass que implementa a interface [ICorRuntimeHost](icorruntimehost-interface.md) ou [ICLRRuntimeHost](iclrruntimehost-interface.md) . Os valores com suporte são CLSID_CorRuntimeHost ou CLSID_CLRRuntimeHost.  
  
 `riid`  
 no O `IID` de ou a `ICorRuntimeHost` `ICLRRuntimeHost` interface. Os valores com suporte são IID_ICorRuntimeHost ou IID_ICLRRuntimeHost.  
  
 `ppv`  
 fora Um ponteiro para o endereço da interface retornada.  
  
## <a name="remarks"></a>Comentários  

 O formato do arquivo XML é modelado após o arquivo de configuração de aplicativo padrão. Para obter mais informações sobre arquivos XML, consulte [esquema do arquivo de configuração](../../configure-apps/file-schema/index.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função CorBindToCurrentRuntime](corbindtocurrentruntime-function.md)
- [Função CorBindToRuntime](corbindtoruntime-function.md)
- [Função CorBindToRuntimeEx](corbindtoruntimeex-function.md)
- [Função CorBindToRuntimeHost](corbindtoruntimehost-function.md)
- [Interface ICorRuntimeHost](icorruntimehost-interface.md)
- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
