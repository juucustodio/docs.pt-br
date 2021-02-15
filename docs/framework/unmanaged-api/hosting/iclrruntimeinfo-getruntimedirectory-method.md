---
description: 'Saiba mais sobre o método: ICLRRuntimeInfo:: GetRuntimeDirectory'
title: Método ICLRRuntimeInfo::GetRuntimeDirectory
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetRuntimeDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetRuntimeDirectory
helpviewer_keywords:
- GetRuntimeDirectory method [.NET Framework hosting]
- ICLRRuntimeInfo::GetRuntimeDirectory method [.NET Framework hosting]
ms.assetid: 4401546e-4d48-453f-a1fb-b2ebda54df5c
topic_type:
- apiref
ms.openlocfilehash: 1e833887568d0a61e9ff9ec358b6979a4bacce41
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637086"
---
# <a name="iclrruntimeinfogetruntimedirectory-method"></a>Método ICLRRuntimeInfo::GetRuntimeDirectory

Obtém o diretório de instalação do Common Language Runtime (CLR) associado a essa interface.  
  
 Esse método substitui a função [GetCORSystemDirectory](getcorsystemdirectory-function.md) fornecida no .NET Framework versões 2,0, 3,0 e 3,5.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRuntimeDirectory(  
[out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
[in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzBuffer`  
 fora Retorna o diretório de instalação do CLR. O caminho de instalação é totalmente qualificado; por exemplo, "c:\Windows\Microsoft.NET\Framework\v1.0.3705 \\ ".  
  
 `pchBuffer`  
 [entrada, saída] Especifica o tamanho de `pwzBuffer` para evitar estouros de buffer. Se `pwzBuffer` for NULL, `pchBuffer` retornará o tamanho necessário de `pwzBuffer` .  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pwzBuffer` ou `pchBuffer` é nulo.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Hospedagem](index.md)
