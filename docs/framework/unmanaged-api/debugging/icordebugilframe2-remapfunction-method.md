---
description: 'Saiba mais sobre o método: ICorDebugILFrame2:: RemapFunction'
title: Método ICorDebugILFrame2::RemapFunction
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame2.RemapFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame2::RemapFunction
helpviewer_keywords:
- ICorDebugILFrame2::RemapFunction method [.NET Framework debugging]
- RemapFunction method [.NET Framework debugging]
ms.assetid: dd639ba0-f77b-426d-9ff6-f92706840348
topic_type:
- apiref
ms.openlocfilehash: d8a6c7f966488e7b74a9661e3a18b5248df7400b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791277"
---
# <a name="icordebugilframe2remapfunction-method"></a>Método ICorDebugILFrame2::RemapFunction

Remapeia uma função editada especificando o novo deslocamento da MSIL (Microsoft Intermediate Language)  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RemapFunction (  
    [in] ULONG32      newILOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `newILOffset`  
 no O novo deslocamento MSIL do quadro de pilha no qual o ponteiro de instrução deve ser colocado. Esse valor deve ser um ponto de sequência.  
  
 É responsabilidade do chamador garantir a validade desse valor. Por exemplo, o deslocamento de MSIL não será válido se estiver fora dos limites da função.  
  
## <a name="remarks"></a>Comentários  

 Quando a função de um quadro é editada, o depurador pode chamar o `RemapFunction` método para alternar a versão mais recente da função do quadro para que possa ser executado. A execução do código será iniciada no deslocamento de MSIL fornecido.  
  
> [!NOTE]
> Chamar `RemapFunction` , como chamar [ICorDebugILFrame:: SetIP](icordebugilframe-setip-method.md), invalidará imediatamente todas as interfaces de depuração relacionadas à geração de um rastreamento de pilha para o thread. Essas interfaces incluem [ICorDebugChain](icordebugchain-interface.md), ICorDebugILFrame, ICorDebugInternalFrame e ICorDebugNativeFrame.  
  
 O `RemapFunction` método pode ser chamado somente no contexto do quadro atual e apenas em um dos seguintes casos:  
  
- Após o recebimento de um retorno de chamada [ICorDebugManagedCallback2:: FunctionRemapOpportunity](icordebugmanagedcallback2-functionremapopportunity-method.md) que ainda não foi continuado.  
  
- Enquanto a execução do código é interrompida devido a um evento [ICorDebugManagedCallback:: EditAndContinueRemap](icordebugmanagedcallback-editandcontinueremap-method.md) para esse quadro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
