---
ms.openlocfilehash: 4bc8db52efdfe483acb4f6b6e33c4fa7716e0b79
ms.sourcegitcommit: 261e0c98a111357692b3b63c596edf0cacf72991
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90770788"
---
### <a name="svctraceviewer-combobox-high-contrast-change"></a>Alteração de alto contraste de ComboBox de svcTraceViewer

#### <a name="details"></a>Detalhes

Na [ferramenta Visualizador de Rastreamento de Serviço da Microsoft](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), os controles ComboBox não eram exibidos na cor correta em determinados temas de alto contraste. O problema foi corrigido no .NET Framework 4.7.2. No entanto, devido aos requisitos de compatibilidade com versões anteriores do SDK do .NET Framework, a correção não estava visível para clientes por padrão. O .NET 4.8 revela essa alteração adicionando os seguintes [comutadores de configuração do AppContext](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) ao arquivo svcTraceViewer.exe.config:

```xml
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
```

#### <a name="suggestion"></a>Sugestão

Se não quiser que a alteração do comportamento de alto contraste seja alterada, você poderá desabilitá-la removendo a seguinte seção do arquivo de svcTraceViewer.exe.config:

```xml
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
```

| Nome    | Valor   |
|:--------|:--------|
| Escopo   | Microsoft Edge    |
| Versão | 4.8     |
| Tipo    | Runtime |

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
