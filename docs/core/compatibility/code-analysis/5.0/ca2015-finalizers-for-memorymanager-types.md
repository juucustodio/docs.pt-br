---
title: 'Alteração significativa: CA2015: não defina finalizadores para tipos derivados de MemoryManager<T>'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA2015.
ms.date: 09/03/2020
ms.openlocfilehash: 5d0ba0546b5a72363559f23713c8af4bb4e26e48
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760300"
---
# <a name="warning-ca2015-do-not-define-finalizers-for-types-derived-from-memorymanagert"></a>Aviso CA2015: não defina finalizadores para tipos derivados de MemoryManager\<T>

A regra do analisador de código .NET [CA2015](/visualstudio/code-quality/ca2015) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para todos os tipos que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2015](/visualstudio/code-quality/ca2015). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

Os tipos de sinalizadores CA2015 de regra que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador. A adição de um finalizador a um tipo derivado de <xref:System.Buffers.MemoryManager%601> é provavelmente uma indicação de um bug. Ele sugere que um recurso nativo que poderia ter sido obtido em um <xref:System.Span%601> está sendo limpo, possivelmente enquanto ainda está em uso pelo <xref:System.Span%601> .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Remova a definição do finalizador. Para obter mais informações, consulte [CA2015](/visualstudio/code-quality/ca2015).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

Code analysis

-->
