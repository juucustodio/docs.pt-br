---
title: Alterações significativas na análise de código
description: Lista as alterações significativas nos analisadores de código-fonte do .NET.
ms.date: 09/02/2020
ms.openlocfilehash: f1e89c90e6d91b9b3555542a0c7adf2607a76a01
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598042"
---
# <a name="code-analysis-breaking-changes"></a>Alterações significativas na análise de código

As seguintes alterações significativas estão documentadas nesta página:

| Alteração significativa | Versão introduzida |
| - | :-: |
| [CA1417: OutAttribute no parâmetro de cadeia de caracteres para P/Invoke](#ca1417-outattribute-on-string-parameter-for-pinvoke) | 5,0 |
| [CA1831: usar asspan em vez de indexadores baseados em intervalo para cadeia de caracteres](#ca1831-use-asspan-instead-of-range-based-indexers-for-string) | 5,0 |
| [CA2013: Não usar ReferenceEquals com tipos de valor](#ca2013-do-not-use-referenceequals-with-value-types) | 5,0 |
| [CA2014: Não usar stackalloc em loops](#ca2014-do-not-use-stackalloc-in-loops) | 5,0 |
| [CA2015: não definir finalizadores para tipos derivados de MemoryManager\<T>](#ca2015-do-not-define-finalizers-for-types-derived-from-memorymanagert) | 5,0 |
| [CA2247: o argumento para o Construtor TaskCompletionSource deve ser um valor TaskCreationOptions](#ca2247-argument-to-taskcompletionsource-constructor-should-be-taskcreationoptions-value) | 5,0 |

## <a name="net-50"></a>.NET 5,0

[!INCLUDE [outattributes-on-pinvoke-string-parameters](../../../includes/core-changes/codeanalysis/5.0/outattributes-on-pinvoke-string-parameters.md)]

***

[!INCLUDE [range-based-indexer-on-string](../../../includes/core-changes/codeanalysis/5.0/range-based-indexer-on-string.md)]

***

[!INCLUDE [referenceequals-on-value-types](../../../includes/core-changes/codeanalysis/5.0/referenceequals-on-value-types.md)]

***

[!INCLUDE [stackalloc-in-loops](../../../includes/core-changes/codeanalysis/5.0/stackalloc-in-loops.md)]

***

[!INCLUDE [finalizers-for-memorymanager-types](../../../includes/core-changes/codeanalysis/5.0/finalizers-for-memorymanager-types.md)]

***

[!INCLUDE [ctor-arg-should-be-taskcreationoptions](../../../includes/core-changes/codeanalysis/5.0/ctor-arg-should-be-taskcreationoptions.md)]

***
