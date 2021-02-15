---
description: 'Saiba mais sobre o método: IMetaDataImport:: getuserstring'
title: Método IMetaDataImport::GetUserString
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetUserString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetUserString
helpviewer_keywords:
- IMetaDataImport::GetUserString method [.NET Framework metadata]
- GetUserString method, IMetaDataImport interface [.NET Framework metadata]
ms.assetid: 0fd3bb47-58b5-4083-b241-b9719df7a285
topic_type:
- apiref
ms.openlocfilehash: 074d196c74be30f5879410ad44b9bb5c096eb153
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789093"
---
# <a name="imetadataimportgetuserstring-method"></a>Método IMetaDataImport::GetUserString

Obtém a cadeia de caracteres literal representada pelo token de metadados especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetUserString (  
   [in]   mdString    stk,  
   [out]  LPWSTR      szString,  
   [in]   ULONG       cchString,  
   [out]  ULONG       *pchString  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `stk`  
 no O token da cadeia de caracteres para o qual retornar a cadeia de caracteres associada.  
  
 `szString`  
 fora Uma cópia da cadeia de caracteres solicitada.  
  
 `cchString`  
 no O tamanho máximo em caracteres largos do solicitado `szString` .  
  
 `pchString`  
 fora O tamanho em caracteres largos do retornado `szString` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
