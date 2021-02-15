---
description: 'Saiba mais sobre: Enumeração CorSymVarFlag'
title: Enumeração CorSymVarFlag
ms.date: 03/30/2017
api_name:
- CorSymVarFlag
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymVarFlag
helpviewer_keywords:
- CorSymVarFlag enumeration [.NET Framework debugging]
ms.assetid: c3f7d307-4047-4f9a-be8c-f152fca42fd0
topic_type:
- apiref
ms.openlocfilehash: 28f4b4775e20703e5dcaa7daf69affd3548aa3f2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800455"
---
# <a name="corsymvarflag-enumeration"></a>Enumeração CorSymVarFlag

Indica se uma variável é gerada pelo compilador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorSymVarFlag
{  
    VAR_IS_COMP_GEN = 1  
} CorSymVarFlag;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`VAR_IS_COMP_GEN`|Indica que a variável fornecida é gerada pelo compilador.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-enumerations.md)
