---
description: 'Saiba mais sobre o método: ICLRRuntimeInfo:: SetDefaultStartupFlags'
title: Método ICLRRuntimeInfo::SetDefaultStartupFlags
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.SetDefaultStartupFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::SetDefaultStartupFlags
helpviewer_keywords:
- ICLRRuntimeInfo::SetDefaultStartupFlags method [.NET Framework hosting]
- SetDefaultStartupFlags method [.NET Framework hosting]
ms.assetid: 98ae174f-bff0-48f1-9e05-6cb63b451824
topic_type:
- apiref
ms.openlocfilehash: eb839b2ff71836adc1b3858092f7caf5787275b1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785036"
---
# <a name="iclrruntimeinfosetdefaultstartupflags-method"></a>Método ICLRRuntimeInfo::SetDefaultStartupFlags

Define os sinalizadores de inicialização e o arquivo de configuração do host que será usado para iniciar o tempo de execução. Esse método substitui o uso do `startupFlags` parâmetro nas funções [CorBindToRuntimeEx](corbindtoruntimeex-function.md) e [CorBindToRuntimeHost](corbindtoruntimehost-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetDefaultStartupFlags(  
           [in]  DWORD dwStartupFlags,  
           [in]  LPCWSTR pwzHostConfigFile);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwStartupFlags`  
 no Os sinalizadores de inicialização do host a serem definidos. Use os mesmos sinalizadores que as funções [CorBindToRuntimeEx](corbindtoruntimeex-function.md) e [CorBindToRuntimeHost](corbindtoruntimehost-function.md) .  
  
 `pwzHostConfigFile`  
 no O caminho do diretório do arquivo de configuração do host a ser definido.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna o HRESULT específico a seguir, bem como erros HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
  
## <a name="remarks"></a>Comentários  

 Um host multi-threaded deve sincronizar chamadas para esse método. Caso contrário, o thread A pode chamar o `SetStartupFlags` método depois que o thread b concluir uma chamada para `SetStartupFlags` e antes do thread b iniciar o tempo de execução.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
