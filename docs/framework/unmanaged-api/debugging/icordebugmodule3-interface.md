---
description: 'Saiba mais sobre: interface ICorDebugModule3'
title: Interface ICorDebugModule3
ms.date: 03/30/2017
api_name:
- ICorDebugModule3
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3
helpviewer_keywords:
- ICorDebugModule3 interface [.NET Framework debugging]
ms.assetid: 0b69f945-263a-4e11-8512-89d27f6ea296
topic_type:
- apiref
ms.openlocfilehash: 5b47cffb267ab97de2cd225aca2998962ba66d99
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790757"
---
# <a name="icordebugmodule3-interface"></a>Interface ICorDebugModule3

Cria um leitor de símbolos para um módulo dinâmico.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
interface ICorDebugModule3 : IUnknown  
{  
    HRESULT CreateReaderForInMemorySymbols  
      (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **  ppObj  
      );  
};  
```  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ICorDebugModule3::CreateReaderForInMemorySymbols](icordebugmodule3-createreaderforinmemorysymbols-method.md)|Cria um leitor de símbolo (normalmente [interface ISymUnmanagedReader](../diagnostics/isymunmanagedreader-interface.md)) para um módulo dinâmico.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface estende logicamente as interfaces "ICorDebugModule" e "ICorDebugModule2".  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 4,5, 4, 3,5 SP1
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRemoteTarget](icordebugremotetarget-interface.md)
- [Interface ICorDebug](icordebug-interface.md)

- [Depurando interfaces](debugging-interfaces.md)
