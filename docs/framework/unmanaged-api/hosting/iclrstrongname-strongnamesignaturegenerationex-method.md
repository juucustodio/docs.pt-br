---
description: 'Saiba mais sobre o método: ICLRStrongName:: StrongNameSignatureGenerationEx'
title: Método ICLRStrongName::StrongNameSignatureGenerationEx
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureGenerationEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx method [.NET Framework hosting]
- StrongNameSignatureGenerationEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: c3f34584-c6e2-41fd-bb44-e44da8546309
topic_type:
- apiref
ms.openlocfilehash: 911f55aa509c25eb0d95d6d2a31c9f715af2080d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781864"
---
# <a name="iclrstrongnamestrongnamesignaturegenerationex-method"></a>Método ICLRStrongName::StrongNameSignatureGenerationEx

Gera uma assinatura de nome forte para o assembly especificado, de acordo com os sinalizadores especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT StrongNameSignatureGenerationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob,  
    [in]  DWORD     dwFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszFilePath`  
 no O caminho para o arquivo que contém o manifesto do assembly para o qual a assinatura de nome forte será gerada.  
  
 `wszKeyContainer`  
 no O nome do contêiner de chave que contém o par de chaves pública/privada.  
  
 Se `pbKeyBlob` for NULL, `wszKeyContainer` deve especificar um contêiner válido no CSP (provedor de serviços de criptografia). Nesse caso, o par de chaves armazenado no contêiner é usado para assinar o arquivo.  
  
 Se `pbKeyBlob` não for NULL, o par de chaves será considerado contido no BLOB (objeto binário grande) de chave.  
  
 `pbKeyBlob`  
 no Um ponteiro para o par de chaves pública/privada. Esse par está no formato criado pela função do Win32 `CryptExportKey` . Se `pbKeyBlob` for NULL, o contêiner de chave especificado por `wszKeyContainer` será considerado para conter o par de chaves.  
  
 `cbKeyBlob`  
 no O tamanho, em bytes, de `pbKeyBlob` .  
  
 `ppbSignatureBlob`  
 fora Um ponteiro para o local no qual o Common Language Runtime retorna a assinatura. Se `ppbSignatureBlob` for NULL, o tempo de execução armazenará a assinatura no arquivo especificado por `wszFilePath` .  
  
 Se `ppbSignatureBlob` não for NULL, o common language runtime aloca espaço para retornar a assinatura. O chamador deve liberar esse espaço usando o método [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) .  
  
 `pcbSignatureBlob`  
 fora O tamanho, em bytes, da assinatura retornada.  
  
 `dwFlags`  
 no Um ou mais dos seguintes valores:  
  
- `SN_SIGN_ALL_FILES` (0x00000001) – recomputar todos os hashes para módulos vinculados.  
  
- `SN_TEST_SIGN` (0x00000002)-testar o assembly.  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o método foi concluído com êxito; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="remarks"></a>Comentários  

 Especifique NULL para `wszFilePath` para calcular o tamanho da assinatura sem criar a assinatura.  
  
 A assinatura pode ser armazenada diretamente no arquivo ou retornada ao chamador.  
  
 Se `SN_SIGN_ALL_FILES` for especificado, mas uma chave pública não estiver incluída ( `pbKeyBlob` e `wszFilePath` forem nulas), os hashes para módulos vinculados serão recalculados, mas o assembly não será assinado novamente.  
  
 Se `SN_TEST_SIGN` for especificado, o cabeçalho de Common Language Runtime não será modificado para indicar que o assembly é assinado com um nome forte.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameSignatureGeneration](iclrstrongname-strongnamesignaturegeneration-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
