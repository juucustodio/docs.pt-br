---
description: 'Saiba mais sobre o método: IMetaDataImport2:: GetVersionString'
title: Método IMetaDataImport2::GetVersionString
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetVersionString
helpviewer_keywords:
- GetVersionString method, IMetaDataImport2 interface [.NET Framework metadata]
- IMetaDataImport2::GetVersionString method [.NET Framework metadata]
ms.assetid: 308183ee-fd44-4432-9d86-ef00d181b49b
topic_type:
- apiref
ms.openlocfilehash: 6f7e296607dc3167936c69d52a8baae4f5555b88
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688553"
---
# <a name="imetadataimport2getversionstring-method"></a>Método IMetaDataImport2::GetVersionString

Obtém o número de versão do tempo de execução que foi usado para compilar o assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetVersionString (  
   [out] LPWSTR      pwzBuf,  
   [in]  DWORD       ccBufSize,  
   [out] DWORD       *pccBufSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzBuf`  
 fora Uma matriz para armazenar a cadeia de caracteres que especifica a versão.  
  
 `ccBufSize`  
 no O tamanho, em caracteres largos, da `pwzBuf` matriz.  
  
 `pccBufSize`  
 fora O número de caracteres largos, incluindo um terminador nulo, retornado na `pwzBuf` matriz.  
  
## <a name="remarks"></a>Comentários  

 O `GetVersionString` método obtém a versão interna do escopo de metadados atual. Se o escopo nunca tiver sido salvo, ele não terá uma versão interna e uma cadeia de caracteres vazia será retornada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport2](imetadataimport2-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
