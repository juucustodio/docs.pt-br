---
description: 'Saiba mais sobre: enumeração de COR_PRF_CLAUSE_TYPE'
title: Enumeração COR_PRF_CLAUSE_TYPE
ms.date: 03/30/2017
api_name:
- COR_PRF_CLAUSE_TYPE
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_CLAUSE_TYPE
helpviewer_keywords:
- COR_PRF_CLAUSE_TYPE enumeration [.NET Framework profiling]
ms.assetid: f64c325a-ed3a-4aaf-b847-a88edbc4fefc
topic_type:
- apiref
ms.openlocfilehash: 413dbc0ad94e4ab670cd7cd9537bbd1735ffd7cf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649254"
---
# <a name="cor_prf_clause_type-enumeration"></a>Enumeração COR_PRF_CLAUSE_TYPE

Indica o tipo de cláusula de exceção que o código acabou de inserir ou deixar.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    COR_PRF_CLAUSE_NONE = 0,  
    COR_PRF_CLAUSE_FILTER = 1,  
    COR_PRF_CLAUSE_CATCH = 2,  
    COR_PRF_CLAUSE_FINALLY = 3,  
} COR_PRF_CLAUSE_TYPE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_PRF_CLAUSE_NONE`|A cláusula de exceção não é válida.|  
|`COR_PRF_CLAUSE_FILTER`|A cláusula de exceção é uma expressão de filtro.|  
|`COR_PRF_CLAUSE_CATCH`|A cláusula de exceção é uma `catch` instrução.|  
|`COR_PRF_CLAUSE_FINALLY`|A cláusula de exceção é uma `finally` instrução.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criando perfil de enumerações](profiling-enumerations.md)
