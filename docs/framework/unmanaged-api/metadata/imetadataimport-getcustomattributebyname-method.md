---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetCustomAttributeByName'
title: Método IMetaDataImport::GetCustomAttributeByName
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetCustomAttributeByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetCustomAttributeByName
helpviewer_keywords:
- IMetaDataImport::GetCustomAttributeByName method [.NET Framework metadata]
- GetCustomAttributeByName method [.NET Framework metadata]
ms.assetid: 909aa530-2e3b-4d0a-a38a-a2750e535d7d
topic_type:
- apiref
ms.openlocfilehash: 1a9ca5f7fe13243c01c5dbcb9f49955e9ce05c26
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745473"
---
# <a name="imetadataimportgetcustomattributebyname-method"></a>Método IMetaDataImport::GetCustomAttributeByName

Obtém o atributo personalizado, dado seu nome e proprietário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCustomAttributeByName (  
   [in]  mdToken          tkObj,  
   [in]  LPCWSTR          szName,  
   [out] const void       **ppData,  
   [out] ULONG            *pcbData  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tkObj`  
 no Um token de metadados que representa o objeto que possui o atributo personalizado.  
  
 `szName`  
 no O nome do atributo personalizado.  
  
 `ppData`  
 fora Um ponteiro para uma matriz de dados que é o valor do atributo personalizado.  
  
 `pcbData`  
 fora O tamanho em bytes dos dados retornados em * `ppData` .  
  
## <a name="remarks"></a>Comentários  

 É legal definir vários atributos personalizados para o mesmo proprietário; Eles podem até mesmo ter o mesmo nome. No entanto, `GetCustomAttributeByName` retorna apenas uma instância. ( `GetCustomAttributeByName` retorna a primeira instância que ele encontra.) Para localizar todas as instâncias de um atributo personalizado, chame o método [IMetaDataImport:: EnumCustomAttributes](imetadataimport-enumcustomattributes-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
