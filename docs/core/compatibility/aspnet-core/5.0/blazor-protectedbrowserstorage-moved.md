---
title: 'Alteração significativa: mais grande: o recurso ProtectedBrowserStorage mudou para a estrutura compartilhada'
description: 'Saiba mais sobre as alterações significativas no ASP.NET Core 5,0 intitulados mais recentes: o recurso ProtectedBrowserStorage mudou para a estrutura compartilhada'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: c8058adf8b66aef8dd011ea672cd306ae4de60a7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760377"
---
# <a name="blazor-protectedbrowserstorage-feature-moved-to-shared-framework"></a>Mais incrivelmente: o recurso ProtectedBrowserStorage mudou para a estrutura compartilhada

Como parte da versão do ASP.NET Core RC2 5,0, o `ProtectedBrowserStorage` recurso foi movido para a estrutura compartilhada ASP.NET Core.

## <a name="version-introduced"></a>Versão introduzida

5,0 RC2

## <a name="old-behavior"></a>Comportamento antigo

No ASP.NET Core 5,0 Preview 8, o recurso está disponível como parte do pacote [Microsoft. AspNetCore. Components. Web. Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.Web.Extensions) , mas só pode ser usado no Webassembly de mais incrivelmente.

No ASP.NET Core 5,0 RC1, o recurso está disponível como parte do pacote [Microsoft. AspNetCore. Components. ProtectedBrowserStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.ProtectedBrowserStorage) , que faz referência à `Microsoft.AspNetCore.App` estrutura compartilhada.

## <a name="new-behavior"></a>Novo comportamento

No ASP.NET Core 5,0 RC2, uma referência de pacote NuGet não é mais necessária para referenciar e usar o recurso.

## <a name="reason-for-change"></a>Motivo da alteração

A mudança para a estrutura compartilhada é uma melhor opção para a experiência do usuário que os clientes esperam.

## <a name="recommended-action"></a>Ação recomendada

Se estiver atualizando do ASP.NET Core 5,0 RC1, conclua as seguintes etapas:

1. Remova a `Microsoft.AspNetCore.Components.ProtectedBrowserStorage` referência do pacote do projeto.
1. Substitua `using Microsoft.AspNetCore.Components.ProtectedBrowserStorage;` por `using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage;`.
1. Remova a chamada de `AddProtectedBrowserStorage` de sua `Startup` classe.

Se estiver atualizando do ASP.NET Core 5,0 Preview 8, conclua as seguintes etapas:

1. Remova a `Microsoft.AspNetCore.Components.Web.Extensions` referência do pacote do projeto.
1. Substitua `using Microsoft.AspNetCore.Components.Web.Extensions;` por `using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage;`.
1. Remova a chamada de `AddProtectedBrowserStorage` de sua `Startup` classe.

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
