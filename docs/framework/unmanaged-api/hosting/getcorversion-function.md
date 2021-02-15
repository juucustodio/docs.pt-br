---
description: 'Saiba mais sobre: função GetCORVersion'
title: Função GetCORVersion
ms.date: 03/30/2017
api_name:
- GetCORVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORVersion
helpviewer_keywords:
- GetCORVersion function [.NET Framework hosting]
ms.assetid: 2f09cd37-bf3a-4cc5-87b0-adc42a7eed31
topic_type:
- apiref
ms.openlocfilehash: 96899b2193be9307314dbc2afb7cd6d70d229cfe
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785322"
---
# <a name="getcorversion-function"></a>Função GetCORVersion

Retorna o número de versão do Common Language Runtime (CLR) em execução no processo atual.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCORVersion (  
    [in] LPWSTR  pbuffer,  
    [in]  DWORD   cchBuffer,
    [out] DWORD*  dwlength  
);
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbuffer`  
 Um ponteiro para um buffer no qual o CLR retorna uma cadeia de caracteres especificando a versão do tempo de execução que está atualmente carregada no processo. A cadeia de caracteres retornada assume a mesma forma que as cadeias passadas para [CorBindToRuntimeEx](corbindtoruntimeex-function.md), por exemplo, "v 1.0.1216". Se o tempo de execução ainda não tiver sido carregado no processo, a função retornará as informações de diretório apropriadas para a versão mais recente do tempo de execução instalada no computador.  
  
 `cchBuffer`  
 O número de caracteres `WCHAR` que podem ser mantidos em `pbuffer` .  
  
 `dwLength`  
 Um ponteiro para o número de caracteres realmente retornados em `pbuffer` . Se `pbuffer` for um ponteiro NULL, o tempo de execução retornará E_POINTER. Se o número de caracteres for maior que o comprimento de `pbuffer` , o tempo de execução retornará ERROR_INSUFFICIENT_BUFFER.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
