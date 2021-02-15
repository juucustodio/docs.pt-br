---
description: 'Saiba mais sobre o método: ICLRStrongName:: StrongNameKeyInstall'
title: Método ICLRStrongName::StrongNameKeyInstall
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyInstall
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyInstall
helpviewer_keywords:
- ICLRStrongName::StrongNameKeyInstall method [.NET Framework hosting]
- StrongNameKeyInstall method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 5c15cf3b-164c-49d1-8e57-e42949d55acf
topic_type:
- apiref
ms.openlocfilehash: 8f9e7bfebff555a6430a3970c8ee1c481e341f58
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799506"
---
# <a name="iclrstrongnamestrongnamekeyinstall-method"></a>Método ICLRStrongName::StrongNameKeyInstall

Importa um par de chaves públicas/privadas em um contêiner.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StrongNameKeyInstall (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszKeyContainer`  
 no O nome do contêiner de chave. `wszKeyContainer` deve ser uma cadeia de caracteres não vazia.  
  
 `pbKeyBlob`  
 no O par de chaves binárias.  
  
 `cbKeyBlob`  
 no O tamanho, em bytes, de `pbKeyBlob` .  
  
## <a name="return-value"></a>Valor retornado  

 `S_OK` Se o método foi concluído com êxito; caso contrário, um valor HRESULT que indica falha (consulte [valores de HRESULT comuns](/windows/win32/seccrypto/common-hresult-values) para uma lista).  
  
## <a name="remarks"></a>Comentários  

 Use o método [ICLRStrongName:: StrongNameKeyDelete](iclrstrongname-strongnamekeydelete-method.md) para excluir o contêiner de chave.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameKeyDelete](iclrstrongname-strongnamekeydelete-method.md)
- [Interface ICLRStrongName](iclrstrongname-interface.md)
