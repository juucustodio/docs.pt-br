---
title: 'Alteração significativa: extensões: alterações de referência de pacote que afetam alguns pacotes NuGet'
description: 'Saiba mais sobre a alteração significativa em extensões com título ASP.NET Core 5,0: alterações de referência de pacote que afetam alguns pacotes NuGet'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 4a525d9f7aad4409fd507fcf80c00968ff4b63d4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760375"
---
# <a name="extensions-package-reference-changes-affecting-some-nuget-packages"></a>Extensões: alterações de referência de pacote que afetam alguns pacotes NuGet

Com a migração de alguns `Microsoft.Extensions.*` pacotes NuGet do repositório [dotnet/extensões](https://github.com/dotnet/extensions) para [dotnet/tempo de execução](https://github.com/dotnet/runtime), conforme descrito em [ASPNET/comunicados # 411](https://github.com/aspnet/Announcements/issues/411), as alterações de empacotamento estão sendo aplicadas a alguns dos pacotes migrados. Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 21033](https://github.com/dotnet/aspnetcore/issues/21033).

## <a name="version-introduced"></a>Versão introduzida

5,0 versão prévia 4

## <a name="old-behavior"></a>Comportamento antigo

Alguns `Microsoft.Extensions.*` pacotes incluíram referências de pacote para APIs nas quais seu aplicativo dependa.

## <a name="new-behavior"></a>Novo comportamento

Seu aplicativo pode ter que adicionar `Microsoft.Extensions.*` dependências de pacote.

## <a name="reason-for-change"></a>Motivo da alteração

As políticas de empacotamento foram atualizadas para se alinharem melhor ao repositório *dotnet/tempo de execução* . Na nova política, as referências de pacote não utilizadas são removidas dos arquivos *. nupkg* durante o empacotamento.

## <a name="recommended-action"></a>Ação recomendada

Os consumidores dos pacotes afetados devem adicionar uma dependência direta da dependência do pacote removido em seu projeto se as APIs da dependência de pacote removido forem usadas. A tabela a seguir lista os pacotes afetados e as alterações correspondentes.

|Nome do pacote|Descrição das alterações|
|------------|------------------|
|[Microsoft.Extensions.Configuração. Associador](https://nuget.org/packages/Microsoft.Extensions.Configuration.Binder)|Referência removida para `Microsoft.Extensions.Configuration`|
|[Microsoft.Extensions.Configuration.Jsem](https://nuget.org/packages/Microsoft.Extensions.Configuration.Json)    |Referência removida para `System.Threading.Tasks.Extensions`|
|[Microsoft. Extensions. Hosting. abstrações](https://nuget.org/packages/Microsoft.Extensions.Hosting.Abstractions)|Referência removida para `Microsoft.Extensions.Logging.Abstractions`|
|[Microsoft.Extensions.Logging](https://nuget.org/packages/Microsoft.Extensions.Logging)                          |Referência removida para `Microsoft.Extensions.Configuration.Binder`|
|[Microsoft. Extensions. Logging. console](https://nuget.org/packages/Microsoft.Extensions.Logging.Console)          |Referência removida para `Microsoft.Extensions.Configuration.Abstractions`|
|[Microsoft. Extensions. Logging. EventLog](https://nuget.org/packages/Microsoft.Extensions.Logging.EventLog)        |Referência removida para `System.Diagnostics.EventLog` para o .NET Framework moniker da estrutura de destino do 4.6.1|
|[Microsoft. Extensions. Logging. EventSource](https://nuget.org/packages/Microsoft.Extensions.Logging.EventSource)  |Referência removida para `System.Threading.Tasks.Extensions`|
|[Microsoft. Extensions. opções](https://nuget.org/packages/Microsoft.Extensions.Options)                          |Referência removida para `System.ComponentModel.Annotations`|

Por exemplo, a referência de pacote a `Microsoft.Extensions.Configuration` foi removida do `Microsoft.Extensions.Configuration.Binder` . Nenhuma API da dependência foi usada no pacote. Os usuários de `Microsoft.Extensions.Configuration.Binder` quem dependem de APIs `Microsoft.Extensions.Configuration` devem adicionar uma referência direta a ele em seu projeto.

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
