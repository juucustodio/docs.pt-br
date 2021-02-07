---
description: 'Saiba mais sobre o método: IMetaDataTables:: GetCodedTokenInfo'
title: Método IMetaDataTables::GetCodedTokenInfo
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetCodedTokenInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetCodedTokenInfo
helpviewer_keywords:
- GetCodedTokenInfo method [.NET Framework metadata]
- IMetaDataTables::GetCodedTokenInfo method [.NET Framework metadata]
ms.assetid: 31214d3a-715e-49af-92b3-0fd11e4f218a
topic_type:
- apiref
ms.openlocfilehash: 982a13636d8b4572113038eaa658158e6c2ca966
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688280"
---
# <a name="imetadatatablesgetcodedtokeninfo-method"></a>Método IMetaDataTables::GetCodedTokenInfo

Obtém um ponteiro para uma matriz de tokens associados ao índice de linha especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCodedTokenInfo (
    [in]  ULONG       ixCdTkn,  
    [out] ULONG       *pcTokens,  
    [out] ULONG       **ppTokens,  
    [out] const char  **ppName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ixCdTkn`  
 no O tipo de token codificado a ser retornado.  
  
 `pcTokens`  
 fora Um ponteiro para o comprimento de `ppTokens` .  
  
 `ppTokens`  
 fora Um ponteiro para um ponteiro para uma matriz que contém a lista de tokens retornados.  
  
 `ppName`  
 fora Um ponteiro para um ponteiro para o nome do token em `ixCdTkn` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataTables](imetadatatables-interface.md)
- [Interface IMetaDataTables2](imetadatatables2-interface.md)
