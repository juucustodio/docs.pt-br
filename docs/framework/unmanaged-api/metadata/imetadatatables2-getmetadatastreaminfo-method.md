---
description: 'Saiba mais sobre o método: IMetaDataTables2:: GetMetaDataStreamInfo'
title: Método IMetaDataTables2::GetMetaDataStreamInfo
ms.date: 03/30/2017
api_name:
- IMetaDataTables2.GetMetaDataStreamInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables2::GetMetaDataStreamInfo
helpviewer_keywords:
- GetMetaDataStreamInfo method [.NET Framework metadata]
- IMetaDataTables2::GetMetaDataStreamInfo method [.NET Framework metadata]
ms.assetid: 8b280627-cc74-4789-95da-1fefc966de05
topic_type:
- apiref
ms.openlocfilehash: 323c31931cc97f18ff09df83c57153a3629d0a10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799233"
---
# <a name="imetadatatables2getmetadatastreaminfo-method"></a>Método IMetaDataTables2::GetMetaDataStreamInfo

Obtém o nome, o tamanho e o conteúdo do fluxo de metadados no índice especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMetaDataStreamInfo (  
   [in]  ULONG        ix,  
   [out] const char   **ppchName,  
   [out] const void   **ppv,  
   [out] ULONG        *pcb  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ix`  
 no O índice do fluxo de metadados solicitado.  
  
 `ppchName`  
 fora Um ponteiro para o nome do fluxo.  
  
 `ppv`  
 fora Um ponteiro para o fluxo de metadados.  
  
 `pcb`  
 fora O tamanho, em bytes, de `ppv` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataTables2](imetadatatables2-interface.md)
- [Interface IMetaDataTables](imetadatatables-interface.md)
