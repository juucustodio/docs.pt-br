---
description: 'Saiba mais sobre o método: ICorDebugThread:: EnumerateChains'
title: Método ICorDebugThread::EnumerateChains
ms.date: 03/30/2017
api_name:
- ICorDebugThread.EnumerateChains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::EnumerateChains
helpviewer_keywords:
- EnumerateChains method [.NET Framework debugging]
- ICorDebugThread::EnumerateChains method [.NET Framework debugging]
ms.assetid: ec00bc21-117e-4acd-9301-2cfafd5be8d3
topic_type:
- apiref
ms.openlocfilehash: b9184a1b298e1d29970c5e56ceca76715b0ed096
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659290"
---
# <a name="icordebugthreadenumeratechains-method"></a>Método ICorDebugThread::EnumerateChains

Obtém um ponteiro de interface para um enumerador ICorDebugChainEnum que contém todas as cadeias de pilha neste objeto ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateChains (  
    [out] ICorDebugChainEnum **ppChains  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppChains`  
 fora Um ponteiro para o endereço de um `ICorDebugChainEnum` objeto que permite a enumeração de todas as cadeias de pilha nesse thread, iniciando na cadeia ativa (ou seja, a mais recente).  
  
## <a name="remarks"></a>Comentários  

 A cadeia de pilha representa a pilha de chamadas física para o thread. As circunstâncias a seguir criam um limite de cadeia de pilha:  
  
- Uma transição gerenciada para não gerenciada ou não gerenciada para gerenciada.  
  
- Uma alternância de contexto.  
  
- Um seqüestro de depurador de um thread de usuário.  
  
 No caso simples de um thread que está executando código puramente gerenciado em um único contexto, uma correspondência um-para-um existirá entre threads e cadeias de pilha.  
  
 Um depurador pode querer reorganizar as pilhas de chamadas físicas de todos os threads em pilhas de chamadas lógicas. Isso envolveria classificar todas as cadeias de threads por seus relacionamentos de chamador/receptor e reagrupá-las.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
