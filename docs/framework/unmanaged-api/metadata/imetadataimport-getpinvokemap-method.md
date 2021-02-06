---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetPinvokeMap'
title: Método IMetaDataImport::GetPinvokeMap
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPinvokeMap
helpviewer_keywords:
- IMetaDataImport::GetPinvokeMap method [.NET Framework metadata]
- GetPinvokeMap method [.NET Framework metadata]
ms.assetid: b8685c1e-b80c-4198-8eb3-748d6f48a99e
topic_type:
- apiref
ms.openlocfilehash: fcf45f4741709423aa48dcf895dfc4be276e19fe
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649423"
---
# <a name="imetadataimportgetpinvokemap-method"></a>Método IMetaDataImport::GetPinvokeMap

Obtém um token ModuleRef para representar o assembly de destino de uma chamada PInvoke.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetPinvokeMap (  
   [in]  mdToken       tk,  
   [out] DWORD         *pdwMappingFlags,  
   [out] LPWSTR        szImportName,  
   [in]  ULONG         cchImportName,  
   [out] ULONG         *pchImportName,  
   [out] mdModuleRef   *pmrImportDLL  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no Um token FieldDef ou MethodDef para obter os metadados de mapeamento do PInvoke.  
  
 `pdwMappingFlags`  
 fora Um ponteiro para sinalizadores usados para mapeamento. Esse valor é um bitmask da enumeração [CorPinvokeMap](corpinvokemap-enumeration.md) .  
  
 `szImportName`  
 fora O nome da DLL de destino não gerenciada.  
  
 `cchImportName`  
 no O tamanho em caracteres largos de `szImportName` .  
  
 `pchImportName`  
 fora O número de caracteres largos retornados em `szImportName` .  
  
 `pmrImportDLL`  
 fora Um ponteiro para um token de ModuleRef que representa a biblioteca de objetos de destino não gerenciado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
