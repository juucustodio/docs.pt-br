---
description: 'Saiba mais sobre: método ImportFileEx2'
title: Método ImportFileEx2
ms.date: 03/30/2017
api_name:
- IALink2.ImportFileEx2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFileEx2
helpviewer_keywords:
- ImportFileEx2 method
ms.assetid: 02c789fd-16fc-48c6-9619-56e87e2a37ca
topic_type:
- apiref
ms.openlocfilehash: 0968318ab7e416e56b71f2f30f2745d538d0ff8a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717999"
---
# <a name="importfileex2-method"></a>Método ImportFileEx2

Importa assemblies e módulos desvinculados. Esse método é como o [Método ImportFile](importfile-method.md), mas funciona mesmo que o arquivo que está sendo importado não exista no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ImportFileEx2(  
    LPCWSTR pszFilename,  
    LPCWSTR pszTargetName,  
    IMetaDataAssemblyImport* pAssemblyScopeIn,  
    BOOL fSmartImport,  
    DWORD dwOpenFlags,  
    mdToken* pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD* pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pszFilename`  
 Nome do arquivo a ser importado.  
  
 `pszTargetName`  
 Nome opcional do arquivo de destino.  
  
 `pAssemblyScopeIn`  
 Interface de [interface IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) de escopo de importação opcional.  
  
 `fSmartImport`  
 Se for TRUE, os irporttypes serão usados; caso contrário, a importação deverá ser executada manualmente.  
  
 `dwOpenFlags`  
 Sinalizadores a serem passados para o [método OpenScope](../metadata/imetadatadispenser-openscope-method.md).  
  
 `pImportToken`  
 Recebe uma ID exclusiva para o assembly ou arquivo.  
  
 `ppAssemblyScope`  
 Recebe interface de [interface IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) de escopo de importação de assembly. Poderá ser NULL se o arquivo não for um assembly.  
  
 `pdwCountOfScopes`  
 Recebe o número de arquivos e/ou escopos importados.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink2](ialink2-interface.md)
- [Interface IALink](ialink-interface.md)
- [API do ALink](index.md)
