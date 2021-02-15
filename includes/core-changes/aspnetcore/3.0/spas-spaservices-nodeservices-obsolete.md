---
ms.openlocfilehash: ac5a3c4f3aefbb59418ad92b2d795f36916f877f
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032313"
---
### <a name="spas-spaservices-and-nodeservices-marked-obsolete"></a>SPAs: SpaServices e Nodeservices marcados como obsoletos

Todos os conteúdos dos pacotes NuGet a seguir foram desnecessários desde ASP.NET Core 2,1. Consequentemente, os seguintes pacotes estão sendo marcados como obsoletos:

- [Microsoft. AspNetCore. SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/)
- [Microsoft. AspNetCore. Nodeservices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/)

Pelo mesmo motivo, os seguintes módulos NPM estão sendo marcados como preteridos:

- [ASPNET-angular](https://www.npmjs.com/package/aspnet-angular)
- [ASPNET-pré-processamento](https://www.npmjs.com/package/aspnet-prerendering)
- [ASPNET-webpack](https://www.npmjs.com/package/aspnet-webpack)
- [ASPNET-webpack – reagir](https://www.npmjs.com/package/aspnet-webpack-react)
- [tarefa de domínio](https://www.npmjs.com/package/domain-task)

Os pacotes anteriores e os módulos NPM serão removidos posteriormente no .NET 5.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Os pacotes preteridos e os módulos NPM foram destinados a integrar ASP.NET Core com várias estruturas de SPA (Single-Page app). Tais estruturas incluem angular, reagir e reagir com Redux.

#### <a name="new-behavior"></a>Novo comportamento

Existe um novo mecanismo de integração no pacote NuGet [Microsoft. AspNetCore. SpaServices. Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices.Extensions/) . O pacote permanece a base dos modelos de projeto angular e reajam desde o ASP.NET Core 2,1.

#### <a name="reason-for-change"></a>Motivo da alteração

O ASP.NET Core dá suporte à integração com várias estruturas de SPA (Single-Page app), incluindo angular, reagir e reagir com Redux. Inicialmente, a integração com essas estruturas foi realizada com componentes específicos do ASP.NET Core que manipulavam cenários como o pré-processamento do lado do servidor e a integração com o webpack. À medida que o tempo passou, os padrões do setor mudaram. Cada uma das estruturas de SPA lançou suas próprias interfaces de linha de comando padrão. Por exemplo, CLI angular e Create-reajam-app.

Quando ASP.NET Core 2,1 foi lançado em maio de 2018, a equipe respondeu à alteração nos padrões. Foi fornecida uma maneira mais nova e mais simples de integrar com o próprio cadeias das estruturas do SPA. O novo mecanismo de integração existe no pacote `Microsoft.AspNetCore.SpaServices.Extensions` e permanece a base dos modelos de projeto angulares e reajam desde o ASP.NET Core 2,1.

Para esclarecer que os componentes mais antigos ASP.NET Core específicos são irrelevantes e não são recomendados:

- O mecanismo de integração anterior ao 2,1 é marcado como obsoleto.
- Os pacotes NPM de suporte são marcados como preteridos.

#### <a name="recommended-action"></a>Ação recomendada

Se você estiver usando esses pacotes, atualize seus aplicativos para usar a funcionalidade:

- No `Microsoft.AspNetCore.SpaServices.Extensions` pacote.
- Fornecido pelas estruturas SPA que você está usando

Para habilitar recursos como o pré-processamento do lado do servidor e a recarga de módulo quente, consulte a documentação da estrutura SPA correspondente. A funcionalidade no `Microsoft.AspNetCore.SpaServices.Extensions` *não* está obsoleta e continuará a receber suporte.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Builder.SpaRouteExtensions?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Builder.WebpackDevMiddleware?displayProperty=nameWithType>

- <xref:Microsoft.AspNetCore.NodeServices.EmbeddedResourceReader?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.INodeServices?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.NodeServicesFactory?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.NodeServicesOptions?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.StringAsTempFile?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.HostingModels.INodeInstance?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.HostingModels.NodeInvocationException?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.HostingModels.NodeInvocationInfo?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.HostingModels.NodeServicesOptionsExtensions?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.NodeServices.HostingModels.OutOfProcessNodeInstance?displayProperty=nameWithType>

- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.ISpaPrerenderer?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.ISpaPrerendererBuilder?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.JavaScriptModuleExport?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.Prerenderer?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.PrerenderTagHelper?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Prerendering.RenderToStringResult?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SpaServices.Webpack.WebpackDevMiddlewareOptions?displayProperty=nameWithType>

- <xref:Microsoft.Extensions.DependencyInjection.NodeServicesServiceCollectionExtensions?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.DependencyInjection.PrerenderingServiceCollectionExtensions?displayProperty=nameWithType>

<!--

#### Affected APIs

- `T:Microsoft.AspNetCore.Builder.SpaRouteExtensions`
- `T:Microsoft.AspNetCore.Builder.WebpackDevMiddleware`

- `T:Microsoft.AspNetCore.NodeServices.EmbeddedResourceReader`
- `T:Microsoft.AspNetCore.NodeServices.INodeServices`
- `T:Microsoft.AspNetCore.NodeServices.NodeServicesFactory`
- `T:Microsoft.AspNetCore.NodeServices.NodeServicesOptions`
- `T:Microsoft.AspNetCore.NodeServices.StringAsTempFile`
- `T:Microsoft.AspNetCore.NodeServices.HostingModels.INodeInstance`
- `T:Microsoft.AspNetCore.NodeServices.HostingModels.NodeInvocationException`
- `T:Microsoft.AspNetCore.NodeServices.HostingModels.NodeInvocationInfo`
- `T:Microsoft.AspNetCore.NodeServices.HostingModels.NodeServicesOptionsExtensions`
- `T:Microsoft.AspNetCore.NodeServices.HostingModels.OutOfProcessNodeInstance`

- `T:Microsoft.AspNetCore.SpaServices.Prerendering.ISpaPrerenderer`
- `T:Microsoft.AspNetCore.SpaServices.Prerendering.ISpaPrerendererBuilder`
- `T:Microsoft.AspNetCore.SpaServices.Prerendering.JavaScriptModuleExport`
- `T:Microsoft.AspNetCore.SpaServices.Prerendering.Prerenderer`
- `T:Microsoft.AspNetCore.SpaServices.Prerendering.PrerenderTagHelper`
- `T:Microsoft.AspNetCore.SpaServices.Prerendering.RenderToStringResult`
- `T:Microsoft.AspNetCore.SpaServices.Webpack.WebpackDevMiddlewareOptions`

- `T:Microsoft.Extensions.DependencyInjection.NodeServicesServiceCollectionExtensions`
- `T:Microsoft.Extensions.DependencyInjection.PrerenderingServiceCollectionExtensions`

-->
