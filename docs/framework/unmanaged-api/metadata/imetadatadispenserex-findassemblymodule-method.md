---
description: 'Saiba mais sobre o método: IMetaDataDispenserEx:: FindAssemblyModule'
title: Método IMetaDataDispenserEx::FindAssemblyModule
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.FindAssemblyModule
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::FindAssemblyModule
helpviewer_keywords:
- FindAssemblyModule method [.NET Framework metadata]
- IMetaDataDispenserEx::FindAssemblyModule method [.NET Framework metadata]
ms.assetid: d1fb65e1-7e19-4513-85b1-44f87c294d3e
topic_type:
- apiref
ms.openlocfilehash: 39ea13a2d8f2436e86db513aaa33f990f43d8132
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753569"
---
# <a name="imetadatadispenserexfindassemblymodule-method"></a>Método IMetaDataDispenserEx::FindAssemblyModule

Este método não está implementado. Se chamado, ele retornará E_NOTIMPL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FindAssemblyModule(  
    [in]  LPCWSTR  szAppBase,  
    [in]  LPCWSTR  szPrivateBin,  
    [in]  LPCWSTR  szGlobalBin,  
    [in]  LPCWSTR  szAssemblyName,  
    [in]  LPCWSTR  szModuleName,  
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
 no O nome do módulo.  
  
 `szModuleName`  
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
