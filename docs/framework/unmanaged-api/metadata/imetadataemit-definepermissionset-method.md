---
description: 'Saiba mais sobre: IMetaDataEmit: método efinePermissionSet de:D'
title: Método IMetaDataEmit::DefinePermissionSet
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefinePermissionSet
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefinePermissionSet
helpviewer_keywords:
- DefinePermissionSet method [.NET Framework metadata]
- IMetaDataEmit::DefinePermissionSet method [.NET Framework metadata]
ms.assetid: 36cffbf7-82ca-4cf9-bf60-50ab491ac2d9
topic_type:
- apiref
ms.openlocfilehash: f5c3f1466217713cb3970c805079d8f65fd429c0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784074"
---
# <a name="imetadataemitdefinepermissionset-method"></a>Método IMetaDataEmit::DefinePermissionSet

Cria uma definição para um conjunto de permissões com a assinatura de metadados especificada e Obtém um token para essa definição de conjunto de permissões.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefinePermissionSet (  
    [in]  mdToken        tk,
    [in]  DWORD          dwAction,
    [in]  void const     *pvPermission,
    [in]  ULONG          cbPermission,
    [out] mdPermission   *ppm
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no O objeto a ser decorado.  
  
 `dwAction`  
 no Um valor de [CorDeclSecurity](cordeclsecurity-enumeration.md) que especifica o tipo de segurança declarativa a ser usado.  
  
 `pvPermission`  
 no O BLOB de permissão.  
  
 `cbPermission`  
 no O tamanho, em bytes, de `pvPermission` .  
  
 `ppm`  
 fora O token de permissão retornado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
