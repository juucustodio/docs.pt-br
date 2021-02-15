---
description: 'Saiba mais sobre: função GetCORRequiredVersion'
title: Função GetCORRequiredVersion
ms.date: 03/30/2017
api_name:
- GetCORRequiredVersion
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetCORRequiredVersion
helpviewer_keywords:
- GetCORRequiredVersion function [.NET Framework hosting]
ms.assetid: 1588fe7b-c378-4f4b-9c4b-48647f1119cc
topic_type:
- apiref
ms.openlocfilehash: ea1b928054e3ec6080b00e2a41228035f50c0f84
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785348"
---
# <a name="getcorrequiredversion-function"></a>Função GetCORRequiredVersion

Obtém o número de versão do Common Language Runtime (CLR) necessário.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCORRequiredVersion (  
    [out] LPWSTR   pbuffer,  
    [in]  DWORD    cchBuffer,  
    [out] DWORD   *dwLength  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbuffer`  
 fora Um buffer que contém uma cadeia de caracteres que especifica o número de versão.  
  
 `cchBuffer`  
 no O tamanho, em bytes, do buffer.  
  
 `dwLength`  
 fora O número de bytes retornados no buffer.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
