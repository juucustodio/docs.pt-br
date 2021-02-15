---
ms.openlocfilehash: cd13e7560ee98e0c862c5e2293521c6aaa273455
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032304"
---
### <a name="razor-runtime-compilation-moved-to-a-package"></a>Razor: compilação de tempo de execução movida para um pacote

O suporte para a compilação em tempo de execução de exibições do Razor e Razor Pages foi movido para um pacote separado.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

A compilação em tempo de execução está disponível sem a necessidade de pacotes adicionais.

#### <a name="new-behavior"></a>Novo comportamento

A funcionalidade foi movida para o pacote [Microsoft. AspNetCore. Mvc. Razor. RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/) .

As APIs a seguir estavam disponíveis anteriormente no `Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions` para dar suporte à compilação em tempo de execução. As APIs agora estão disponíveis por meio do `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation.MvcRazorRuntimeCompilationOptions` .

- `RazorViewEngineOptions.FileProviders` agora é `MvcRazorRuntimeCompilationOptions.FileProviders`
- `RazorViewEngineOptions.AdditionalCompilationReferences` agora é `MvcRazorRuntimeCompilationOptions.AdditionalReferencePaths`

Além disso, o `Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange` foi removido. A recompilação em alterações de arquivo é habilitada por padrão referenciando o `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` pacote.

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi necessária para remover a dependência de estrutura compartilhada ASP.NET Core em Roslyn.

#### <a name="recommended-action"></a>Ação recomendada

Aplicativos que exigem compilação em tempo de execução ou recompilação de arquivos Razor devem executar as seguintes etapas:

1. Adicione uma referência ao `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` pacote.
1. Atualize o método do projeto `Startup.ConfigureServices` para incluir uma chamada para `AddRazorRuntimeCompilation` . Por exemplo:

    ```csharp
    services.AddMvc()
        .AddRazorRuntimeCompilation();
    ```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions?displayProperty=fullName>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions`

-->
