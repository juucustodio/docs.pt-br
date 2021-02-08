---
description: 'Saiba mais sobre o método: ICLRStrongName:: StrongNameTokenFromAssembly'
title: Método ICLRStrongName::StrongNameTokenFromAssembly
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameTokenFromAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly
helpviewer_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly method [.NET Framework hosting]
- StrongNameTokenFromAssembly method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: fc725afb-b66b-4015-aa44-1c0d1304197f
topic_type:
- apiref
ms.openlocfilehash: 520d327767f91763f8f2b3efea098c7c2790939e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781812"
---
# <a name="iclrstrongnamestrongnametokenfromassembly-method"></a>Método ICLRStrongName::StrongNameTokenFromAssembly

Cria um token de nome forte do arquivo do assembly especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StrongNameTokenFromAssembly (  
    [in]  LPCWSTR   wszFilePath,  
    [out] BYTE      **ppbStrongNameToken,  
    [out] ULONG     *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O caminho para o arquivo executável portátil (PE) para o assembly.  
  
 `ppbStrongNameToken`  
 fora O token de nome forte retornado.  
  
 `pcbStrongNameToken`  
 fora O tamanho, em bytes, do token de nome forte.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o método foi concluído com êxito; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="remarks"></a>Comentários  

 Um token de nome forte é a forma abreviada de uma chave pública. O token é um hash de 64 bits que é criado a partir da chave pública usada para assinar o assembly. O token é uma parte do nome forte para o assembly e pode ser lido nos metadados do assembly.  
  
 Depois que o token é criado, você deve chamar o método [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) para liberar a memória alocada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameTokenFromAssemblyEx](iclrstrongname-strongnametokenfromassemblyex-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
