---
description: 'Saiba mais sobre o método: ICorDebugController:: Continue'
title: Método ICorDebugController::Continue
ms.date: 03/30/2017
api_name:
- ICorDebugController.Continue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Continue
helpviewer_keywords:
- Continue method [.NET Framework debugging]
- ICorDebugController::Continue method [.NET Framework debugging]
ms.assetid: 8684cd06-ad3e-48ef-832e-15320e1f43a2
topic_type:
- apiref
ms.openlocfilehash: e5858a8c287e8dd5a493a85c9f427ad8acd9ecc5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710784"
---
# <a name="icordebugcontrollercontinue-method"></a>Método ICorDebugController::Continue

Retoma a execução de threads gerenciados após uma chamada para o [método Stop](icordebugcontroller-stop-method.md).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Continue (
    [in] BOOL fIsOutOfBand
);
```

## <a name="parameters"></a>Parâmetros

`fIsOutOfBand`  
no Defina como `true` se estiver continuando com um evento fora de banda; caso contrário, defina como `false` .

## <a name="remarks"></a>Comentários

`Continue` continua o processo após uma chamada para o `ICorDebugController::Stop` método.

Ao fazer a depuração de modo misto, não chame `Continue` no thread de eventos do Win32, a menos que você esteja continuando de um evento fora de banda.

Um *evento em banda* é um evento gerenciado ou um evento não gerenciado normal durante o qual o depurador dá suporte à interação com o estado gerenciado do processo. Nesse caso, o depurador recebe o retorno de chamada [ICorDebugUnmanagedCallback::D ebugevent](icordebugunmanagedcallback-debugevent-method.md) com seu `fOutOfBand` parâmetro definido como `false` .

Um *evento fora de banda* é um evento não gerenciado durante o qual a interação com o estado gerenciado do processo é impossível enquanto o processo é interrompido devido ao evento. Nesse caso, o depurador recebe o `ICorDebugUnmanagedCallback::DebugEvent` retorno de chamada com seu `fOutOfBand` parâmetro definido como `true` .

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
