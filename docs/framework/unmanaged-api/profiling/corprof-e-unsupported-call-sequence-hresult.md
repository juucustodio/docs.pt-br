---
description: 'Saiba mais sobre: CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT'
title: CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT
ms.date: 03/30/2017
f1_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE
helpviewer_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT [.NET Framework profiling]
ms.assetid: f2fc441f-d62e-4f72-a011-354ea13c8c59
ms.openlocfilehash: 05f5364768d04b571e8901362d9ca2d26ecaa15d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753296"
---
# <a name="corprof_e_unsupported_call_sequence-hresult"></a>CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT

O CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT foi introduzido na versão .NET Framework 2,0. .NET Framework 4 retorna esse HRESULT em dois cenários:  
  
- Quando um criador de perfil de seqüestro redefine forçosamente o contexto de registro de um thread em um momento arbitrário para que o thread tente acessar as estruturas que estão em um estado inconsistente.  
  
- Quando um criador de perfil tenta chamar um método informativo que dispara a coleta de lixo de um método de retorno de chamada que proíbe a coleta de lixo.  
  
Esses dois cenários são discutidos nas seções a seguir.  
  
## <a name="hijacking-profilers"></a>Profileres de seqüestro  

  (Esse cenário é basicamente um problema com os profileres de seqüestro, embora haja casos em que os profileres de não-seqüestro possam ver esse HRESULT.)  
  
 Nesse cenário, um criador de perfil de seqüestro redefine forçosamente o contexto de registro de um thread em um momento arbitrário para que o thread possa inserir o código do criador de perfil ou reinserir o Common Language Runtime (CLR) por meio de um método [ICorProfilerInfo](icorprofilerinfo-interface.md) .  
  
 Muitas das IDs que a API de criação de perfil fornece aponta para estruturas de dados no CLR. Muitas `ICorProfilerInfo` chamadas simplesmente lêem informações dessas estruturas de dados e as transmitem de volta. No entanto, o CLR pode alterar as coisas nessas estruturas à medida que é executado e pode usar bloqueios para fazer isso. Suponha que o CLR já esteja mantendo (ou tentando adquirir) um bloqueio no momento em que o criador de perfil seqüestrar o thread. Se o thread reinserir o CLR e tentar obter mais bloqueios ou inspecionar estruturas que estavam no processo de ser modificado, essas estruturas poderão estar em um estado inconsistente. Deadlocks e violações de acesso podem ocorrer facilmente nessas situações.  
  
 Em geral, quando um profiler sem seqüestro executa o código dentro de um método [ICorProfilerCallback](icorprofilercallback-interface.md) e chama um `ICorProfilerInfo` método com parâmetros válidos, ele não deve ter um deadlock ou receber uma violação de acesso. Por exemplo, o código do criador de perfil que é executado dentro do método [ICorProfilerCallback:: ClassLoadFinished](icorprofilercallback-classloadfinished-method.md) pode solicitar informações sobre a classe chamando o método [ICorProfilerInfo2:: GetClassIDInfo2](icorprofilerinfo2-getclassidinfo2-method.md) . O código pode receber um CORPROF_E_DATAINCOMPLETE HRESULT para indicar que as informações não estão disponíveis. No entanto, ele não causará deadlock ou receberá uma violação de acesso. Essas chamadas em `ICorProfilerInfo` são consideradas síncronas, pois são feitas de um `ICorProfilerCallback` método.  
  
 No entanto, um thread gerenciado que executa o código que não está dentro de um `ICorProfilerCallback` método é considerado como tendo uma chamada assíncrona. No .NET Framework versão 1, era difícil determinar o que pode acontecer em uma chamada assíncrona. A chamada pode travar, falhar ou dar uma resposta inválida. .NET Framework versão 2,0 introduziu algumas verificações simples para ajudá-lo a evitar esse problema. No .NET Framework 2,0, se você chamar uma função não segura `ICorProfilerInfo` de forma assíncrona, ela falhará com um CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT.  
  
 Em geral, as chamadas assíncronas não são seguras. No entanto, os métodos a seguir são seguros e oferecem suporte especificamente a chamadas assíncronas:  
  
- [GetEventMask](icorprofilerinfo-geteventmask-method.md)  
  
- [SetEventMask](icorprofilerinfo-seteventmask-method.md)  
  
- [GetCurrentThreadID](icorprofilerinfo-getcurrentthreadid-method.md)  
  
- [GetThreadContext](icorprofilerinfo-getthreadcontext-method.md)  
  
- [GetThreadAppDomain](icorprofilerinfo2-getthreadappdomain-method.md)  
  
- [GetFunctionFromIP](icorprofilerinfo-getfunctionfromip-method.md)  
  
- [GetFunctionInfo](icorprofilerinfo-getfunctioninfo-method.md)  
  
- [GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md)  
  
- [GetCodeInfo](icorprofilerinfo-getcodeinfo-method.md)  
  
