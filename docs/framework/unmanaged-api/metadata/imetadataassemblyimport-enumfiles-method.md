---
description: 'Saiba mais sobre o método: IMetaDataAssemblyImport:: EnumFiles'
title: Método IMetaDataAssemblyImport::EnumFiles
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.EnumFiles
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::EnumFiles
helpviewer_keywords:
- IMetaDataAssemblyImport::EnumFiles method [.NET Framework metadata]
- EnumFiles method [.NET Framework metadata]
ms.assetid: f0d721e2-b946-426d-8e20-9124bd04e4cb
topic_type:
- apiref
ms.openlocfilehash: 25282edd081e937e4c84334f9f004e201b9db46f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671016"
---
# <a name="imetadataassemblyimportenumfiles-method"></a>Método IMetaDataAssemblyImport::EnumFiles

Enumera os arquivos referenciados no manifesto do assembly atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumFiles (  
    [in, out] HCORENUM    *phEnum,
    [out] mdFile          rFiles[],
    [in]  ULONG           cMax,
    [out] ULONG           *pcTokens  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador. Deve ser um valor nulo para a primeira chamada deste método.  
  
 `rFiles`  
 fora A matriz usada para armazenar os `mdFile` tokens de metadados.  
  
 `cMax`  
 no O número máximo de `mdFile` tokens que podem ser colocados `rFiles` .  
  
 `pcTokens`  
 fora O número de `mdFile` tokens realmente colocados no `rFiles` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumFiles` retornado com êxito.|  
|`S_FALSE`|Não há tokens para enumerar. Nesse caso, `pcTokens` é definido como zero.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyImport](imetadataassemblyimport-interface.md)
