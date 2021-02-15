---
ms.openlocfilehash: 35dd8db243b03e1dfd6311195ec97673cf114877
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032302"
---
### <a name="razor-razortemplateengine-api-removed"></a>Razor: API RazorTemplateEngine removida

A API [RazorTemplateEngine](/dotnet/api/microsoft.aspnetcore.razor.language.razortemplateengine?view=aspnetcore-2.2) foi removida e substituída por <xref:Microsoft.AspNetCore.Razor.Language.RazorProjectEngine> .

Para obter uma discussão, consulte o problema do GitHub [dotnet/aspnetcore # 25215](https://github.com/dotnet/aspnetcore/issues/25215).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Um mecanismo de modelo pode ser criado e usado para analisar e gerar código para arquivos Razor.

#### <a name="new-behavior"></a>Novo comportamento

`RazorProjectEngine` pode ser criado e fornecido o mesmo tipo de informação `RazorTemplateEngine` para analisar e gerar código para arquivos Razor. `RazorProjectEngine` também fornece níveis extras de configuração.

#### <a name="reason-for-change"></a>Motivo da alteração

`RazorTemplateEngine` estava intimamente acoplado às implementações existentes. Esse acoplamento rígido levou a mais perguntas ao tentar configurar corretamente um pipeline de análise/geração do Razor.

#### <a name="recommended-action"></a>Ação recomendada

Use `RazorProjectEngine` em vez de `RazorTemplateEngine`. Considere os exemplos a seguir.

##### <a name="create-and-configure-the-razorprojectengine"></a>Criar e configurar o RazorProjectEngine

```csharp
RazorProjectEngine projectEngine =
    RazorProjectEngine.Create(RazorConfiguration.Default,
        RazorProjectFileSystem.Create(@"C:\source\repos\ConsoleApp4\ConsoleApp4"),
        builder =>
        {
            builder.ConfigureClass((document, classNode) =>
            {
                classNode.ClassName = "MyClassName";

                // Can also configure other aspects of the class here.
            });

            // More configuration can go here
        });
```

##### <a name="generate-code-for-a-razor-file"></a>Gerar código para um arquivo Razor

```csharp
RazorProjectItem item = projectEngine.FileSystem.GetItem(
    @"C:\source\repos\ConsoleApp4\ConsoleApp4\Example.cshtml",
    FileKinds.Legacy);
RazorCodeDocument output = projectEngine.Process(item);

// Things available
RazorSyntaxTree syntaxTree = output.GetSyntaxTree();
DocumentIntermediateNode intermediateDocument =
    output.GetDocumentIntermediateNode();
RazorCSharpDocument csharpDocument = output.GetCSharpDocument();
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- [RazorTemplateEngine](/dotnet/api/microsoft.aspnetcore.razor.language.razortemplateengine?view=aspnetcore-2.2)
- [RazorTemplateEngineOptions](/dotnet/api/microsoft.aspnetcore.razor.language.razortemplateengineoptions?view=aspnetcore-2.2)

<!--

#### Affected APIs

- `T:Microsoft.AspNetCore.Razor.Language.RazorTemplateEngine`
- `T:Microsoft.AspNetCore.Razor.Language.RazorTemplateEngineOptions`

-->
