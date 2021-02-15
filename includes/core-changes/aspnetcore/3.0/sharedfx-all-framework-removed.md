---
ms.openlocfilehash: 959f3959c28c7d0159be7a213986345e2865b9a2
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032306"
---
### <a name="shared-framework-removed-microsoftaspnetcoreall"></a>Estrutura compartilhada: Microsoft. AspNetCore. All removido

A partir do ASP.NET Core 3,0, o `Microsoft.AspNetCore.All` metapacote e a `Microsoft.AspNetCore.All` estrutura compartilhada correspondente não são mais produzidos. Este pacote está disponível no ASP.NET Core 2,2 e continuará a receber atualizações de serviço no ASP.NET Core 2,1.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Os aplicativos podem usar o `Microsoft.AspNetCore.All` metapacote para direcionar a `Microsoft.AspNetCore.All` estrutura compartilhada no .NET Core.

#### <a name="new-behavior"></a>Novo comportamento

O .NET Core 3,0 não inclui uma `Microsoft.AspNetCore.All` estrutura compartilhada.

#### <a name="reason-for-change"></a>Motivo da alteração

O `Microsoft.AspNetCore.All` metapacote incluiu um grande número de dependências externas.

#### <a name="recommended-action"></a>Ação recomendada

Migre seu projeto para usar a `Microsoft.AspNetCore.App` estrutura. Os componentes que estavam disponíveis anteriormente no `Microsoft.AspNetCore.All` ainda estão disponíveis no NuGet. Esses componentes agora são implantados com seu aplicativo, em vez de serem incluídos na estrutura compartilhada.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
