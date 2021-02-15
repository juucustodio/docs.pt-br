---
description: 'Saiba mais sobre o método: IMetaDataEmit2:: SaveDeltaToMemory'
title: Método IMetaDataEmit2::SaveDeltaToMemory
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.SaveDeltaToMemory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::SaveDeltaToMemory
helpviewer_keywords:
- SaveDeltaToMemory method [.NET Framework metadata]
- IMetaDataEmit2::SaveDeltaToMemory method [.NET Framework metadata]
ms.assetid: e2146726-0084-4c9e-a2d2-e8d461b13b21
topic_type:
- apiref
ms.openlocfilehash: 3ef01889df6dede85947508ca08635c95d655666
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99771750"
---
# <a name="imetadataemit2savedeltatomemory-method"></a>Método IMetaDataEmit2::SaveDeltaToMemory

Salva as alterações da sessão de edição e continuação atual na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SaveDeltaToMemory (  
    [out] void        *pbData,
    [in]  ULONG       cbData  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbData`  
 fora O endereço no qual começar a gravar o Delta de metadados.  
  
 `cbData`  
 no O tamanho das alterações. Use [IMetaDataEmit2:: GetDeltaSaveSize](imetadataemit2-getdeltasavesize-method.md) para determinar o tamanho.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
