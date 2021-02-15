---
description: 'Saiba mais sobre o método: ICLRStrongName:: StrongNameSignatureVerificationEx'
title: Método ICLRStrongName::StrongNameSignatureVerificationEx
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerificationEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerificationEx
helpviewer_keywords:
- StrongNameSignatureVerificationEx method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameSignatureVerificationEx method [.NET Framework hosting]
ms.assetid: dbd2f662-208b-4174-b301-5c99af91040f
topic_type:
- apiref
ms.openlocfilehash: 0e1692d7151e09a621b93823424b3ac10b6607d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789756"
---
# <a name="iclrstrongnamestrongnamesignatureverificationex-method"></a>Método ICLRStrongName::StrongNameSignatureVerificationEx

Obtém um valor que indica se o manifesto do assembly no caminho fornecido contém uma assinatura de nome forte.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StrongNameSignatureVerificationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  BOOLEAN   fForceVerification,  
    [out] BOOLEAN   *pfWasVerified  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O caminho para o arquivo executável portátil (. exe ou. dll) para o assembly a ser verificado.  
  
 `fForceVerification`  
 [in] `true` para executar a verificação, mesmo se for necessário substituir as configurações do registro; caso contrário, `false` .  
  
 `pfWasVerified`  
 [fora] `true` se a assinatura de nome forte foi verificada; caso contrário, `false` . `pfWasVerified` também será definido como `false` se a verificação tiver sido bem-sucedida devido a configurações do registro.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` se a verificação foi bem-sucedida; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="remarks"></a>Comentários  

 O método [ICLRStrongName:: StrongNameSignatureVerificationEx](iclrstrongname-strongnamesignatureverificationex-method.md) fornece um recurso semelhante ao método [ICLRStrongName:: StrongNameSignatureVerification](iclrstrongname-strongnamesignatureverification-method.md) . No entanto, o segundo parâmetro de entrada e o parâmetro de saída para [ICLRStrongName:: StrongNameSignatureVerificationEx](iclrstrongname-strongnamesignatureverificationex-method.md) são do tipo `BOOLEAN` em vez de `DWORD` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameSignatureVerification](iclrstrongname-strongnamesignatureverification-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
