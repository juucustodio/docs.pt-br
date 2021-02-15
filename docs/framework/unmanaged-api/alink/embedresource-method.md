---
description: 'Saiba mais sobre: método EmbedResource'
title: Método EmbedResource
ms.date: 03/30/2017
api_name:
- IALink.EmbedResource
- EmbedResource
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EmbedResource
helpviewer_keywords:
- EmbedResource method
ms.assetid: 667bd954-6dc6-4020-a3cb-0e8224179993
topic_type:
- apiref
ms.openlocfilehash: f7896172e7416048352788caf7e092096924b7af
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638347"
---
# <a name="embedresource-method"></a>Método EmbedResource

Declara um recurso inserido. Esse método não insere o recurso de fato.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EmbedResource(  
    mdAssembly  AssemblyID,  
    mdToken     FileToken,  
    LPCWSTR     pszResourceName,  
    DWORD       dwOffset,  
    DWORD       dwFlags  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly.  
  
 `FileToken`  
 Token do arquivo ou ID do assembly do arquivo que contém o recurso.  
  
 `pszResourceName`  
 Nome do recurso.  
  
 `dwOffset`  
 Deslocamento do recurso de RVA.  
  
 `dwFlags`  
 Sinalizadores de acessibilidade, como `mrPublic` e `mrPrivate` . Esses sinalizadores podem ser passados para o [método DefineExportedType](../metadata/imetadataassemblyemit-defineexportedtype-method.md).  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
