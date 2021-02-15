---
description: 'Saiba mais sobre: criação de perfil de funções estáticas globais'
title: Criando perfil de funções estáticas globais
ms.date: 03/30/2017
helpviewer_keywords:
- global static functions [.NET Framework profiling]
- profiling global static functions [.NET Framework]
- unmanaged global static functions [.NET Framework], profiling
ms.assetid: 08a13a57-dc49-488d-b937-31e3051fda97
ms.openlocfilehash: 86e4b6bda73b0783f5f95e4e7dbc24f1ccccb130
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646368"
---
# <a name="profiling-global-static-functions"></a>Criando perfil de funções estáticas globais

Esta seção descreve as funções de API não gerenciadas que a API de criação de perfil usa.  
  
## <a name="in-this-section"></a>Nesta seção  
  
## <a name="net-framework-version-1-profiling-functions"></a>Funções de criação de perfil .NET Framework versão 1  

 [Função FunctionEnter](functionenter-function.md)  
 Notifica o criador de perfil que o controle está sendo passado para uma função. Preterido no .NET Framework 2,0.  
  
 [Função FunctionLeave](functionleave-function.md)  
 Notifica o criador de perfil de que uma função está prestes a retornar ao chamador. Preterido no .NET Framework 2,0.  
  
 [Função FunctionTailcall](functiontailcall-function.md)  
 Notifica o criador de perfil de que a função atualmente em execução está prestes a executar uma chamada tail para outra função. Preterido no .NET Framework 2,0.  
  
## <a name="net-framework-version-2-profiling-functions"></a>Funções de criação de perfil .NET Framework versão 2  

 [Função FunctionIDMapper](functionidmapper-function.md)  
 Notifica o criador de perfil de que o identificador fornecido de uma função pode ser remapeado para uma ID alternativa a ser usada nos retornos de chamada [FunctionEnter2](functionenter2-function.md), [FunctionLeave2](functionleave2-function.md)e [FunctionTailcall2](functiontailcall2-function.md) para essa função. Também permite que o criador de perfil indique se deseja receber retornos de chamada para essa função  
  
 [Função FunctionEnter2](functionenter2-function.md)  
 Notifica o criador de perfil que o controle está sendo passado para uma função e fornece informações sobre o quadro de pilha e os argumentos de função. Preterido no .NET Framework 4.  
  
 [Função FunctionLeave2](functionleave2-function.md)  
 Notifica o criador de perfil de que uma função está prestes a retornar ao chamador e fornece informações sobre o quadro de pilha e o valor de retorno da função. Preterido no .NET Framework 4.  
  
 [Função FunctionTailcall2](functiontailcall2-function.md)  
 Notifica o criador de perfil de que a função atualmente em execução está prestes a executar uma chamada tail para outra função e fornece informações sobre o registro de ativação. Preterido no .NET Framework 4.  
  
 [Função StackSnapshotCallback](stacksnapshotcallback-function.md)  
 Fornece ao criador de perfil informações sobre cada quadro gerenciado e cada execução de quadros não gerenciados na pilha durante uma movimentação de pilha, que é iniciada pelo método [ICorProfilerInfo2::D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md) .  
  
## <a name="net-framework-version-4-profiling-functions"></a>Funções de criação de perfil .NET Framework versão 4  

 [Função FunctionIDMapper2](functionidmapper2-function.md)  
 Notifica o criador de perfil de que o identificador fornecido de uma função pode ser remapeado para uma ID alternativa a ser usada nos retornos de chamada [FunctionEnter3](functionenter3-function.md), [FunctionLeave3](functionleave3-function.md)e [FunctionTailcall3](functiontailcall3-function.md)ou[FunctionEnter3WithInfo](functionenter3withinfo-function.md), [FunctionLeave3WithInfo](functionleave3withinfo-function.md)e [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md) para essa função. Também permite que o criador de perfil indique se deseja receber retornos de chamada para essa função.  
  
 `FunctionIDMapper2` estende a função [FunctionIDMapper](functionidmapper-function.md) com um `clientData` parâmetro, que os profileres podem usar para fazer a ambiguidade entre os tempos de execução.  
  
 [Função FunctionEnter3](functionenter3-function.md)  
 Notifica o criador de perfil que o controle está sendo passado para uma função.  
  
 [Função FunctionEnter3WithInfo](functionenter3withinfo-function.md)  
 Notifica o criador de perfil que o controle está sendo passado para uma função e fornece um identificador que pode ser passado para [ICorProfilerInfo3:: GetFunctionEnter3Info](icorprofilerinfo3-getfunctionenter3info-method.md) para recuperar o quadro de pilha e os argumentos de função.  
  
 [Função FunctionLeave3](functionleave3-function.md)  
 Notifica o criador de perfil que o controle está sendo retornado de uma função.  
  
 [Função FunctionLeave3WithInfo](functionleave3withinfo-function.md)  
 Notifica o criador de perfil que o controle está sendo retornado de uma função e fornece um identificador que pode ser passado para [ICorProfilerInfo3:: GetFunctionLeave3Info](icorprofilerinfo3-getfunctionleave3info-method.md) para recuperar o quadro de pilha e o valor de retorno.  
  
 [Função FunctionTailcall3](functiontailcall3-function.md)  
 Notifica o criador de perfil de que a função atualmente em execução está prestes a executar uma chamada tail para outra função.  
  
 [Função FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)  
 Notifica o criador de perfil de que a função atualmente em execução está prestes a executar uma chamada tail para outra função e fornece um identificador que pode ser passado para [ICorProfilerInfo3:: GetFunctionTailcall3Info](icorprofilerinfo3-getfunctiontailcall3info-method.md) para recuperar o quadro de pilha.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Visão geral da criação de perfil](profiling-overview.md)  
  
 [Criação de perfil de interfaces](profiling-interfaces.md)  
  
 [Criando perfil de enumerações](profiling-enumerations.md)  
  
 [Estruturas de criação de perfil](profiling-structures.md)
