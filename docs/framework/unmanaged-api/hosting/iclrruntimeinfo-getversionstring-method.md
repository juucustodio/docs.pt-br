---
description: 'Saiba mais sobre o método: ICLRRuntimeInfo:: GetVersionString'
title: Método ICLRRuntimeInfo::GetVersionString
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetVersionString
helpviewer_keywords:
- ICLRRuntimeInfo::GetVersionString method [.NET Framework hosting]
- GetVersionString method, ICLRRuntimeInfo interface [.NET Framework hosting]
ms.assetid: 98b097ef-2276-4dd9-8551-b03c972e8179
topic_type:
- apiref
ms.openlocfilehash: 1c7603f4e9bb1142c415ba9da7a05a52d2d5e776
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753868"
---
# <a name="iclrruntimeinfogetversionstring-method"></a>Método ICLRRuntimeInfo::GetVersionString

Obtém informações de versão Common Language Runtime (CLR) associadas a uma determinada interface [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) .  
  
 Esse método substitui as seguintes funções:  
  
- [GetRequestedRuntimeInfo](getrequestedruntimeinfo-function.md)  
  
- [GetRequestedRuntimeVersion](getrequestedruntimeversion-function.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetVersionString(  
    [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
    [in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzBuffer`  
 fora A versão de compilação .NET Framework no formato "v *A*. *B*[.*X*] ". *A*, *B* e *X* são números decimais que correspondem à versão principal, à versão secundária e ao número da compilação. *X* é opcional. Se *X* não estiver presente, não haverá nenhum ponto à direita.  
  
> [!NOTE]
> Esse parâmetro deve corresponder ao nome do diretório para a versão .NET Framework, pois ele aparece em C:\Windows\Microsoft.NET\Framework.  
  
 Os valores de exemplo são "v 1.0.3705", "v 1.1.4322", "v 2.0.50727" e "v 4.0. *x*", em que *x* depende do número de Build instalado. Observe que o prefixo "v" é obrigatório.  
  
 `pchBuffer`  
 [entrada, saída] Especifica o tamanho de `pwzBuffer` para evitar estouros de buffer. Se `pwzBuffer` for `null` , `pchBuffer` retorna o tamanho necessário de `pwzBuffer` para permitir a prealocação.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pwzBuffer` ou `pchBuffer` é nulo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Interfaces de hospedagem CLR adicionadas no .NET Framework 4 e 4.5](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [Hospedagem](index.md)
