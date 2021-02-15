---
description: 'Saiba mais sobre: estrutura CustomDumpItem'
title: Estrutura CustomDumpItem
ms.date: 03/30/2017
api_name:
- CustomDumpItem
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CustomDumpItem
helpviewer_keywords:
- CustomDumpItem structure [.NET Framework hosting]
ms.assetid: fd9085ff-7beb-4c38-97f0-037cd8ba4f65
topic_type:
- apiref
ms.openlocfilehash: 9bd7b2bb59675bc01e24dc6e6d0ce524f3d35466
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716888"
---
# <a name="customdumpitem-structure"></a>Estrutura CustomDumpItem

Descreve um item a ser adicionado a um despejo personalizado no relatório de erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
struct {  
    ECustomDumpItemKind itemKind;
    union {  
        UINT_PTR pReserved;  
    }  
} CustomDumpItem;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`itemKind`|Um valor [ECustomDumpItemKind](ecustomdumpitemkind-enumeration.md) que indica o tipo de item a ser adicionado.|  
|`pReserved`|Não usado no momento. Os itens adicionados à União não devem ser maiores do que o tamanho do ponteiro. Se `struct` for necessário, você deverá alocá-lo separadamente e apontar para ele.|  
  
## <a name="remarks"></a>Comentários  

 [ICLRErrorReportingManager:: BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md) usa um parâmetro do tipo `CustomDumpItem` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. idl  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de hospedagem](hosting-structures.md)
