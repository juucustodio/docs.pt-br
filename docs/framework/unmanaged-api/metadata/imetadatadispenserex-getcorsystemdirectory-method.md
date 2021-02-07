---
description: 'Saiba mais sobre o método: IMetaDataDispenserEx:: GetCORSystemDirectory'
title: Método IMetaDataDispenserEx::GetCORSystemDirectory
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.GetCORSystemDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory
helpviewer_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory method [.NET Framework metadata]
- GetCORSystemDirectory method [.NET Framework metadata]
ms.assetid: d9e0f3b6-e106-4820-bada-5bfba34ce360
topic_type:
- apiref
ms.openlocfilehash: 3ceda653e50ba5ad7de5548b78781f48cda41624
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753556"
---
# <a name="imetadatadispenserexgetcorsystemdirectory-method"></a>Método IMetaDataDispenserEx::GetCORSystemDirectory

Obtém o diretório que contém o Common Language Runtime atual (CLR). Esse método só tem suporte para uso por depuradores fora do processo. Se for chamado de outro componente, ele retornará E_NOTIMPL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCORSystemDirectory (  
    [out] LPWSTR      szBuffer,
    [in]  DWORD       cchBuffer,
    [out] DWORD*      pchBuffer  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szBuffer`  
 fora O buffer para receber o nome do diretório.  
  
 `cchBuffer`  
 no O tamanho, em bytes, de `szBuffer` .  
  
 `pchBuffer`  
 fora O número de bytes realmente retornados em `szBuffer` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Interface IMetaDataDispenser](imetadatadispenser-interface.md)
