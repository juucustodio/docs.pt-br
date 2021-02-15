---
description: 'Saiba mais sobre o método: ICLRStrongName:: GetHashFromAssemblyFile'
title: Método ICLRStrongName::GetHashFromAssemblyFile
ms.date: 03/30/2017
api_name:
- ICLRStrongName.GetHashFromAssemblyFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::GetHashFromAssemblyFile
helpviewer_keywords:
- ICLRStrongName::GetHashFromAssemblyFile method [.NET Framework hosting]
- GetHashFromAssemblyFile method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 0b67ea03-d474-4605-acaa-57455790250c
topic_type:
- apiref
ms.openlocfilehash: 40a8e2aabe9ade00243c535d63389f4265cc6ab0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799688"
---
# <a name="iclrstrongnamegethashfromassemblyfile-method"></a>Método ICLRStrongName::GetHashFromAssemblyFile

Obtém um hash do arquivo do assembly especificado, usando o algoritmo de hash especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetHashFromAssemblyFile (  
    [in]  LPCSTR   szFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE     *pbHash,  
    [in]  DWORD    cchHash,  
    [out] DWORD    *pchHash  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szFilePath`  
 no O caminho para o arquivo a ser transformado em hash.  
  
 `piHashAlg`  
 [entrada, saída] Uma constante que especifica o algoritmo de hash. Use zero para o algoritmo de hash padrão.  
  
 `pbHash`  
 fora O buffer de hash retornado.  
  
 `cchHash`  
 no O tamanho máximo solicitado de `pbHash` .  
  
 `pchHash`  
 fora O tamanho retornado, em bytes, de `pbHash` .  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o método foi concluído com êxito; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetHashFromAssemblyFileW](iclrstrongname-gethashfromassemblyfilew-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
