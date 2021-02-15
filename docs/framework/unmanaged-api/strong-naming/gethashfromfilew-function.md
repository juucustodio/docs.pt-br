---
description: 'Saiba mais sobre: Função GetHashFromFileW'
title: Função GetHashFromFileW
ms.date: 03/30/2017
api_name:
- GetHashFromFileW
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromFileW
helpviewer_keywords:
- GetHashFromFileW function [.NET Framework strong naming]
ms.assetid: 97c2d7a6-5376-45a1-ba65-146a249147cc
topic_type:
- apiref
ms.openlocfilehash: daebd06de02dfe936f1bdeb8697de4fe6524dce3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736502"
---
# <a name="gethashfromfilew-function"></a>Função GetHashFromFileW

Gera um hash sobre o conteúdo do arquivo especificado por uma cadeia de caracteres Unicode.  
  
 Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: GetHashFromFileW](../hosting/iclrstrongname-gethashfromfilew-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetHashFromFileW (
    [in]  LPCWSTR   wszFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE      *pbHash,  
    [in]  DWORD     cchHash,  
    [out] DWORD     *pchHash  
);
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O nome Unicode do arquivo para hash.  
  
 `piHashAlg`  
 [entrada, saída] O algoritmo a ser usado ao gerar o hash. Os algoritmos válidos são aqueles definidos pelo CryptoAPI do Win32. Se `piHashAlg` for definido como 0, o algoritmo padrão CALG_SHA-1 será usado.  
  
 `pbHash`  
 fora Uma matriz de bytes que contém o hash gerado.  
  
 `cchHash`  
 no O tamanho máximo do buffer apontado por `pbHash` .  
  
 `pchHash`  
 fora O tamanho, em bytes, de `pbHash` .  
  
## <a name="remarks"></a>Comentários  

 Essa função é igual a [GetHashFromFile](gethashfromfile-function.md), exceto que a especificação de nome de arquivo é Unicode em vez de ANSI.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetHashFromFileW](../hosting/iclrstrongname-gethashfromfilew-method.md)
- [Método GetHashFromFile](../hosting/iclrstrongname-gethashfromfile-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
