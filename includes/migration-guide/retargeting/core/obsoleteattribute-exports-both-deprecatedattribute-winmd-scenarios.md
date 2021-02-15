---
ms.openlocfilehash: 7d7424b3ca0d295022999e95ed9862b5226b6220
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606804"
---
### <a name="obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>ObsoleteAttribute exporta ObsoleteAttribute e DeprecatedAttribute em cenários WinMD

#### <a name="details"></a>Detalhes

Quando você cria uma biblioteca de Metadados do Windows (arquivo .winmd), o atributo <xref:System.ObsoleteAttribute?displayProperty=fullName> é exportado como <xref:System.ObsoleteAttribute?displayProperty=fullName> e [ Windows.Foundation.DeprecatedAttribute](/uwp/api/windows.foundation.metadata.deprecatedattribute).

#### <a name="suggestion"></a>Sugestão

A recompilação do código-fonte existente que usa o atributo <xref:System.ObsoleteAttribute?displayProperty=fullName> pode gerar avisos durante o consumo desse código do C++/CX ou JavaScript. Não é recomendável aplicar <xref:System.ObsoleteAttribute?displayProperty=fullName> e [Windows.Foundation.DeprecatedAttribute](/uwp/api/windows.foundation.metadata.deprecatedattribute) ao código em assemblies gerenciados, isso pode gerar avisos de compilação.

| Name    | Valor       |
|:--------|:------------|
| Escopo   | Microsoft Edge        |
| Versão | 4.5.1       |
| Tipo    | Redirecionando |
