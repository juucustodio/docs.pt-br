---
ms.openlocfilehash: 75945e7ff26c1c6db891d12cef4c16ed210da6af
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032299"
---
### <a name="mvc-web-api-compatibility-shim-removed"></a>MVC: Shim de compatibilidade da API Web removido

A partir do ASP.NET Core 3,0, o `Microsoft.AspNetCore.Mvc.WebApiCompatShim` pacote não está mais disponível.

#### <a name="change-description"></a>Descrição das alterações

O `Microsoft.AspNetCore.Mvc.WebApiCompatShim` pacote (WebApiCompatShim) fornece compatibilidade parcial em ASP.NET Core com a API web ASP.NET 4. x para simplificar a migração de implementações de API Web existentes para ASP.NET Core. No entanto, os aplicativos que usam o WebApiCompatShim não se beneficiam dos recursos relacionados à API fornecidos em versões recentes de ASP.NET Core. Esses recursos incluem geração aprimorada de especificação de API aberta, tratamento de erro padronizado e geração de código de cliente. Para focar melhor os esforços de API em 3,0, o WebApiCompatShim foi removido. Os aplicativos existentes que usam o WebApiCompatShim devem migrar para o modelo mais recente `[ApiController]` .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

O Shim da compatibilidade da API Web era uma ferramenta de migração. Ele restringe o acesso do usuário à nova funcionalidade adicionada no ASP.NET Core.

#### <a name="recommended-action"></a>Ação recomendada

Remova o uso desse Shim e migre diretamente para a funcionalidade semelhante no ASP.NET Core em si.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Mvc.WebApiCompatShim?displayProperty=fullName>

<!--

#### Affected APIs

N:Microsoft.AspNetCore.Mvc.WebApiCompatShim

-->
