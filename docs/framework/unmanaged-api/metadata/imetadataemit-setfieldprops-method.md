---
description: 'Saiba mais sobre o método: IMetaDataEmit:: SetFieldProps'
title: Método IMetaDataEmit::SetFieldProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetFieldProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetFieldProps
helpviewer_keywords:
- IMetaDataEmit::SetFieldProps method [.NET Framework metadata]
- SetFieldProps method [.NET Framework metadata]
ms.assetid: 47132dda-fa92-4bd1-ae4b-24cd9a60665a
topic_type:
- apiref
ms.openlocfilehash: ee9964077e556a1d0666a836ca0c3bab92540252
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658003"
---
# <a name="imetadataemitsetfieldprops-method"></a>Método IMetaDataEmit::SetFieldProps

Define ou atualiza o valor padrão para o campo referenciado pelo token do campo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetFieldProps (  
    [in]  mdFieldDef  fd,
    [in]  DWORD       dwFieldFlags,
    [in]  DWORD       dwCPlusTypeFlag,
    [in]  void const  *pValue,
    [in]  ULONG       cchValue
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fd`  
 no O token para o campo de destino.  
  
 `dwFieldFlags`  
 no Atributos de campo. Esta é uma bitmask de `CorFieldAttr` valores.  
  
 `dwCPlusTypeFlag`  
 no O `ELEMENT_TYPE_` *\** para o valor da constante. Esse é um `CorElementType` valor. Se uma constante não estiver sendo definida, defina esse valor como `ELEMENT_TYPE_END` .  
  
 `pValue`  
 no O valor constante para o campo.  
  
 `cchValue`  
 no O tamanho, em caracteres Unicode, de `pValue` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
