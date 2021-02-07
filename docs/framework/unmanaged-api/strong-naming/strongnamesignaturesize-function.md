---
description: 'Saiba mais sobre: Função StrongNameSignatureSize'
title: Função StrongNameSignatureSize
ms.date: 03/30/2017
api_name:
- StrongNameSignatureSize
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureSize
helpviewer_keywords:
- StrongNameSignatureSize function [.NET Framework strong naming]
ms.assetid: 4fde4cd0-f53e-4411-a2fe-fc5c54472f95
topic_type:
- apiref
ms.openlocfilehash: b3f22a6a4d5455af4dd17cb75edfd18befed7de3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99670509"
---
# <a name="strongnamesignaturesize-function"></a>Função StrongNameSignatureSize

Retorna o tamanho da assinatura de nome forte. `StrongNameSignatureSize` normalmente é usado por compiladores para determinar a quantidade de espaço a ser reservada no arquivo ao criar um assembly com assinatura atrasada.  
  
 Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: StrongNameSignatureSize](../hosting/iclrstrongname-strongnamesignaturesize-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOLEAN StrongNameSignatureSize (
    [in]  BYTE   *pbPublicKeyBlob,  
    [in]  ULONG  cbPublicKeyBlob,
    [in]  DWORD  *pcbSize  
);
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbPublicKeyBlob`  
 no Uma estrutura do tipo [PublicKeyBlob](publickeyblob-structure.md) que contém a parte pública do par de chaves usado para gerar a assinatura de nome forte.  
  
 `cbPublicKeyBlob`  
 no O tamanho, em bytes, de `pbPublicKeyBlob` .  
  
 `pcbSize`  
 no O número de bytes necessários para armazenar a assinatura de nome forte.  
  
## <a name="return-value"></a>Valor retornado  

 `true` após a conclusão bem-sucedida; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 Se a `StrongNameSignatureSize` função não for concluída com êxito, chame a função [StrongNameErrorInfo](strongnameerrorinfo-function.md) para recuperar o último erro gerado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameSignatureSize](../hosting/iclrstrongname-strongnamesignaturesize-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
