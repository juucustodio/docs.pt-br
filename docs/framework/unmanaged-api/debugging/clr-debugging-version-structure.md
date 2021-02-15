---
description: 'Saiba mais sobre: estrutura de CLR_DEBUGGING_VERSION'
title: Estrutura CLR_DEBUGGING_VERSION
ms.date: 03/30/2017
api_name:
- CLR_DEBUGGING_VERSION
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CLR_DEBUGGING_VERSION
helpviewer_keywords:
- CLR_DEBUGGING_VERSION structure [.NET Framework debugging]
ms.assetid: 4d821186-3ddf-405a-ac44-d79438a9f7f3
topic_type:
- apiref
ms.openlocfilehash: 2d274a91948b98dc309cd5670c3dd3bf6cd01e2b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772777"
---
# <a name="clr_debugging_version-structure"></a>Estrutura CLR_DEBUGGING_VERSION

Define a versão do produto do CLR (Common Language Runtime) para fins de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _CLR_DEBUGGING_VERSION  
{  
    WORD wStructVersion;
    WORD wMajor;
    WORD wMinor;
    WORD wBuild;
    WORD wRevision;
} CLR_DEBUGGING_VERSION;
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`wStructVersion`|O número de versão da estrutura|  
|`wMajor`|O número da versão principal.|  
|`wMinor`|O número da versão secundária.|  
|`wBuild`|O número de build.|  
|`wRevision`|O número de revisão.|  
  
## <a name="remarks"></a>Comentários  

 A estrutura `CLR_DEBUGGING_VERSION` é a mesma que a estrutura de COR_VERSION, no entanto, a `CLR_DEBUGGING_VERSION` estrutura fornece um campo de versão de estrutura adicional ( `wStructVersion` ). No momento, esse campo deve ser definido como zero.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
