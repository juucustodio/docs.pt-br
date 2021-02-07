---
description: 'Saiba mais sobre: estrutura CodeChunkInfo'
title: Estrutura CodeChunkInfo
ms.date: 03/30/2017
api_name:
- CodeChunkInfo
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CodeChunkInfo
helpviewer_keywords:
- CodeChunkInfo structure [.NET Framework debugging]
ms.assetid: 0f482454-8517-48de-ba7a-d7aedab13bb5
topic_type:
- apiref
ms.openlocfilehash: 017a9ee8c608d4efae98eb0a342a3371ef8ec310
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712344"
---
# <a name="codechunkinfo-structure"></a>Estrutura CodeChunkInfo

Representa uma única parte de código na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _CodeChunkInfo {  
    CORDB_ADDRESS startAddr;  
    ULONG32       length;  
} CodeChunkInfo;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`startAddr`|Um `CORDB_ADDRESS` valor que especifica o endereço inicial da parte.|  
|`length`|O tamanho, em bytes, da parte.|  
  
## <a name="remarks"></a>Comentários  

 A única parte do código é uma região de código nativo que faz parte de um objeto de código, como uma função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetCodeChunks](icordebugcode2-getcodechunks-method.md)
- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
