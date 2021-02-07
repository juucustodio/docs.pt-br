---
description: 'Saiba mais sobre: estrutura StackOverflowInfo'
title: Estrutura StackOverflowInfo
ms.date: 03/30/2017
api_name:
- StackOverflowInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StackOverflowInfo
helpviewer_keywords:
- StackOverflowInfo structure [.NET Framework hosting]
ms.assetid: 519389f2-0217-436c-99d4-93a76ebce5b5
topic_type:
- apiref
ms.openlocfilehash: cca65e4293c05b89ebefc3c6dd36a6b8898eb15f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99679388"
---
# <a name="stackoverflowinfo-structure"></a>Estrutura StackOverflowInfo

Armazena o tipo de estouro que ocorreu e informações sobre a exceção que foi lançada devido ao estouro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _StackOverflowInfo {  
    StackOverflowType   soType;  
    EXCEPTION_POINTERS  *pExceptionInfo;  
} StackOverflowInfo;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`soType`|Um valor da enumeração [StackOverflowType](stackoverflowtype-enumeration.md) que especifica o tipo de estouro.|  
|`pExceptionInfo`|Um ponteiro para um `EXCEPTION_POINTERS` objeto Win32, que contém um registro de exceção com uma descrição independente de computador de uma exceção e um registro de contexto com uma descrição dependente de computador do contexto do processador no momento da exceção.|  
  
## <a name="remarks"></a>Comentários  

 Um `StackOverflowInfo` objeto é passado para o método [IActionOnCLREvent:: OnEvent](iactiononclrevent-onevent-method.md) para `Event_StackOverflow` eventos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. idl  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de hospedagem](hosting-structures.md)
