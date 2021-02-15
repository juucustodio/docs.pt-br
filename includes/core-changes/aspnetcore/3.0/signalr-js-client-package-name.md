---
ms.openlocfilehash: f202b39f1a45f740625827be25e72df0e403d605
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032310"
---
### <a name="signalr-javascript-client-package-name-changed"></a>Signalr: nome do pacote de cliente JavaScript alterado

No ASP.NET Core 3,0 Preview 7, o nome do pacote de cliente do sinalizador JavaScript mudou de `@aspnet/signalr` para `@microsoft/signalr` . A alteração de nome reflete o fato de que o Signalr é útil em mais do que apenas ASP.NET Core aplicativos, graças ao serviço de Signaler do Azure.

Para reagir a essa alteração, altere as referências no seu *package.jsem* arquivos, `require` instruções e `import` instruções ECMAScript. Nenhuma API será alterada como parte dessa renomeação.

Para obter uma discussão, consulte [dotnet/aspnetcore # 11637](https://github.com/dotnet/aspnetcore/issues/11637).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O pacote do cliente foi nomeado `@aspnet/signalr` .

#### <a name="new-behavior"></a>Novo comportamento

O pacote do cliente é nomeado `@microsoft/signalr` .

#### <a name="reason-for-change"></a>Motivo da alteração

A alteração de nome esclarece que o Signalr é útil além dos aplicativos ASP.NET Core, graças ao serviço do Azure Signalr.

#### <a name="recommended-action"></a>Ação recomendada

Alterne para o novo pacote `@microsoft/signalr` .

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
