---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetNameFromToken'
title: Método IMetaDataImport::GetNameFromToken
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetNameFromToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetNameFromToken
helpviewer_keywords:
- GetNameFromToken method [.NET Framework metadata]
- IMetaDataImport::GetNameFromToken method [.NET Framework metadata]
ms.assetid: 32114ecf-8916-4ab2-a201-179c017344f1
topic_type:
- apiref
ms.openlocfilehash: 6195020a2b291a47e908b257896bdba64b0a40d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720846"
---
# <a name="imetadataimportgetnamefromtoken-method"></a>Método IMetaDataImport::GetNameFromToken

Obtém o nome UTF-8 do objeto referenciado pelo token de metadados especificado. Esse método é obsoleto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNameFromToken (  
   [in] mdToken      tk,  
   [out] MDUTF8CSTR  *pszUtf8NamePtr  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no O token que representa o objeto para o qual retornar o nome.  
  
 `pszUtf8NamePtr`  
 fora Um ponteiro para o nome do objeto UTF-8 no heap.  
  
## <a name="remarks"></a>Comentários  

 `GetNameFromToken` é obsoleto. Como alternativa, chame um método para obter as propriedades do tipo específico de token necessário, como `GetFieldProps` para um campo ou `GetMethodProps` para um método.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **Versões do .NET Framework:** 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
