---
description: 'Saiba mais sobre: enumerações de criação de perfil'
title: Criando perfil de enumerações
ms.date: 03/30/2017
helpviewer_keywords:
- profiling enumerations [.NET Framework]
- enumerations [.NET Framework profiling]
- unmanaged enumerations [.NET Framework], profiling
ms.assetid: 8d5f9570-9853-4ce8-8101-df235d5b258e
ms.openlocfilehash: f202e70dd27654dd39740851549477d4a6bf77a3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736746"
---
# <a name="profiling-enumerations"></a>Criando perfil de enumerações

Esta seção descreve as enumerações não gerenciadas que a API de criação de perfis utiliza.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Enumeração COR_PRF_CLAUSE_TYPE](cor-prf-clause-type-enumeration.md)  
 Indica o tipo de cláusula de exceção que o código acabou de inserir ou deixar.  
  
 [Enumeração COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md)  
 Define os sinalizadores de geração de código que podem ser definidos com o método [ICorProfilerFunctionControl:: SetCodegenFlags](icorprofilerfunctioncontrol-setcodegenflags-method.md) .  
  
 [Enumeração COR_PRF_FINALIZER_FLAGS](cor-prf-finalizer-flags-enumeration.md)  
 Descreve o finalizador de um objeto.  
  
 [Enumeração COR_PRF_GC_GENERATION](cor-prf-gc-generation-enumeration.md)  
 Identifica uma geração de coleta de lixo.  
  
 [Enumeração COR_PRF_GC_REASON](cor-prf-gc-reason-enumeration.md)  
 Indica o motivo pelo qual essa coleta de lixo está ocorrendo.  
  
 [Enumeração COR_PRF_GC_ROOT_FLAGS](cor-prf-gc-root-flags-enumeration.md)  
 Indica propriedades de uma raiz do coletor de lixo.  
  
 [Enumeração COR_PRF_GC_ROOT_KIND](cor-prf-gc-root-kind-enumeration.md)  
 Indica o tipo de raiz do coletor de lixo que é exposto pelo retorno de chamada [ICorProfilerCallback2:: RootReferences2](icorprofilercallback2-rootreferences2-method.md) .  
  
 [Enumeração COR_PRF_HIGH_MONITOR](cor-prf-high-monitor-enumeration.md)  
 Fornece sinalizadores além daqueles encontrados na enumeração de [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) que o criador de perfil pode especificar para o método [ICorProfilerInfo5:: SetEventMask2](icorprofilerinfo5-seteventmask2-method.md) quando ele está sendo carregado.  
  
 [Enumeração COR_PRF_JIT_CACHE](cor-prf-jit-cache-enumeration.md)  
 Indica o resultado de uma busca de função armazenada em cache.  
  
 [Enumeração COR_PRF_MISC](cor-prf-misc-enumeration.md)  
 Contém valores constantes que especificam identificadores especiais.  
  
 [Enumeração COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md)  
 Especifica as propriedades de um módulo.  
  
 [Enumeração COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)  
 Contém valores usados para especificar comportamentos, recursos ou eventos que o criador de perfis deseja assinar.  
  
 [Enumeração COR_PRF_RUNTIME_TYPE](cor-prf-runtime-type-enumeration.md)  
 Contém valores que indicam a versão do runtime da linguagem comum.  
  
 [Enumeração COR_PRF_SNAPSHOT_INFO](cor-prf-snapshot-info-enumeration.md)  
 Especifica a quantidade de dados repassada com um instantâneo da pilha em cada chamada para a função `StackSnapshotCallback` do criador de perfis.  
  
 [Enumeração COR_PRF_STATIC_TYPE](cor-prf-static-type-enumeration.md)  
 Indica se um campo é estático e, em caso positivo, a qualidade estática aplicada ao campo.  
  
 [Enumeração COR_PRF_SUSPEND_REASON](cor-prf-suspend-reason-enumeration.md)  
 Indica o motivo pelo qual o runtime foi suspenso.  
  
 [Enumeração COR_PRF_TRANSITION_REASON](cor-prf-transition-reason-enumeration.md)  
 Indica o motivo para uma transição de código gerenciado para não gerenciado ou vice-versa.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Visão geral da criação de perfil](profiling-overview.md)  
  
 [Criação de perfil de interfaces](profiling-interfaces.md)  
  
 [Criando perfil de funções estáticas globais](profiling-global-static-functions.md)  
  
 [Estruturas de criação de perfil](profiling-structures.md)
