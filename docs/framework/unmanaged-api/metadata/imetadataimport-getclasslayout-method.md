---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetClassLayout'
title: Método IMetaDataImport::GetClassLayout
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetClassLayout
helpviewer_keywords:
- IMetaDataImport::GetClassLayout method [.NET Framework metadata]
- GetClassLayout method, IMetaDataImport interface [.NET Framework metadata]
ms.assetid: 8f35414d-f40b-4b99-8768-9adb675c622a
topic_type:
- apiref
ms.openlocfilehash: 74a3170e40a7f857b9150f2d0048af3eac0f2cbd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745418"
---
# <a name="imetadataimportgetclasslayout-method"></a>Método IMetaDataImport::GetClassLayout

Obtém informações de layout para a classe referenciada pelo token de TypeDef especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetClassLayout  (
   [in]  mdTypeDef          td,
   [out] DWORD              *pdwPackSize,  
   [out] COR_FIELD_OFFSET   rFieldOffset[],  
   [in]  ULONG              cMax,  
   [out] ULONG              *pcFieldOffset,  
   [out] ULONG              *pulClassSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `td`  
 no O token de TypeDef para a classe com o layout a ser retornado.  
  
 `pdwPackSize`  
 fora Um dos valores 1, 2, 4, 8 ou 16, que representa o tamanho do pacote da classe.  
  
 `rFieldOffset`  
 fora Uma matriz de valores de [COR_FIELD_OFFSET](cor-field-offset-structure.md) .  
  
 `cMax`  
 no O tamanho máximo da `rFieldOffset` matriz.  
  
 `pcFieldOffset`  
 fora O número de elementos retornados em `rFieldOffset` .  
  
 `pulClassSize`  
 fora O tamanho em bytes da classe representada por `td` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
