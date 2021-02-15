---
ms.openlocfilehash: 82103d82a6f68c62f3532608718bc71b0ba126bf
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032236"
---
### <a name="hosting-aspnetcoremodule-v1-removed-from-windows-hosting-bundle"></a>Hospedagem: AspNetCoreModule v1 removido do pacote de hospedagem do Windows

A partir do ASP.NET Core 3,0, o grupo de hospedagem do Windows não conterá AspNetCoreModule (ANCM) v1.

O ANCM V2 é compatível com versões anteriores com ANCM OutOfProcess e é recomendado para uso com ASP.NET Core aplicativos 3,0.

Para obter uma discussão, consulte [dotnet/aspnetcore # 7095](https://github.com/dotnet/aspnetcore/issues/7095).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O ANCM v1 está incluído no pacote de hospedagem do Windows.

#### <a name="new-behavior"></a>Novo comportamento

O ANCM v1 não está incluído no pacote de hospedagem do Windows.

#### <a name="reason-for-change"></a>Motivo da alteração

O ANCM V2 é compatível com versões anteriores com ANCM OutOfProcess e é recomendado para uso com ASP.NET Core aplicativos 3,0.

#### <a name="recommended-action"></a>Ação recomendada

Use o ANCM V2 com aplicativos ASP.NET Core 3,0.

Se o ANCM v1 for necessário, ele poderá ser instalado usando o pacote de hospedagem ASP.NET Core 2,1 ou 2,2 do Windows.

Essa alteração interromperá ASP.NET Core aplicativos 3,0 que:

- Optamos explicitamente por usar o ANCM v1 com `<AspNetCoreModuleName>AspNetCoreModule</AspNetCoreModuleName>` .
- Ter um arquivo de *web.config* personalizado com `<add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />` .

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
