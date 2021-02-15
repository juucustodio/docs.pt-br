---
description: 'Saiba mais sobre: método ImportFileEx'
title: Método ImportFileEx
ms.date: 03/30/2017
api_name:
- IALink2.ImportFileEx
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFileEx
helpviewer_keywords:
- ImportFileEx method
ms.assetid: ad276f3f-b303-46ac-97e0-66a377adaa4f
topic_type:
- apiref
ms.openlocfilehash: a8a7e5a142091bf7cc93f50a4ae20c59d800f3ff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718012"
---
# <a name="importfileex-method"></a>Método ImportFileEx

Importações indicadas módulo de assembly ou não associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ImportFileEx(  
    LPCWSTR pszFilename,  
    LPCWSTR pszTargetName,  
    BOOL fSmartImport,  
    DWORD dwOpenFlags,  
    mdToken* pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD* pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pszFilename`  
 Nome totalmente qualificado do arquivo do qual importar.  
  
 `pszTargetName`  
 Nome opcional do arquivo de destino.  
  
 `fSmartImport`  
 Se for TRUE, os irporttypes serão usados; caso contrário, a importação deverá ser executada manualmente.  
  
 `dwOpenFlags`  
 Sinalizadores a serem passados para o [método OpenScope](../metadata/imetadatadispenser-openscope-method.md).  
  
 `pImportToken`  
 Recebe a ID do arquivo que está sendo importado.  
  
 `ppAssemblyScope`  
 Recebe interface de [interface IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) de escopo de importação de assembly. Será definido como NULL se o arquivo não for um assembly.  
  
 `pdwCountOfScopes`  
 Recebe a contagem de escopos e/ou arquivos importados.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink2](ialink2-interface.md)
- [Interface IALink](ialink-interface.md)
- [API do ALink](index.md)
