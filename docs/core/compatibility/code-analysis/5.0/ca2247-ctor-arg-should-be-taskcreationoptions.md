---
title: 'Alteração significativa: CA2247: o argumento para o Construtor TaskCompletionSource deve ser um valor TaskCreationOptions'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA2247.
ms.date: 09/03/2020
ms.openlocfilehash: 323fd5a05da4dfeb68ef75d88d5d293ba01c8ade
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760405"
---
# <a name="warning-ca2247-argument-to-taskcompletionsource-constructor-should-be-taskcreationoptions-value"></a>Aviso CA2247: o argumento para o Construtor TaskCompletionSource deve ser um valor TaskCreationOptions

A regra do analisador de código .NET [CA2247](/visualstudio/code-quality/ca2247) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para chamadas para o <xref:System.Threading.Tasks.TaskCompletionSource%601> Construtor que passa um argumento do tipo <xref:System.Threading.Tasks.TaskContinuationOptions> .

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2247](/visualstudio/code-quality/ca2247). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2247 localiza chamadas para o <xref:System.Threading.Tasks.TaskCompletionSource%601> Construtor que passa um argumento do tipo <xref:System.Threading.Tasks.TaskContinuationOptions> . O <xref:System.Threading.Tasks.TaskCompletionSource%601> tipo tem um construtor que aceita um <xref:System.Threading.Tasks.TaskCreationOptions> valor e outro construtor que aceita um <xref:System.Object> . Se você passar acidentalmente um <xref:System.Threading.Tasks.TaskContinuationOptions> valor em vez de um <xref:System.Threading.Tasks.TaskCreationOptions> valor, o construtor com o <xref:System.Object> parâmetro será chamado em tempo de execução. Seu código será compilado e executado, mas não terá o comportamento pretendido.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Substitua o <xref:System.Threading.Tasks.TaskContinuationOptions> argumento pelo valor correspondente <xref:System.Threading.Tasks.TaskCreationOptions> . Não suprimir este aviso, pois quase sempre realça um bug em seu código. Para obter mais informações, consulte [CA2247](/visualstudio/code-quality/ca2247).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Threading.Tasks.TaskCompletionSource%601.%23ctor(System.Object)>

<!--

### Affected APIs

- ``M:System.Threading.Tasks.TaskCompletionSource`1.#ctor(System.Object)``

### Category

Code analysis

-->