- [GetCodeInfo2](icorprofilerinfo2-getcodeinfo2-method.md)  
  
- [GetModuleInfo](icorprofilerinfo-getmoduleinfo-method.md)  
  
- [GetClassIDInfo](icorprofilerinfo-getclassidinfo-method.md)  
  
- [GetClassIDInfo2](icorprofilerinfo2-getclassidinfo2-method.md)  
  
- [IsArrayClass](icorprofilerinfo-isarrayclass-method.md)  
  
- [SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)  
  
- [DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md)  
  
 Para obter mais informações, consulte a entrada [por que temos CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](/archive/blogs/davbr/why-we-have-corprof_e_unsupported_call_sequence) no blog da API de criação de perfil do CLR.  
  
## <a name="triggering-garbage-collections"></a>Disparando coleções de lixo  

 Esse cenário envolve um criador de perfil que está sendo executado dentro de um método de retorno de chamada (por exemplo, um dos `ICorProfilerCallback` métodos) que proíbe a coleta de lixo. Se o criador de perfil tentar chamar um método informativo (por exemplo, um método na `ICorProfilerInfo` interface) que possa disparar uma coleta de lixo, o método informativo falhará com um CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT.  
  
 A tabela a seguir exibe os métodos de retorno de chamada que proíbem coletas de lixo e métodos informativos que podem disparar coletas de lixo. Se o criador de perfil for executado dentro de um dos métodos de retorno de chamada listados e chamar um dos métodos informativos listados, esse método informativo falhará com um CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT.  
  
|Métodos de retorno de chamada que proíbem coletas de lixo|Métodos informativos que disparam coletas de lixo|  
|------------------------------------------------------|------------------------------------------------------------|  
|[ThreadAssignedToOSThread](icorprofilercallback-threadassignedtoosthread-method.md)<br /><br /> [ExceptionUnwindFunctionEnter](icorprofilercallback-exceptionunwindfunctionenter-method.md)<br /><br /> [ExceptionUnwindFunctionLeave](icorprofilercallback-exceptionunwindfunctionleave-method.md)<br /><br /> [ExceptionUnwindFinallyEnter](icorprofilercallback-exceptionunwindfinallyenter-method.md)<br /><br /> [ExceptionUnwindFinallyLeave](icorprofilercallback-exceptionunwindfinallyleave-method.md)<br /><br /> [ExceptionCatcherEnter](icorprofilercallback-exceptioncatcherenter-method.md)<br /><br /> [RuntimeSuspendStarted](icorprofilercallback-runtimesuspendstarted-method.md)<br /><br /> [RuntimeSuspendFinished](icorprofilercallback-runtimesuspendfinished-method.md)<br /><br /> [RuntimeSuspendAborted](icorprofilercallback-runtimesuspendaborted-method.md)<br /><br /> [RuntimeThreadSuspended](icorprofilercallback-runtimethreadsuspended-method.md)<br /><br /> [RuntimeThreadResumed](icorprofilercallback-runtimethreadresumed-method.md)<br /><br /> [MovedReferences](icorprofilercallback-movedreferences-method.md)<br /><br /> [Objectreferências](icorprofilercallback-objectreferences-method.md)<br /><br /> [ObjectsAllocatedByClass](icorprofilercallback-objectsallocatedbyclass-method.md)<br /><br /> [RootReferences2](icorprofilercallback-rootreferences-method.md)<br /><br /> [HandleCreated](icorprofilercallback2-handlecreated-method.md)<br /><br /> [HandleDestroyed](icorprofilercallback2-handledestroyed-method.md)<br /><br /> [GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md)<br /><br /> [GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)|[GetILFunctionBodyAllocator](icorprofilerinfo-getilfunctionbodyallocator-method.md)<br /><br /> [SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md)<br /><br /> [SetILInstrumentedCodeMap](icorprofilerinfo-setilinstrumentedcodemap-method.md)<br /><br /> [ForceGC](icorprofilerinfo-forcegc-method.md)<br /><br /> [GetClassFromToken](icorprofilerinfo-getclassfromtoken-method.md)<br /><br /> [GetClassFromTokenAndTypeArgs](icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)<br /><br /> [GetFunctionFromTokenAndTypeArgs](icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)<br /><br /> [GetAppDomainInfo](icorprofilerinfo-getappdomaininfo-method.md)<br /><br /> [EnumModules](icorprofilerinfo3-enummodules-method.md)<br /><br /> [RequestProfilerDetach](icorprofilerinfo3-requestprofilerdetach-method.md)<br /><br /> [GetAppDomainsContainingModule](icorprofilerinfo3-getappdomainscontainingmodule-method.md)|  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Interface ICorProfilerCallback2](icorprofilercallback2-interface.md)
- [Interface ICorProfilerCallback3](icorprofilercallback3-interface.md)
- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Interface ICorProfilerInfo2](icorprofilerinfo2-interface.md)
- [Interface ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
