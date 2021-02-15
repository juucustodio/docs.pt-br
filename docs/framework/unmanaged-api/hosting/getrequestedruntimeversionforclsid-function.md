---
description: 'Saiba mais sobre: função GetRequestedRuntimeVersionForCLSID'
title: Função GetRequestedRuntimeVersionForCLSID
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeVersionForCLSID
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeVersionForCLSID
helpviewer_keywords:
- GetRequestedRuntimeVersionForCLSID function [.NET Framework hosting]
ms.assetid: 5bb12f9a-0612-434b-b4ed-2db636a20bec
topic_type:
- apiref
ms.openlocfilehash: 10fdc947181d3f1fa12b33f11cf31b68fc4285cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785257"
---
# <a name="getrequestedruntimeversionforclsid-function"></a>Função GetRequestedRuntimeVersionForCLSID

Obtém as informações de versão do Common Language Runtime (CLR) apropriadas para a classe com o especificado `CLSID` .  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRequestedRuntimeVersionForCLSID (  
    [in]  REFCLSID   rclsid,
    [out]  LPWSTR     pVersion,
    [in]  DWORD      cchBuffer,
    [out] DWORD*     dwLength,
    [in]  CLSID_RESOLUTION_FLAGS dwResolutionFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `rclsid`  
 no  O `CLSID` do componente.  
  
 `pVersion`  
 fora  Um buffer que contém a cadeia de caracteres de número de versão após a conclusão bem-sucedida.  
  
 `cchBuffer`  
 no  O tamanho, em caracteres largos, do `pVersion` buffer.  
  
 `dwLength`  
 fora O comprimento, em bytes, do buffer retornado.  
  
 `dwResolutionFlags`  
 no  Um dos valores de CLSID_RESOLUTION_FLAGS. Os seguintes valores têm suporte:  
  
- CLSID_RESOLUTION_DEFAULT: (0x0) especifica que o comportamento de interoperabilidade padrão deve ser usado.  
  
- CLSID_RESOLUTION_REGISTERED: (0x1) especifica que o registro deve ser pesquisado e que a política de Shim deve ser aplicada.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A função retornou com êxito.|  
|E_INVALIDARG|Um dos parâmetros tem um tipo ou formato inválido.|  
|ERROR_INSUFFICIENT_BUFFER|O `pVersion` buffer não é grande o suficiente para manter a cadeia de caracteres da versão inteira.|  
|REGDB_E_CLASSNOTREG|Não há nenhuma classe registrada com o especificado `CLSID` .|  
|E_POINTER|`dwLength` é nulo ou `cchBuffer` é grande o suficiente para conter a cadeia de caracteres de versão, mas `pVersion` é nulo.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
