---
description: 'Saiba mais sobre: função StrongNameGetPublicKey'
title: Função StrongNameGetPublicKey
ms.date: 03/30/2017
api_name:
- StrongNameGetPublicKey
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey function [.NET Framework strong naming]
ms.assetid: 5b58c87f-3f72-40df-9b9a-291076931cc3
topic_type:
- apiref
ms.openlocfilehash: c94ffdd20e83b03da27b2f44ebbc279cfd8b8afc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99670561"
---
# <a name="strongnamegetpublickey-function"></a>Função StrongNameGetPublicKey

Obtém a chave pública de um par de chaves pública/privada. O par de chaves pode ser fornecido como um nome de contêiner de chave em um CSP (provedor de serviços de criptografia) ou como uma coleção bruta de bytes.  
  
 Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: StrongNameGetPublicKey](../hosting/iclrstrongname-strongnamegetpublickey-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOLEAN StrongNameGetPublicKey (
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szKeyContainer`  
 no O nome do contêiner de chave que contém o par de chaves pública/privada. Se `pbKeyBlob` for NULL, `szKeyContainer` deve especificar um contêiner válido no CSP. Nesse caso, `StrongNameGetPublicKey` o extrai a chave pública do par de chaves armazenado no contêiner.  
  
 Se `pbKeyBlob` não for NULL, o par de chaves será considerado contido no BLOB (objeto binário grande) de chave.  
  
 As chaves devem ter chaves de assinatura de 1024 bits Rivest-Shamir-Adleman (RSA). Não há suporte para nenhum outro tipo de chave no momento.  
  
 `pbKeyBlob`  
 no Um ponteiro para o par de chaves pública/privada. Esse par está no formato criado pela função do Win32 `CryptExportKey` . Se `pbKeyBlob` for NULL, o contêiner de chave especificado por `szKeyContainer` será considerado para conter o par de chaves.  
  
 `cbKeyBlob`  
 no O tamanho, em bytes, de `pbKeyBlob` .  
  
 `ppbPublicKeyBlob`  
 fora O BLOB de chave pública retornado. O `ppbPublicKeyBlob` parâmetro é alocado pelo Common Language Runtime e retornado ao chamador. O chamador deve liberar a memória usando a função [StrongNameFreeBuffer](strongnamefreebuffer-function.md) .  
  
 `pcbPublicKeyBlob`  
 fora O tamanho do BLOB de chave pública retornado.  
  
## <a name="return-value"></a>Valor retornado  

 `true` após a conclusão bem-sucedida; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 A chave pública está contida em uma estrutura [PublicKeyBlob](publickeyblob-structure.md) .  
  
 Se a `StrongNameGetPublicKey` função não for concluída com êxito, chame a função [StrongNameErrorInfo](strongnameerrorinfo-function.md) para recuperar o último erro gerado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameGetPublicKey](../hosting/iclrstrongname-strongnamegetpublickey-method.md)
- [Método StrongNameTokenFromPublicKey](../hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
- [Estrutura PublicKeyBlob](publickeyblob-structure.md)
