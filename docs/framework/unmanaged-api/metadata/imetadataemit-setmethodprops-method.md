---
description: 'Saiba mais sobre o método: IMetaDataEmit:: SetMethodProps'
title: Método IMetaDataEmit::SetMethodProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetMethodProps
helpviewer_keywords:
- SetMethodProps method [.NET Framework metadata]
- IMetaDataEmit::SetMethodProps method [.NET Framework metadata]
ms.assetid: e0c6ac12-22ea-43f5-b799-8cda0faf3336
topic_type:
- apiref
ms.openlocfilehash: edecdc14abb386f8fa4cd70535f2b8c012bdc59f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772088"
---
# <a name="imetadataemitsetmethodprops-method"></a>Método IMetaDataEmit::SetMethodProps

Define ou atualiza o recurso, armazenado no endereço virtual relativo especificado, de um método definido por uma chamada anterior para [IMetaDataEmit::D efinemethod](imetadataemit-definemethod-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetMethodProps (
    [in]  mdMethodDef md,
    [in]  DWORD       dwMethodFlags,  
    [in]  ULONG       ulCodeRVA,
    [in]  DWORD       dwImplFlags
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `md`  
 no O token para o método a ser alterado.  
  
 `dwMethodFlags`  
 no Os atributos de membro.  
  
 `ulCodeRVA`  
 no O endereço do código.  
  
 `dwImplFlags`  
 no Os sinalizadores de implementação para o método.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
