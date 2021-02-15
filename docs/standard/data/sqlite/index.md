---
title: Visão geral
ms.date: 12/13/2019
description: Uma visão geral do Microsoft. Data. sqlite
ms.openlocfilehash: 7c952848f7e7ea04f11fe9340f77a1f376a1be07
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90552434"
---
# <a name="microsoftdatasqlite-overview"></a>Visão geral do Microsoft. Data. sqlite

Microsoft. Data. SQLite é um provedor [ADO.net](../../../framework/data/adonet/index.md) leve para SQLite. O provedor de [Entity Framework Core](/ef/core/) para SQLite é criado sobre esta biblioteca. No entanto, ele também pode ser usado de forma independente ou com outras bibliotecas de acesso a dados.

## <a name="installation"></a>Instalação

A versão estável mais recente está disponível no [NuGet](https://www.nuget.org/packages/Microsoft.Data.Sqlite).

### <a name="net-core-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite
```

---

## <a name="usage"></a>Uso

Essa biblioteca implementa as abstrações ADO.NET comuns para conexões, comandos, leitores de dados e assim por diante.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/HelloWorldSample/Program.cs?name=snippet_HelloWorld)]

## <a name="see-also"></a>Confira também

* [Cadeias de conexão](connection-strings.md)
* [Referência da API](../../../../api/index.md?view=msdata-sqlite-3.0)
* [Sintaxe SQL](https://www.sqlite.org/lang.html)
