---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetCustomAttributeProps'
title: Método IMetaDataImport::GetCustomAttributeProps
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetCustomAttributeProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetCustomAttributeProps
helpviewer_keywords:
- GetCustomAttributeProps method [.NET Framework metadata]
- IMetaDataImport::GetCustomAttributeProps method [.NET Framework metadata]
ms.assetid: 6eefb243-a281-41c1-bcdc-7e17513bc446
topic_type:
- apiref
ms.openlocfilehash: 9bd8e83301252d7ead225146e562d3a58feb244a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745356"
---
# <a name="imetadataimportgetcustomattributeprops-method"></a>Método IMetaDataImport::GetCustomAttributeProps

Obtém o valor do atributo personalizado, dado seu token de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCustomAttributeProps (  
   [in]            mdCustomAttribute   cv,  
   [out, optional] mdToken             *ptkObj,  
   [out, optional] mdToken             *ptkType,  
   [out, optional] void const          **ppBlob,  
   [out, optional] ULONG               *pcbSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cv`  
 no Um token de metadados que representa o atributo personalizado a ser recuperado.  
  
 `ptkObj`  
 [saída, opcional] Um token de metadados que representa o objeto que o atributo personalizado modifica. Esse valor pode ser qualquer tipo de token de metadados, exceto `mdCustomAttribute` .  
  
 `ptkType`  
 [saída, opcional] Um `mdMethodDef` `mdMemberRef` token de metadados ou que representa o <xref:System.Type> do atributo personalizado retornado.  
  
 `ppBlob`  
 [saída, opcional] Um ponteiro para uma matriz de dados que é o valor do atributo personalizado.  
  
 `pcbSize`  
 [saída, opcional] O tamanho em bytes dos dados retornados em * `ppBlob` .  
  
## <a name="remarks"></a>Comentários  

 Um atributo personalizado é armazenado como uma matriz de dados, o formato que é compreendido pelo mecanismo de metadados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
