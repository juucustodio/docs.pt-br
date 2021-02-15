---
title: 'Alteração significativa: CreateCounterSetInstance gera InvalidOperationException se a instância já existe'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que CounterSet. CreateCounterSetInstance gera uma exceção diferente se o contador já existir.
ms.date: 11/01/2020
ms.openlocfilehash: 28042690b71f9b86e4e54748ec75467bbe232684
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760419"
---
# <a name="countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists"></a>CounterSet. CreateCounterSetInstance agora lança InvalidOperationException se a instância já existe

A partir do .NET 5,0, <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance(System.String)?displayProperty=nameWithType> o lançará um <xref:System.InvalidOperationException> em vez de um <xref:System.ArgumentException> se o conjunto de contadores já existir.

## <a name="change-description"></a>Descrição das alterações

No .NET Framework e no .NET Core 1,0 a 3,1, você pode criar uma instância do conjunto de contadores chamando <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> . No entanto, se o conjunto de contadores já existir, o método lançará uma <xref:System.ArgumentException> exceção.

No .NET 5,0 e versões posteriores, quando você chama <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> e o conjunto de contadores existe, uma <xref:System.InvalidOperationException> exceção é lançada.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Se você capturar <xref:System.ArgumentException> exceções em seu aplicativo ao chamar <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> , considere também capturar <xref:System.InvalidOperationException> exceções.

> [!NOTE]
> <xref:System.ArgumentException>Não é recomendável capturar exceções.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `M:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance(System.String)`

-->
