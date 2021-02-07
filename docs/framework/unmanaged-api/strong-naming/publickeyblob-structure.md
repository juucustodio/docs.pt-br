---
description: 'Saiba mais sobre: estrutura PublicKeyBlob'
title: Estrutura PublicKeyBlob
ms.date: 03/30/2017
api_name:
- PublicKeyBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- PublicKeyBlob
helpviewer_keywords:
- PublicKeyBlob structure [.NET Framework strong naming]
ms.assetid: b9240712-829c-4c8d-9a09-a6e7aa63f63a
topic_type:
- apiref
ms.openlocfilehash: 94c1ea3d5a41bbb8941658e87f97cd6d6336187a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736473"
---
# <a name="publickeyblob-structure"></a>Estrutura PublicKeyBlob

Representa, em formato binário, a chave pública de um par de chaves pública/privada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct {  
    unsigned int SigAlgId;  
    unsigned int HashAlgId;  
    ULONG cbPublicKey;  
    BYTE PublicKey[1]  
} PublicKeyBlob;
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`SigAlgId`|O identificador do algoritmo de assinatura (do tipo `ALG_ID` , conforme definido em Wincrypt. h) da chave pública.|  
|`HashAlgId`|O identificador do algoritmo de hash (do tipo `ALG_ID` , conforme definido em Wincrypt. h) da chave pública.|  
|`cbPublicKey`|O comprimento da chave em bytes.|  
|`PublicKey`|Uma matriz de bytes de comprimento variável que contém o valor da chave no formato retornado pela CryptoAPI.|  
  
## <a name="remarks"></a>Comentários  

 A `PublicKeyBlob` estrutura é usada por [StrongNameGetPublicKey](strongnamegetpublickey-function.md), [StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md)e outras funções de nome forte para representar a chave pública de um par de chaves pública/privada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função StrongNameGetPublicKey](strongnamegetpublickey-function.md)
- [Função StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md)
