---
description: 'Saiba mais sobre: função CLRCreateInstance'
title: Função CLRCreateInstance
ms.date: 03/30/2017
api_name:
- CLRCreateInstance
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- COM
f1_keywords:
- CLRCreateInstance
helpviewer_keywords:
- CLRCreateInstance function [.NET Framework hosting]
ms.assetid: 5de13327-96c6-4697-a89e-b8bf40717855
topic_type:
- apiref
ms.openlocfilehash: 3b4dd9f07444f3e7ca68af3b85a7a053fc72b772
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799933"
---
# <a name="clrcreateinstance-function"></a>Função CLRCreateInstance

Fornece uma das três interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)ou [ICLRDebugging](../debugging/iclrdebugging-interface.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CLRCreateInstance(  
    [in]  REFCLSID  clsid,  
    [in]  REFIID     riid,  
    [out] LPVOID  * ppInterface  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `clsid`  
 no Um dos três identificadores de classe: CLSID_CLRMetaHost, CLSID_CLRMetaHostPolicy ou CLSID_CLRDebugging.  
  
 `riid`  
 no Um dos três identificadores de interface (IIDs): IID_ICLRMetaHost, IID_ICLRMetaHostPolicy ou IID_ICLRDebugging.  
  
 `ppInterface`  
 fora Uma das três interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)ou [ICLRDebugging](../debugging/iclrdebugging-interface.md).  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`ppInterface` é nulo.|  
  
## <a name="remarks"></a>Comentários  

 A tabela a seguir mostra as combinações com suporte para o `clsid` e o `riid` .  
  
|`clsid`|`riid`|  
|--------------|------------|  
|CLSID_CLRMetaHost|IID_ICLRMetaHost|  
|CLSID_CLRMetaHostPolicy|IID_ICLRMetaHostPolicy|  
|CLSID_CLRDebugging|IID_ICLRDebugging|  
  
 O código a seguir mostra como usar o `CLRCreateInstance` para obter todas as três interfaces:  
  
```cpp  
#include <metahost.h>  
#pragma comment(lib, "mscoree.lib")  
  
ICLRMetaHost       *pMetaHost       = NULL;  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
ICLRDebugging      *pCLRDebugging   = NULL;  
HRESULT hr;  
hr = CLRCreateInstance(CLSID_CLRMetaHost, IID_ICLRMetaHost,  
                    (LPVOID*)&pMetaHost);  
hr = CLRCreateInstance (CLSID_CLRMetaHostPolicy, IID_ICLRMetaHostPolicy,  
                    (LPVOID*)&pMetaHostPolicy);  
hr = CLRCreateInstance (CLSID_CLRDebugging, IID_ICLRDebugging,  
                    (LPVOID*)&pCLRDebugging);  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Hospedagem](index.md)
