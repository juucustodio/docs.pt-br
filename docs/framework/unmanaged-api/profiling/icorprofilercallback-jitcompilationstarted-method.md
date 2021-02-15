---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: JITCompilationStarted'
title: Método ICorProfilerCallback::JITCompilationStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCompilationStarted
helpviewer_keywords:
- JITCompilationStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCompilationStarted method [.NET Framework profiling]
ms.assetid: 31782b36-d311-4518-8f45-25f65385af5b
topic_type:
- apiref
ms.openlocfilehash: 984c19e1601f83cc0f52145403ad85affc158050
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705727"
---
# <a name="icorprofilercallbackjitcompilationstarted-method"></a>Método ICorProfilerCallback::JITCompilationStarted

Notifica o criador de perfil de que o compilador JIT (just-in-time) começou a compilar uma função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT JITCompilationStarted(  
    [in] FunctionID functionId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `functionId`  
 no A ID da função para a qual a compilação está sendo iniciada.  
  
 `fIsSafeToBlock`  
 no Um valor que indica ao criador de perfil se o bloqueio afetará a operação do tempo de execução. O valor é `true` se o bloqueio pode fazer com que o tempo de execução aguarde o thread de chamada retornar desse retorno de chamada; caso contrário, `false` .  
  
 Embora um valor de `true` não danifique o tempo de execução, ele pode distorcer os resultados de criação de perfil.  
  
## <a name="remarks"></a>Comentários  

 É possível receber mais de um par de `JITCompilationStarted` chamadas e [ICorProfilerCallback:: JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md) para cada função devido à maneira como o tempo de execução manipula construtores de classe. Por exemplo, o tempo de execução inicia o método A de compilação JIT a, mas o construtor de classe para a classe B precisa ser executado. Portanto, o tempo de execução JIT compila o construtor para a classe B e o executa. Enquanto o Construtor está em execução, ele faz uma chamada para o método A, o que faz com que o método A seja compilado em JIT novamente. Nesse cenário, a primeira compilação JIT do método A é interrompida. No entanto, ambas as tentativas de compilação JIT do método A são relatadas com eventos de compilação JIT. Se o criador de perfil substituir o código MSIL (Microsoft Intermediate Language) para o método A chamando o método [ICorProfilerInfo:: SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md) , ele deverá fazer isso para ambos os `JITCompilationStarted` eventos, mas poderá usar o mesmo bloco MSIL para ambos.  
  
 Os profileres devem dar suporte à sequência de retornos de chamada JIT nos casos em que dois threads estão realizando retornos de chamada simultaneamente. Por exemplo, thread A chama `JITCompilationStarted` . No entanto, antes de chamar Thread A `JITCompilationFinished` , thread B chama [ICorProfilerCallback:: ExceptionSearchFunctionEnter](icorprofilercallback-exceptionsearchfunctionenter-method.md) com a ID de função do retorno de chamada do thread A `JITCompilationStarted` . Pode parecer que a ID da função ainda não deve ser válida porque uma chamada para `JITCompilationFinished` ainda não foi recebida pelo criador de perfil. No entanto, em um caso como este, a ID da função é válida.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md)
