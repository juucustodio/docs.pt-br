---
description: 'Saiba mais sobre: IMetaDataEmit: método efinePinvokeMap de:D'
title: Método IMetaDataEmit::DefinePinvokeMap
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefinePinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefinePinvokeMap
helpviewer_keywords:
- DefinePinvokeMap method [.NET Framework metadata]
- IMetaDataEmit::DefinePinvokeMap method [.NET Framework metadata]
ms.assetid: 03abf921-5154-4070-88fa-10b7092901fb
topic_type:
- apiref
ms.openlocfilehash: 7b0477ca603241e773a67f335da579daa2ed3d30
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784061"
---
# <a name="imetadataemitdefinepinvokemap-method"></a>Método IMetaDataEmit::DefinePinvokeMap

Define os recursos da assinatura PInvoke do método referenciado pelo token especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefinePinvokeMap (
    [in]  mdToken            tk,
    [in]  DWORD              dwMappingFlags,
    [in]  LPCWSTR            szImportName,
    [in]  mdModuleRef        mrImportDLL
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no O token para o método de destino.  
  
 `dwMappingFlags`  
 no Sinalizadores usados pelo PInvoke para fazer o mapeamento.  
  
 `szImportName`  
 no O nome do método de exportação de destino em uma DLL não gerenciada.  
  
 `mrImportDLL`  
 no O token para a DLL nativa de destino.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
