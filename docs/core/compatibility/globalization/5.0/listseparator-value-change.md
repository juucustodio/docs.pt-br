---
title: 'Alteração significativa: alteração de valor de TextInfo. ListSeparator'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em que o valor padrão de TextInfo. ListSeparator foi alterado entre as versões 5,0 e 5.0.1.
ms.date: 12/10/2020
ms.openlocfilehash: 720d46c1908bcd70812f575a90f580470dbc7f32
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596452"
---
# <a name="textinfolistseparator-values-changed"></a>Valores de TextInfo. ListSeparator alterados

Os <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> valores padrão para culturas diferentes foram alterados em todos os sistemas operacionais.

## <a name="change-description"></a>Descrição das alterações

No .NET 5.0.0, como parte da [mudança do NLS para bibliotecas ICU](icu-globalization-api.md), os valores padrão <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> para diferentes culturas são alterados no Windows. Os valores de separador decimal, obtidos de componentes internacionais para Unicode (ICU), foram usados como <xref:System.Globalization.TextInfo.ListSeparator> valores. No Linux e no macOS, não havia nenhuma alteração nos <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> valores; ou seja, eles continuaram a usar valores de separadores decimais.

Para todos os sistemas operacionais no .NET 5.0.1 e versões posteriores, os valores de <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> são equivalentes aos valores que seriam obtidos do NLS. Para o Windows, isso significa que os valores são equivalentes ao que estavam em .NET Framework e no .NET Core 1,0-3,1. Para Linux e macOS, os <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> valores agora correspondem aos <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> valores para o Windows.

A tabela a seguir resume as alterações de <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> valores.

| | .NET Framework<br/>.NET Core 1,0-3,1 | .NET 5.0 | .NET 5.0.1 |
-|-|-|-
| **Windows** | Obter do NLS | Separador decimal do ICU.<br/>Pode voltar para o NLS. | Equivalente ao NLS |
| **Linux e macOS** | Separador decimal do ICU | Separador decimal do ICU | Equivalente ao NLS |

## <a name="version-introduced"></a>Versão introduzida

5.0.1

## <a name="reason-for-change"></a>Motivo da alteração

Os desenvolvedores relataram que usam a <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> propriedade ao analisar arquivos de valores separados por vírgulas (CSV) e os novos valores desapareceram <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> que a análise.

## <a name="recommended-action"></a>Ação recomendada

Se o seu código depende dos valores de separadores decimais anteriores, você pode codificar os valores desejados <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=fullName>

<!--

#### Category

- Globalization

### Affected APIs

- `P:System.Globalization.TextInfo.ListSeparator`

-->
