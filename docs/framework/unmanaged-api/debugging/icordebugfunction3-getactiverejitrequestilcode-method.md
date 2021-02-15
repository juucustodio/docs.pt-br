---
description: 'Saiba mais sobre o método: ICorDebugFunction3:: GetActiveReJitRequestILCode'
title: ICorDebugFunction3::Método GetActiveReJitRequestILCode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugFunction3.GetActiveReJitRequestILCode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 88584574-ade5-45b2-9778-489ed5c4dd7f
topic_type:
- apiref
ms.openlocfilehash: 9225c5cdf97395b7e1b11c61d653cab8d52031c6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692115"
---
# <a name="icordebugfunction3getactiverejitrequestilcode-method"></a>ICorDebugFunction3::Método GetActiveReJitRequestILCode

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Obtém um ponteiro de interface para um [ICorDebugILCode](icordebugilcode-interface.md) que contém o Il de uma solicitação de ReJIT ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetActiveReJitRequestILCode(  
   ICorDebugILCode **ppReJitedILCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppReJitedILCode`  
 Um ponteiro para a IL de uma solicitação ReJIT ativa.  
  
## <a name="remarks"></a>Comentários  

 Se o método representado por este objeto `ICorDebugFunction3` tiver uma solicitação ReJIT ativa, `ppReJitedILCode` retornará um ponteiro para sua IL. Se não houver nenhuma solicitação ativa, que é um caso comum, `ppReJitedILCode` será **NULL**.  
  
 Uma solicitação ReJIT torna-se ativa logo após a execução retornar da chamada do método [ICorProfilerCallback4:: GetReJITParameters](../profiling/icorprofilercallback4-getrejitparameters-method.md) . Pode ainda não estar compilada em JIT e threads podem ainda estar em execução na versão original do código. Uma solicitação ReJIT se torna inativa durante a chamada do criador de perfil para o método [ICorProfilerInfo4:: RequestRevert](../profiling/icorprofilerinfo4-requestrevert-method.md) . Mesmo depois que a IL é revertida, um thread ainda pode estar em execução no código ReJIT (recompilado por JIT).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugFunction3](icordebugfunction3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [ReJIT: um guia de How-To](/archive/blogs/davbr/rejit-a-how-to-guide)
