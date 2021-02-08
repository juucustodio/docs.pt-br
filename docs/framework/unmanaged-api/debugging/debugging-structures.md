---
description: 'Saiba mais sobre: estruturas de depuração'
title: Estruturas de depuração
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged structures [.NET Framework], debugging
- debugging structures [.NET Framework]
- structures [.NET Framework debugging]
ms.assetid: 173ba2c2-ab34-49ae-b6a8-e5c49882bf05
ms.openlocfilehash: 2b3b9e3678b34a25f9bfa58fcf6913cfe95aa729
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791550"
---
# <a name="debugging-structures"></a>Estruturas de depuração

Esta seção descreve as estruturas não gerenciadas que a API de depuração usa.

## <a name="in-this-section"></a>Nesta seção

 [Estrutura de CLRDATA_ADDRESS_RANGE](clrdata-address-range-structure.md) Define um intervalo de endereços.

 [Estrutura de CLRDATA_IL_ADDRESS_MAP](clrdata-il-address-map-structure.md) Define um IL para o mapeamento de endereços

 [Estrutura de CLR_DEBUGGING_VERSION](clr-debugging-version-structure.md) Define a versão do produto do Common Language Runtime (CLR) para fins de depuração.

 [Estrutura CodeChunkInfo](codechunkinfo-structure.md) Representa uma única parte do código na memória.

 [COR_ACTIVE_FUNCTION](cor-active-function-structure.md) Contém informações sobre as funções que estão atualmente ativas em quadros de um thread.

 [Estrutura de COR_ARRAY_LAYOUT](cor-array-layout-structure.md) Fornece informações sobre o layout de um objeto de matriz na memória.

 [COR_DEBUG_IL_TO_NATIVE_MAP](cor-debug-il-to-native-map-structure.md) Contém os deslocamentos que são usados para mapear o código MSIL (Microsoft Intermediate Language) para o código nativo.

 [COR_DEBUG_STEP_RANGE](cor-debug-step-range-structure.md) Contém as informações de deslocamento de um intervalo de código.

 [Estrutura de COR_FIELD](cor-field-structure.md) Fornece informações sobre um campo em um objeto.

 [Estrutura de COR_GC_REFERENCE](cor-gc-reference-structure.md) Contém informações sobre um objeto que deve ser coletado pelo lixo.

 [Estrutura de COR_HEAPINFO](cor-heapinfo-structure.md) Fornece informações gerais sobre o heap de coleta de lixo, incluindo se ele é enumerável.

 [Estrutura de COR_HEAPOBJECT](cor-heapobject-structure.md) Fornece informações sobre um objeto no heap gerenciado.

 [COR_IL_MAP](cor-il-map-structure.md) Especifica alterações no deslocamento relativo de uma função.

 [Estrutura de COR_SEGMENT](cor-segment-structure.md) Contém informações sobre uma região de memória no heap gerenciado.

 [Estrutura de COR_TYPEID](cor-typeid-structure.md) Contém um identificador de tipo.

 [Estrutura de COR_TYPE_LAYOUT](cor-type-layout-structure.md) Fornece informações sobre o layout de um objeto na memória.

 [COR_VERSION](cor-version-structure.md) Armazena o número de versão padrão de quatro partes do Common Language Runtime.

 [Estrutura CorDebugBlockingObject](cordebugblockingobject-structure.md) Define um objeto que está bloqueando um thread e o motivo pelo qual o thread é bloqueado.

 [Estrutura CorDebugEHClause](cordebugehclause-structure.md) Representa uma cláusula de tratamento de exceção (EH) para uma determinada linguagem intermediária (IL).

 [Estrutura CorDebugExceptionObjectStackFrame](cordebugexceptionobjectstackframe-structure.md) Representa informações de quadros de pilha de um objeto de exceção.

 [Estrutura CorDebugGuidToTypeMapping](cordebugguidtotypemapping-structure.md) Mapeia um GUID de Windows Runtime para seu objeto [ICorDebugType](icordebugtype-interface.md) correspondente.

 [Estrutura DacpGetModuleAddress](dacpgetmoduleaddress-structure.md) Define o contêiner para uma solicitação de endereço de módulo.

 [Estrutura DacpMethodDescData](dacpmethoddescdata-structure.md) Define um buffer de transporte para as informações de tempo de execução de um método.

 [Estrutura DacpModuleData](dacpmoduledata-structure.md) Define um buffer de transporte para as informações de tempo de execução de um módulo.

 [Estrutura DacpReJitData](dacprejitdata-structure.md) Define as informações básicas sobre um determinado método de instrumento do criador de perfil.

 [Estrutura de StackTrace_SimpleContext](stacktrace-simplecontext-structure.md) Fornece um contexto simples que pode ser usado no lugar de uma `CONTEXT` estrutura completa.

## <a name="related-sections"></a>Seções relacionadas

 [Depurando coclasses](debugging-coclasses.md)

 [Depurando interfaces](debugging-interfaces.md)

 [Depurando funções estáticas globais](debugging-global-static-functions.md)

 [Declarando enumerações](debugging-enumerations.md)

 [Depuração](index.md)
