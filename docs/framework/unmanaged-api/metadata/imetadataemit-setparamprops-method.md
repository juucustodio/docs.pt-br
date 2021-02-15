---
description: 'Saiba mais sobre o método: IMetaDataEmit:: SetParamProps'
title: Método IMetaDataEmit::SetParamProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetParamProps
helpviewer_keywords:
- IMetaDataEmit::SetParamProps method [.NET Framework metadata]
- SetParamProps method [.NET Framework metadata]
ms.assetid: a95a3908-9f87-4084-937e-8e01ef03ad63
topic_type:
- apiref
ms.openlocfilehash: 35e839b05b3671c6c09f315ac636971c386e766e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772010"
---
# <a name="imetadataemitsetparamprops-method"></a>Método IMetaDataEmit::SetParamProps

Define ou altera recursos de um parâmetro de método que foi definido por uma chamada anterior para [IMetaDataEmit::D efineparam](imetadataemit-defineparam-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetParamProps (
    [in]  mdParamDef  pd,
    [in]  LPCWSTR     szName,
    [in]  DWORD       dwParamFlags,
    [in]  DWORD       dwCPlusTypeFlag,
    [in]  void const  *pValue,
    [in]  ULONG       cchValue
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pd`  
 no O token para o parâmetro de destino.  
  
 `szName`  
 no O nome do parâmetro em Unicode.  
  
 `dwParamFlags`  
 no Os sinalizadores para o parâmetro.  
  
 `dwCPlusTypeFlag`  
 no O ELEMENT_TYPE_ * para o valor constante.  
  
 `pValue`  
 no O valor da constante para o parâmetro.  
  
 `cchValue`  
 no O tamanho em caracteres (Unicode) de `pValue` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
