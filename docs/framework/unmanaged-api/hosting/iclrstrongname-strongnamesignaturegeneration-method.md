---
description: 'Saiba mais sobre o método: ICLRStrongName:: StrongNameSignatureGeneration'
title: Método ICLRStrongName::StrongNameSignatureGeneration
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureGeneration
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureGeneration
helpviewer_keywords:
- StrongNameSignatureGeneration method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameSignatureGeneration method [.NET Framework hosting]
ms.assetid: 4cdb1284-947a-4ed4-94c1-c5ff5cdfce56
topic_type:
- apiref
ms.openlocfilehash: ea8a6a9ea1e85af9d4e78cc950a02dbbc6815e4c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781877"
---
# <a name="iclrstrongnamestrongnamesignaturegeneration-method"></a>Método ICLRStrongName::StrongNameSignatureGeneration

Gera uma assinatura de nome forte para o assembly especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StrongNameSignatureGeneration (
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O caminho para o arquivo que contém o manifesto do assembly para o qual a assinatura de nome forte será gerada.  
  
 `wszKeyContainer`  
 no O nome do contêiner de chave que contém o par de chaves pública/privada.  
  
 Se `pbKeyBlob` for NULL, `wszKeyContainer` deve especificar um contêiner válido no CSP (provedor de serviços de criptografia). Nesse caso, o par de chaves armazenado no contêiner é usado para assinar o arquivo.  
  
 Se `pbKeyBlob` não for NULL, o par de chaves será considerado contido no BLOB (objeto binário grande) de chave.  
  
 As chaves devem ter chaves de assinatura de 1024 bits Rivest-Shamir-Adleman (RSA). Não há suporte para nenhum outro tipo de chave no momento.  
  
 `pbKeyBlob`  
 no Um ponteiro para o par de chaves pública/privada. Esse par está no formato criado pela função do Win32 `CryptExportKey` . Se `pbKeyBlob` for NULL, o contêiner de chave especificado por `wszKeyContainer` será considerado para conter o par de chaves.  
  
 `cbKeyBlob`  
 no O tamanho, em bytes, de `pbKeyBlob` .  
  
 `ppbSignatureBlob`  
 fora Um ponteiro para o local no qual o Common Language Runtime retorna a assinatura. Se `ppbSignatureBlob` for NULL, o tempo de execução armazenará a assinatura no arquivo especificado por `wszFilePath` .  
  
 Se `ppbSignatureBlob` não for NULL, o common language runtime aloca espaço para retornar a assinatura. O chamador deve liberar esse espaço usando o método [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) .  
  
 `pcbSignatureBlob`  
 fora O tamanho, em bytes, da assinatura retornada.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o método foi concluído com êxito; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="remarks"></a>Comentários  

 Especifique NULL para `wszFilePath` para calcular o tamanho da assinatura sem criar a assinatura.  
  
 A assinatura pode ser armazenada diretamente no arquivo ou retornada ao chamador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameSignatureGenerationEx](iclrstrongname-strongnamesignaturegenerationex-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
