---
description: 'Saiba mais sobre: função GetHashFromAssemblyFileW'
title: Função GetHashFromAssemblyFileW
ms.date: 03/30/2017
api_name:
- GetHashFromAssemblyFileW
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromAssemblyFileW
helpviewer_keywords:
- GetHashFromAssemblyFileW function [.NET Framework strong naming]
ms.assetid: d1b2b172-5353-42af-a877-cf653c68ece0
topic_type:
- apiref
ms.openlocfilehash: 7f44106f12a2d21ea67acb874b577c5b303632b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736668"
---
# <a name="gethashfromassemblyfilew-function"></a>Função GetHashFromAssemblyFileW

Obtém um hash do arquivo do assembly especificado, usando o algoritmo de hash especificado. O caminho para o arquivo de assembly deve ser especificado como uma cadeia de caracteres Unicode.  
  
 Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: GetHashFromAssemblyFileW](../hosting/iclrstrongname-gethashfromassemblyfilew-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetHashFromAssemblyFileW (  
    [in]  LPCWSTR   wszFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE      *pbHash,  
    [in]  DWORD     cchHash,  
    [out] DWORD     *pchHash  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O caminho para o arquivo a ser transformado em hash. Esse parâmetro deve ser uma cadeia de caracteres Unicode.  
  
 `piHashAlg`  
 [entrada, saída] Uma constante que especifica o algoritmo de hash. Use zero para o algoritmo de hash padrão.  
  
 `pbHash`  
 fora O buffer de hash retornado.  
  
 `cchHash`  
 no O tamanho máximo solicitado de `pbHash` .  
  
 `pchHash`  
 fora O tamanho retornado, em bytes, de `pbHash` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetHashFromAssemblyFileW](../hosting/iclrstrongname-gethashfromassemblyfilew-method.md)
- [Método GetHashFromAssemblyFile](../hosting/iclrstrongname-gethashfromassemblyfile-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
