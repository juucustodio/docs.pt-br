---
ms.openlocfilehash: 8395428e1729a00fc1af72cf53fe689ee95b5fdf
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032294"
---
### <a name="mvc-precompilation-tool-deprecated"></a>MVC: ferramenta de pré-compilação preterida

No ASP.NET Core 1,1, o `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacote (ferramenta de pré-compilação Mvc) foi introduzido para adicionar suporte à compilação de tempo de publicação de arquivos Razor (arquivos *. cshtml* ). No ASP.NET Core 2,1, o [SDK do Razor](/aspnet/core/razor-pages/sdk?view=aspnetcore-2.1) foi introduzido para expandir os recursos da ferramenta de pré-compilação. O SDK do Razor adicionou suporte para compilação de compilação e tempo de publicação de arquivos Razor. O SDK verifica a exatidão dos arquivos *. cshtml* no momento da compilação, ao mesmo tempo em que melhora o tempo de inicialização do aplicativo. O SDK do Razor está ativado por padrão e nenhum gesto é necessário para começar a usá-lo.

No ASP.NET Core 3,0, a ferramenta de pré-compilação MVC ASP.NET Core 1,1 de era removida. Versões anteriores do pacote continuarão recebendo correções importantes de bugs e de segurança na versão do patch.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacote foi usado para pré-compilar exibições do Razor do MVC.

#### <a name="new-behavior"></a>Novo comportamento

O SDK do Razor oferece suporte nativo a essa funcionalidade. O `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacote não é mais atualizado.

#### <a name="reason-for-change"></a>Motivo da alteração

O SDK do Razor fornece mais funcionalidade e verifica a exatidão dos arquivos *. cshtml* no momento da compilação. O SDK também melhora o tempo de inicialização do aplicativo.

#### <a name="recommended-action"></a>Ação recomendada

Para usuários do ASP.NET Core 2,1 ou posterior, atualize para usar o suporte nativo para pré-compilação no SDK do [Razor](/aspnet/core/razor-pages/sdk?view=aspnetcore-3.0). Se os bugs ou os recursos ausentes impedirem a migração para o SDK do Razor, abra um problema em [dotnet/aspnetcore](https://github.com/dotnet/aspnetcore/issues).

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
