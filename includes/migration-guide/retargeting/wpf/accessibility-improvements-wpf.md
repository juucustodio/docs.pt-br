---
ms.openlocfilehash: 895d09e4ec39bd4a92ed1f4910da80474334d99b
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497591"
---
### <a name="accessibility-improvements-in-wpf"></a>Melhorias de acessibilidade no WPF

#### <a name="details"></a>Detalhes

**Melhorias de Alto Contraste**

- Agora, o foco do controle <xref:System.Windows.Controls.Expander> é visível. Em versões anteriores do .NET Framework, não era.
- Agora, é mais fácil ver o texto nos controles <xref:System.Windows.Controls.CheckBox> e <xref:System.Windows.Controls.RadioButton> quando eles estão selecionados do que nas versões anteriores do .NET Framework.
- A borda de um <xref:System.Windows.Controls.ComboBox> desabilitado agora é da mesma cor do texto desabilitado. Em versões anteriores do .NET Framework, não era.
- Botões desabilitados e com foco usam a cor de tema correta. Em versões anteriores do .NET Framework, eles não fizeram isso.
- O botão suspenso agora fica visível quando o <xref:System.Windows.Controls.ComboBox> estilo de um controle é definido como <xref:System.Windows.Controls.ToolBar.ComboBoxStyleKey?displayProperty=nameWithType> . Em versões anteriores do .NET Framework, não era.
- A seta de indicação de classificação em um controle <xref:System.Windows.Controls.DataGrid> agora usa cores do tema. Em versões anteriores do .NET Framework, isso não era feito.
- O estilo do hiperlink padrão agora é alterado para a cor de tema correto ao passar o mouse. Em versões anteriores do .NET Framework, isso não era feito.
- O foco do teclado em botões de opção agora fica visível. Em versões anteriores do .NET Framework, não era.
- A coluna da caixa de seleção do controle <xref:System.Windows.Controls.DataGrid> usa as cores esperadas para o feedback de foco do teclado. Em versões anteriores do .NET Framework, isso não era feito.
- os visuais de foco do teclado agora estão visíveis nos controles <xref:System.Windows.Controls.ComboBox> e <xref:System.Windows.Controls.ListBox>. Em versões anteriores do .NET Framework, não era.

**Melhorias de interação do leitor de tela**

- Agora, controles <xref:System.Windows.Controls.Expander> são anunciados corretamente como grupos (expandir/recolher) por leitores de tela.
- Agora, controles <xref:System.Windows.Controls.DataGridCell> são anunciados corretamente como uma célula de grade de dados (localizada) por leitores de tela.
- Leitores de tela agora anunciam o nome de um <xref:System.Windows.Controls.ComboBox> editável.
- <xref:System.Windows.Controls.PasswordBox> os controles não são mais anunciados como "nenhum item na exibição" pelos leitores de tela.

**Suporte para LiveRegion**

Leitores de tela, como o narrador, ajudam as pessoas a entender a interface do usuário de um aplicativo, geralmente descrevendo o elemento da interface do usuário que atualmente tem foco. No entanto, se um elemento da interface do usuário for alterado em alguma parte da tela e não tiver o foco, o usuário poderá não ser informado e poderá perder informações importantes. LiveRegions devem resolver esse problema. O desenvolvedor pode usá-las para informar o leitor de tela ou qualquer outro cliente de [Automação da interface do usuário](~/docs/framework/ui-automation/ui-automation-overview.md) de que foi feita uma alteração importante em um elemento da interface do usuário. Em seguida, o leitor de tela pode decidir como e quando informar o usuário dessa alteração. A propriedade LiveSetting também permite que o leitor de tela saiba o quanto é importante informar o usuário sobre a alteração feita na interface do usuário.

#### <a name="suggestion"></a>Sugestão

**Como aceitar ou recusar essas alterações**

Para que o aplicativo se beneficie dessas alterações, ele deve ser executado no .NET Framework 4.7.1 ou posterior. O aplicativo pode se beneficiar dessas alterações de uma das seguintes maneiras:

- Destino .NET Framework 4.7.1. Essa é a abordagem recomendada. Essas alterações de acessibilidade são habilitadas por padrão em aplicativos WPF que se destinam .NET Framework 4.7.1 ou posterior.
- Recusar os comportamentos de acessibilidade herdados adicionando a seguinte [Opção de AppContext](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) à seção `<runtime>` do arquivo de configuração de aplicativo e configurando-a como `false`, como mostra o exemplo a seguir.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7"/>
    </startup>
    <runtime>
      <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false'  -->
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
    </runtime>
  </configuration>
  ```

Aplicativos direcionados .NET Framework 4.7.1 ou posterior e que desejam preservar o comportamento de acessibilidade herdado podem optar pelo uso de recursos de acessibilidade herdados definindo explicitamente essa opção AppContext como `true` .
Para obter uma visão geral da automação da interface do usuário, consulte [visão geral da automação da IU](~/docs/framework/ui-automation/ui-automation-overview.md).

| Nome    | Valor       |
|:--------|:------------|
| Escopo   | Principal       |
| Versão | 4.7.1       |
| Tipo    | Redirecionando |

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType>
- <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType>
- <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType>
- <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType>
- <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting(System.Windows.DependencyObject,System.Windows.Automation.AutomationLiveSetting)?displayProperty=nameWithType>
- <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting(System.Windows.DependencyObject)?displayProperty=nameWithType>
- <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore?displayProperty=nameWithType>
