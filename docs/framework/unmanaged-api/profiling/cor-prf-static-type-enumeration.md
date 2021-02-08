---
description: 'Saiba mais sobre: enumeração de COR_PRF_STATIC_TYPE'
title: Enumeração COR_PRF_STATIC_TYPE
ms.date: 03/30/2017
api_name:
- COR_PRF_STATIC_TYPE
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_STATIC_TYPE
helpviewer_keywords:
- COR_PRF_STATIC_TYPE enumeration [.NET Framework profiling]
ms.assetid: 441d7809-5b65-41a5-ba64-2910a8008315
topic_type:
- apiref
ms.openlocfilehash: b7171fe4e9c536d94109d46ae6cad9201a15bab9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789028"
---
# <a name="cor_prf_static_type-enumeration"></a>Enumeração COR_PRF_STATIC_TYPE

Indica se um campo é estático e, em caso positivo, a qualidade estática aplicada ao campo. Esses valores podem ser combinados usando-se a operação OR de bits para indicar que o campo tem várias qualidades estáticas diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    COR_PRF_FIELD_NOT_A_STATIC = 0x0,  
    COR_PRF_FIELD_APP_DOMAIN_STATIC = 0x1,  
    COR_PRF_FIELD_THREAD_STATIC = 0x2,  
    COR_PRF_FIELD_CONTEXT_STATIC = 0x4,  
    COR_PRF_FIELD_RVA_STATIC = 0x8  
} COR_PRF_STATIC_TYPE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`COR_PRF_FIELD_NOT_A_STATIC`|O campo não é estático.|  
|`COR_PRF_FIELD_APP_DOMAIN_STATIC`|O campo é um domínio de aplicativo estático.|  
|`COR_PRF_FIELD_THREAD_STATIC`|O campo é thread-estático.|  
|`COR_PRF_FIELD_CONTEXT_STATIC`|O campo é de contexto estático.|  
|`COR_PRF_FIELD_RVA_STATIC`|O campo é um endereço virtual relativo (RVA)-estático.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Criando perfil de enumerações](profiling-enumerations.md)
