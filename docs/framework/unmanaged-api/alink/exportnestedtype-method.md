---
description: 'Saiba mais sobre: método ExportNestedType'
title: Método ExportNestedType
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedType
- ExportNestedType
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedType
helpviewer_keywords:
- ExportNestedType method
ms.assetid: dec7df60-4d30-47c8-99db-72e0419e5f76
topic_type:
- apiref
ms.openlocfilehash: 66cf4c3572857a0e7e99efa966cdb0b9ae2be673
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638131"
---
# <a name="exportnestedtype-method"></a>Método ExportNestedType

Especifica os tipos aninhados como exportáveis. O [método ExportType](exporttype-method.md) também pode exportar tipos aninhados, mas esse método é mais rápido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExportNestedType(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly do qual exportar.  
  
 `FileToken`  
 Token de arquivo ou assembly de arquivo que define o tipo a ser tornado exportável.  
  
 `TypeToken`  
 Tipo de token do tipo a ser tornado exportável.  
  
 `ParentType`  
 Token do tipo pai.  
  
 `pszTypename`  
 Nome de tipo totalmente qualificado para exportar.  
  
 `dwFlags`  
 `ComType` sinalizadores como `tdPublic` ou `tdNested` . Esse valor pode ser passado para o [método DefineExportedType](../metadata/imetadataassemblyemit-defineexportedtype-method.md).  
  
 `pType`  
 Recebe o token para o tipo exportado.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
