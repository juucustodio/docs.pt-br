---
description: 'Saiba mais sobre: IMetaDataAssemblyEmit: método efineFile de:D'
title: Método IMetaDataAssemblyEmit::DefineFile
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineFile
helpviewer_keywords:
- IMetaDataAssemblyEmit::DefineFile method [.NET Framework metadata]
- DefineFile method [.NET Framework metadata]
ms.assetid: c065aadf-c1ca-4981-bde6-597042cb29c4
topic_type:
- apiref
ms.openlocfilehash: 825ef44c2b0a5f312b4c5f9c851d62e75709c7ff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671042"
---
# <a name="imetadataassemblyemitdefinefile-method"></a>Método IMetaDataAssemblyEmit::DefineFile

Cria uma `File` estrutura de metadados que contém metadados para o assembly referenciado por esse assembly e retorna o token de metadados associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineFile (  
    [in]  LPCWSTR        szName,
    [in]  const void     *pbHashValue,
    [in]  ULONG          cbHashValue,  
    [in]  DWORD          dwFileFlags,  
    [out] mdFile         *pmdf  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szName`  
 no O nome do arquivo a ser consumido.  
  
 `pbHashValue`  
 no Um ponteiro para os dados de hash associados ao assembly.  
  
 `cbHashValue`  
 no O tamanho em bytes de `pbHashValue` .  
  
 `dwFileFlags`  
 no Uma combinação de bits de `FileFlags` valores que especifica as configurações de propriedade.  
  
 `pmdf`  
 fora Um ponteiro para o `File` token retornado.  
  
## <a name="remarks"></a>Comentários  

 Uma `File` estrutura de metadados deve ser definida para cada arquivo que faz parte desse assembly no momento em que esse assembly foi criado, excluindo o arquivo que contém os metadados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
