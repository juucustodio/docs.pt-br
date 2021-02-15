---
description: 'Saiba mais sobre: função CreateAssemblyCache'
title: Função CreateAssemblyCache
ms.date: 03/30/2017
api_name:
- CreateAssemblyCache
api_location:
- fusion.dll
- clr.dll
- mscorwks.dll
api_type:
- DLLExport
f1_keywords:
- CreateAssemblyCache
helpviewer_keywords:
- CreateAssemblyCache function [.NET Framework fusion]
ms.assetid: 348c7c8c-8578-46ae-97cf-480d6015c3c6
topic_type:
- apiref
ms.openlocfilehash: 1646e1d33401c557b13ae5c025f53aef48042004
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761151"
---
# <a name="createassemblycache-function"></a>Função CreateAssemblyCache

Obtém um ponteiro para uma nova instância [IAssemblyCache](iassemblycache-interface.md) que representa o cache de assembly global.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateAssemblyCache (  
    [out] IAssemblyCache  **ppAsmCache,  
    [in]  DWORD           dwReserved  
 );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppAsmCache`  
 fora O `IAssemblyCache` ponteiro retornado.  
  
 `dwReserved`  
 no Reservado para extensibilidade futura. `dwReserved` deve ser 0 (zero).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IAssemblyCache](iassemblycache-interface.md)
- [Funções estáticas globais de fusão](fusion-global-static-functions.md)
- [Cache de assemblies global](../../app-domains/gac.md)
