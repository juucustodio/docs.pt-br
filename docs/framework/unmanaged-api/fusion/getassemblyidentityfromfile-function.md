---
description: 'Saiba mais sobre: função GetAssemblyIdentityFromFile'
title: Função GetAssemblyIdentityFromFile
ms.date: 03/30/2017
api_name:
- GetAssemblyIdentityFromFile
api_location:
- fusion.dll
- clr.dll
- mscorwks.dll
api_type:
- COM
f1_keywords:
- GetAssemblyIdentityFromFile
helpviewer_keywords:
- GetAssemblyIdentityFromFile function [.NET Framework fusion]
ms.assetid: 2c32da53-76c7-4048-84d0-d05207333004
topic_type:
- apiref
ms.openlocfilehash: 8832e03182a5652c938404c99115fa8059439d1d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761012"
---
# <a name="getassemblyidentityfromfile-function"></a>Função GetAssemblyIdentityFromFile

Obtém um ponteiro para um `IUnknown` objeto com o especificado `IID` no assembly no caminho do arquivo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAssemblyIdentityFromFile (  
    [in]  LPCWSTR   pwzFilePath,  
    [in]  REFIID    riid,  
    [out] IUnknown  **ppIdentity  
 );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzFilePath`  
 no Um caminho válido para o assembly solicitado.  
  
 `riid`  
 no O `IID` da interface a ser retornada.  
  
 `ppIdentity`  
 fora O ponteiro de interface retornado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [IUnknown](/cpp/atl/iunknown)
- [Funções estáticas globais de fusão](fusion-global-static-functions.md)
