---
description: 'Saiba mais sobre: função GetRequestedRuntimeInfo'
title: Função GetRequestedRuntimeInfo
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeInfo
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeInfo
helpviewer_keywords:
- GetRequestedRuntimeInfo function [.NET Framework hosting]
ms.assetid: 0dfd7cdc-c116-4e25-b56a-ac7b0378c942
topic_type:
- apiref
ms.openlocfilehash: 63d0bdcd07be5727cddc0acc352e8358b5ff0090
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785283"
---
# <a name="getrequestedruntimeinfo-function"></a>Função GetRequestedRuntimeInfo

Obtém informações de versão e diretório sobre o Common Language Runtime (CLR) solicitado por um aplicativo.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRequestedRuntimeInfo (  
    [in]  LPCWSTR  pExe,
    [in]  LPCWSTR  pwszVersion,
    [in]  LPCWSTR  pConfigurationFile,
    [in]  DWORD    startupFlags,
    [in]  DWORD    runtimeInfoFlags,
    [out] LPWSTR   pDirectory,
    [in]  DWORD    dwDirectory,
    [out] DWORD   *dwDirectoryLength,
    [out] LPWSTR   pVersion,
    [in]  DWORD    cchBuffer,
    [out] DWORD   *dwlength  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pExe`  
 no O nome do aplicativo.  
  
 `pwszVersion`  
 no Uma cadeia de caracteres que especifica o número de versão do tempo de execução.  
  
 `pConfigurationFile`  
 no O nome do arquivo de configuração associado ao `pExe` .  
  
 `startupFlags`  
 no Um ou mais dos [STARTUP_FLAGS](startup-flags-enumeration.md) valores de enumeração.  
  
 `runtimeInfoFlags`  
 no Um ou mais dos [RUNTIME_INFO_FLAGS](runtime-info-flags-enumeration.md) valores de enumeração.  
  
 `pDirectory`  
 fora Um buffer que contém o caminho do diretório para o tempo de execução após a conclusão bem-sucedida.  
  
 `dwDirectory`  
 no O comprimento do buffer de diretório.  
  
 `dwDirectoryLength`  
 fora Um ponteiro para o comprimento da cadeia de caracteres do caminho do diretório.  
  
 `pVersion`  
 fora Um buffer que contém o número de versão do tempo de execução após a conclusão bem-sucedida.  
  
 `cchBuffer`  
 no O comprimento do buffer de cadeia de caracteres da versão.  
  
 `dwlength`  
 fora Um ponteiro para o comprimento da cadeia de caracteres da versão.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro padrão de Component Object Model (COM), conforme definido no WinError. h, além dos valores a seguir.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|ERROR_INSUFFICIENT_BUFFER|O buffer de diretório não é grande o suficiente para armazenar o caminho do diretório.<br /><br /> - ou -<br /><br /> O buffer de versão não é grande o suficiente para armazenar a cadeia de caracteres de versão.|  
  
## <a name="remarks"></a>Comentários  

 O `GetRequestedRuntimeInfo` método retorna informações de tempo de execução sobre a versão carregada no processo, que não é necessariamente a versão mais recente instalada no computador.  
  
 Na versão .NET Framework 2,0, você pode obter informações sobre a versão instalada mais recente usando o `GetRequestedRuntimeInfo` método da seguinte maneira:  
  
- Especifique os `pExe` `pwszVersion` parâmetros, e `pConfigurationFile` como NULL.  
  
- Especifique o sinalizador de RUNTIME_INFO_UPGRADE_VERSION nas `RUNTIME_INFO_FLAGS` enumerações para o `runtimeInfoFlags` parâmetro.  
  
 O `GetRequestedRuntimeInfo` método não retorna a versão mais recente do CLR nas seguintes circunstâncias:  
  
- Existe um arquivo de configuração de aplicativo que especifica o carregamento de uma versão CLR específica. Observe que o .NET Framework usará o arquivo de configuração mesmo se você especificar NULL para o `pConfigurationFile` parâmetro.  
  
- O método [CorBindToRuntimeEx](corbindtoruntimeex-function.md) foi chamado especificando uma versão anterior do CLR.  
  
- Um aplicativo que foi compilado para uma versão anterior do CLR está em execução no momento.  
  
 Para o `runtimeInfoFlags` parâmetro, você pode especificar apenas uma das constantes de arquitetura da `RUNTIME_INFO_FLAGS` enumeração de cada vez:  
  
- RUNTIME_INFO_REQUEST_IA64  
  
- RUNTIME_INFO_REQUEST_AMD64  
  
- RUNTIME_INFO_REQUEST_X86  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função GetRequestedRuntimeVersion](getrequestedruntimeversion-function.md)
- [Função GetVersionFromProcess](getversionfromprocess-function.md)
- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
