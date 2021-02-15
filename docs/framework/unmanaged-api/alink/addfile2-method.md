---
description: 'Saiba mais sobre: método addfile2'
title: Método AddFile2
ms.date: 03/30/2017
api_name:
- AddFile2
- IALink2.AddFile2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddFile2
helpviewer_keywords:
- AddFile2 method
ms.assetid: 03bc49bf-a89b-4fb6-a88d-97482e061195
topic_type:
- apiref
ms.openlocfilehash: d53527ecf7e8b3a99a11ea99512fbc812125de3e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638607"
---
# <a name="addfile2-method"></a>Método AddFile2

Adiciona arquivos ao assembly. Também pode ser usado para criar módulos desvinculados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AddFile2(  
    mdAssembly AssemblyID,  
    LPCWSTR pszFilename,  
    DWORD dwFlags,  
    IMetaDataEmit2* pEmitter,  
    mdFile* pFileToken  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly ao qual o arquivo é adicionado.  
  
 `pszFilename`  
 Nome do arquivo a ser adicionado.  
  
 `dwFlags`  
 `FileDef`Sinalizadores com+, como `ffContainsNoMetaData` e `ffWriteable` . `dwFlags` é passado para o [método definofile](../metadata/imetadataassemblyemit-definefile-method.md).  
  
 `pEmitter`  
 Interface para interface de [interface IMetaDataEmit2](../metadata/imetadataemit2-interface.md) .  
  
 `pFileToken`  
 Recebe a ID do arquivo que está sendo adicionado.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink2](ialink2-interface.md)
- [Interface IALink](ialink-interface.md)
- [API do ALink](index.md)
