---
description: 'Saiba mais sobre: método AddFile'
title: Método AddFile
ms.date: 03/30/2017
api_name:
- IALink.AddFile
- AddFile
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddFile
helpviewer_keywords:
- AddFile method
ms.assetid: 9e707abb-f905-4568-9356-12aa21d1b11c
topic_type:
- apiref
ms.openlocfilehash: 5e1253587298b2c1559c72dced43ec70dc169090
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638620"
---
# <a name="addfile-method"></a>Método AddFile

Adiciona arquivos ao assembly. Também pode ser usado para criar módulos desvinculados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AddFile(  
    mdAssembly      AssemblyID,  
    LPCWSTR         pszFilename,  
    DWORD           dwFlags,  
    IMetaDataEmit*  pEmitter,  
    mdFile*         pFileToken  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID exclusiva do assembly a ser aumentada.  
  
 `pszFilename`  
 Nome totalmente qualificado do arquivo a ser adicionado.  
  
 `dwFlags`  
 Sinalizadores de FileDef COM+, como `ffContainsNoMetaData` e `ffWriteable` . `dwFlags` é passado para o [método definofile](../metadata/imetadataassemblyemit-definefile-method.md).  
  
 `pEmitter`  
 Interface de [interface IMetaDataEmit](../metadata/imetadataemit-interface.md) a ser usada para emitir metadados, se necessário.  
  
 `pFileToken`  
 Ponteiro para onde a ID exclusiva do arquivo adicionado será armazenada.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
