---
title: 'Alteração significativa: ordem das marcas na atividade. as marcas são revertidas'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que Activity. Tags agora armazena itens na lista de acordo com a ordem em que são adicionados.
ms.date: 11/01/2020
ms.openlocfilehash: 1ff14dc1a4f7a0bf8cf9e79f3750b819f4d4a5ca
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760386"
---
# <a name="order-of-tags-in-activitytags-is-reversed"></a>Ordem das marcas na atividade. as marcas são revertidas

<xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> Agora armazena itens na lista de acordo com a ordem em que são adicionados, ou seja, o primeiro item que é adicionado é o primeiro na lista. Essa alteração foi feita para corresponder à [especificação de atributos OpenTelemetry](https://github.com/open-telemetry/opentelemetry-specification/blob/master/specification/common/common.md#attributes).

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, o <xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> armazena itens na ordem inversa da qual eles são adicionados. Ou seja, o primeiro item adicionado é o último na lista. A partir do .NET 5,0, a ordem dos itens é revertida e o primeiro item adicionado sempre é o primeiro na lista.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Se seu aplicativo tiver uma dependência na <xref:System.Diagnostics.Activity.Tags?displayProperty=nameWithType> ordem da lista e você estiver atualizando para o .net 5,0 ou posterior, você precisará alterar esta parte do seu código.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.Activity.Tags?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `P:System.Diagnostics.Activity.Tags`

-->
