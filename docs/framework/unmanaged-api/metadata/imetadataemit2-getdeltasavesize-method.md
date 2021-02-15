---
description: 'Saiba mais sobre o método: IMetaDataEmit2:: GetDeltaSaveSize'
title: Método IMetaDataEmit2::GetDeltaSaveSize
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.GetDeltaSaveSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::GetDeltaSaveSize
helpviewer_keywords:
- IMetaDataEmit2::GetDeltaSaveSize method [.NET Framework metadata]
- GetDeltaSaveSize method [.NET Framework metadata]
ms.assetid: 036db5e7-8211-4645-9a34-03d1a89be955
topic_type:
- apiref
ms.openlocfilehash: d7b5eae7f89a5465876083c5cc8021330d3c59de
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745756"
---
# <a name="imetadataemit2getdeltasavesize-method"></a>Método IMetaDataEmit2::GetDeltaSaveSize

Obtém um valor que indica qualquer alteração no tamanho dos metadados que resulta da sessão de edição e continuação atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDeltaSaveSize (  
    [in]  CorSaveSize  fSave,  
    [out] DWORD        *pdwSaveSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fSave`  
 no Um dos valores de [CorSaveSize](corsavesize-enumeration.md) , indicando o nível de precisão desejado. Para o .NET Framework versão 2,0, esse parâmetro é ignorado.  
  
 `pdwSaveSize`  
 fora A alteração no tamanho dos metadados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
