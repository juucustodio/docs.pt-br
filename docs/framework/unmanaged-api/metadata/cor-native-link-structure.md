---
description: 'Saiba mais sobre: estrutura de COR_NATIVE_LINK'
title: Estrutura COR_NATIVE_LINK
ms.date: 03/30/2017
api_name:
- COR_NATIVE_LINK
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_NATIVE_LINK
helpviewer_keywords:
- COR_NATIVE_LINK structure [.NET Framework metadata]
ms.assetid: 6ef78d3c-1c69-4141-b687-dcb065b7a74d
topic_type:
- apiref
ms.openlocfilehash: 09c715af698a0614fd4a9a17679df6908a1497a6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678569"
---
# <a name="cor_native_link-structure"></a>Estrutura COR_NATIVE_LINK

Contém informações que são usadas para vincular código nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct
{  
    BYTE        m_linkType;  
    BYTE        m_flags;  
    mdMemberRef m_entryPoint;  
} COR_NATIVE_LINK;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`m_linkType`|O tipo a ser vinculado em código nativo. Esse valor é um dos valores de [CorNativeLinkType](cornativelinktype-enumeration.md) .|  
|`m_flags`|Sinalizadores usados pelo vinculador ao vincular código nativo. Esse valor é um dos valores de [CorNativeLinkFlags](cornativelinkflags-enumeration.md) .|  
|`m_entryPoint`|O token de metadados de MemberRef que representa o ponto de entrada. O formato é `lib:entrypoint`.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de metadados](metadata-structures.md)
- [Enumeração CorNativeLinkType](cornativelinktype-enumeration.md)
- [Enumeração CorNativeLinkFlags](cornativelinkflags-enumeration.md)
