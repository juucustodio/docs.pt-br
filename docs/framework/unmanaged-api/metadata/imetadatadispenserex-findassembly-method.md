---
description: 'Saiba mais sobre o método: IMetaDataDispenserEx:: FindAssembly'
title: Método IMetaDataDispenserEx::FindAssembly
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.FindAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::FindAssembly
helpviewer_keywords:
- FindAssembly method [.NET Framework metadata]
- IMetaDataDispenserEx::FindAssembly method [.NET Framework metadata]
ms.assetid: 3afe7252-5f28-48d9-a74d-1927566c404c
topic_type:
- apiref
ms.openlocfilehash: 6bed016e9235281b42f5a3231ef2aff284b6cc3b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753595"
---
# <a name="imetadatadispenserexfindassembly-method"></a>Método IMetaDataDispenserEx::FindAssembly

Este método não está implementado. Se chamado, ele retornará E_NOTIMPL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FindAssembly(  
    [in]  LPCWSTR  szAppBase,  
    [in]  LPCWSTR  szPrivateBin,  
    [in]  LPCWSTR  szGlobalBin,  
    [in]  LPCWSTR  szAssemblyName,  
    [out] LPCWSTR  szName,  
    [in]  ULONG    cchName,  
    [out] ULONG    *pcName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szAppBase`  
 no Não usado.  
  
 `szPrivateBin`  
 no Não usado.  
  
 `szGlobalBin`  
 no Não usado.  
  
 `szAssemblyName`  
 no O assembly a ser encontrado.  
  
 `szName`  
 fora O nome simples do assembly.  
  
 `cchName`  
 no O tamanho, em bytes, de `szName` .  
  
 `pcName`  
 fora O número de caracteres realmente retornados em `szName` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Interface IMetaDataDispenser](imetadatadispenser-interface.md)
