---
description: 'Saiba mais sobre: método ImportFile2'
title: Método ImportFile2
ms.date: 03/30/2017
api_name:
- IALink.ImportFile2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFile2
helpviewer_keywords:
- ImportFile2 method
ms.assetid: 9a6be861-c260-4a35-acea-3372ea515a0f
topic_type:
- apiref
ms.openlocfilehash: 98da8ecf4bfc19e52c5a92e6509f6af49afbdd5f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718051"
---
# <a name="importfile2-method"></a>Método ImportFile2

Importa assemblies e módulos desvinculados. Esse método é como o [Método ImportFile](importfile-method.md), mas funciona mesmo que o arquivo que está sendo importado não exista no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ImportFile2(  
    LPCWSTR         pszFilename,  
    LPCWSTR         pszTargetName,  
    IMetaDataAssemblyImport* pAssemblyScopeIn,  
    BOOL            fSmartImport,  
    mdToken*        pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD*          pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pszFilename`  
 Nome do arquivo a ser importado.  
  
 `pszTargetName`  
 Nome de arquivo de saída opcional que pode ser usado para renomear o arquivo, pois ele está vinculado ao assembly.  
  
 `pAssemblyScopeIn`  
 Interface de [interface IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) de escopo opcional.  
  
 `fSmartImport`  
 Se for TRUE, os irporttypes serão usados; caso contrário, a importação deverá ser executada manualmente.  
  
 `pImportToken`  
 Recebe a ID do arquivo ou assembly.  
  
 `ppAssemblyScope`  
 Recebe a interface de [interface IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) . NULL se o arquivo não for um assembly.  
  
 `pdwCountOfScopes`  
 Recebe a encontrada a partir de arquivos e/ou escopos importados.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
