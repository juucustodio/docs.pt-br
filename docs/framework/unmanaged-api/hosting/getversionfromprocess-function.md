---
description: 'Saiba mais sobre: função GetVersionFromProcess'
title: Função GetVersionFromProcess
ms.date: 03/30/2017
api_name:
- GetVersionFromProcess
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetVersionFromProcess
helpviewer_keywords:
- GetVersionFromProcess function [.NET Framework hosting]
ms.assetid: a9f7f824-64a1-408d-8607-91c7f19d21fe
topic_type:
- apiref
ms.openlocfilehash: ab665d2984f79baf049009690b36782528094937
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785244"
---
# <a name="getversionfromprocess-function"></a>Função GetVersionFromProcess

Obtém o número de versão do Common Language Runtime (CLR) associado ao identificador de processo especificado.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetVersionFromProcess (  
    [in]  HANDLE  hProcess,
    [out] LPWSTR  pVersion,
    [in]  DWORD   cchBuffer,
    [out] DWORD  *dwLength  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hProcess`  
 no Um identificador para um processo.  
  
 `pVersion`  
 fora Um buffer que contém a cadeia de caracteres de número de versão após a conclusão bem-sucedida do método.  
  
 `cchBuffer`  
 no O comprimento do buffer de versão.  
  
 `pdwLength`  
 fora Um ponteiro para o comprimento da cadeia de caracteres do número de versão.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro padrão de Component Object Model (COM), conforme definido no WinError. h, além dos valores a seguir.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_INVALIDARG|`pVersion` é NULL e `cchBuffer` não é nulo, ou vice-versa.<br /><br /> -ou-<br /><br /> `hProcess` Não é um identificador válido para um processo.<br /><br /> -ou-<br /><br /> O CLR não está carregado.|  
|ERROR_INSUFFICIENT_BUFFER|`cchBuffer` é nulo ou menor que o comprimento da cadeia de caracteres da versão.|  
|E_NOTIMPL|Esse método não está disponível no sistema operacional Microsoft Windows 95, Microsoft Windows 98 ou Microsoft Windows Millennium Edition.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função GetRequestedRuntimeInfo](getrequestedruntimeinfo-function.md)
- [Função GetRequestedRuntimeVersion](getrequestedruntimeversion-function.md)
- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
