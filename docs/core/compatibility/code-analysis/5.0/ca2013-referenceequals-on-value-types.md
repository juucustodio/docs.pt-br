---
title: 'Alteração significativa: CA2013: não use ReferenceEquals com tipos de valor'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA2013.
ms.date: 09/03/2020
ms.openlocfilehash: ca2b845427eff547b996b577394c6859e30f50bf
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760302"
---
# <a name="warning-ca2013-do-not-use-referenceequals-with-value-types"></a>Aviso CA2013: não use ReferenceEquals com tipos de valor

A regra do analisador de código .NET [CA2013](/visualstudio/code-quality/ca2013) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer código em que <xref:System.Object.ReferenceEquals(System.Object,System.Object)> é usado para comparar um ou mais tipos de valor para igualdade.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2013](/visualstudio/code-quality/ca2013). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2013 localiza instâncias em que <xref:System.Object.ReferenceEquals(System.Object,System.Object)> é usada para comparar um ou mais tipos de valor para igualdade. Comparar tipos de valor para igualdade dessa maneira pode levar a resultados incorretos, porque os valores estão em caixa antes que eles sejam comparados. <xref:System.Object.ReferenceEquals(System.Object,System.Object)> retornará `false` mesmo se os valores comparados representarem a mesma instância de um tipo de valor.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Altere o código para usar um operador de igualdade apropriado, como `==` . Você não deve suprimir este aviso.

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Object.ReferenceEquals(System.Object,System.Object)`

### Category

Code analysis

-->
