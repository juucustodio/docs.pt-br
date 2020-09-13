---
title: Versões personalizadas do SQLite
ms.date: 09/04/2020
description: Saiba como usar uma versão personalizada da biblioteca SQLite nativa.
ms.openlocfilehash: fbf4b4cd33e6e890ce0c0cfe0b7688487b94b4a3
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516132"
---
# <a name="custom-sqlite-versions"></a>Versões personalizadas do SQLite

`Microsoft.Data.Sqlite` é criado com base em `SQLitePCLRaw` . Você pode usar versões personalizadas da biblioteca SQLite nativa usando um pacote ou configurando um `SQLitePCLRaw` provedor.

## <a name="bundles"></a>Pacotes

`SQLitePCLRaw` fornece pacotes de pacote baseados em conveniência, que facilitam a tarefa de trazer as dependências certas entre diferentes plataformas. O `Microsoft.Data.Sqlite` pacote principal traz `SQLitePCLRaw.bundle_e_sqlite3` por padrão. Para usar um pacote diferente, instale o `Microsoft.Data.Sqlite.Core` pacote, juntamente com o pacote de pacotes que você deseja usar. Os grupos são inicializados automaticamente pelo `Microsoft.Data.Sqlite` .

| Pacote | Descrição |
|--|--|
| [SQLitePCLRaw. bundle_e_sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.bundle_e_sqlite3) | Fornece uma versão consistente do SQLite em todas as plataformas. Inclui as extensões de árvore FTS4, FTS5, JSON1 e R *. Este é o padrão. |
| [SQLitePCLRaw. bundle_e_sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.bundle_e_sqlcipher) | Fornece uma compilação não oficial de código aberto do `SQLCipher` . |
| [SQLitePCLRaw. bundle_green](https://www.nuget.org/packages/SQLitePCLRaw.bundle_green) | O mesmo que `bundle_e_sqlite3` , exceto no Ios, em que ele usa a biblioteca SQLite do sistema. |
| [SQLitePCLRaw. bundle_sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.bundle_sqlite3) | Usa a biblioteca SQLite do sistema. |
| [SQLitePCLRaw. bundle_winsqlite3](https://www.nuget.org/packages/SQLitePCLRaw.bundle_winsqlite3) | Usa `winsqlite3.dll` o, a biblioteca SQLite do sistema no Windows 10. |
| [SQLitePCLRaw. bundle_zetetic](https://www.nuget.org/packages/SQLitePCLRaw.bundle_zetetic) | Usa as `SQLCipher` compilações oficiais do Zetetic (não incluído). |

Por exemplo, para usar a compilação de código aberto não oficial, `SQLCipher` use os comandos a seguir.

### <a name="net-core-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.bundle_e_sqlcipher
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.bundle_e_sqlcipher
```

---

## <a name="sqlitepclraw-available-providers"></a>Provedores SQLitePCLRaw disponíveis

Quando não depender de um pacote, você pode usar os provedores disponíveis do SQLite com o assembly principal.

| Provedor | Descrição |
|--|--|
| [SQLitePCLRaw. Provider. Dynamic](https://www.nuget.org/packages/SQLitePCLRaw.provider.dynamic) | O `dynamic` provedor carrega a biblioteca nativa em vez de usar <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=nameWithType> atributos. Para obter mais informações sobre como usar esse provedor, consulte [usar o provedor dinâmico](#use-the-dynamic-provider). |
| [SQLitePCLRaw. Provider. e_sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.e_sqlite3) | O `e_sqlite3` é o provedor padrão. |
| [SQLitePCLRaw. Provider. e_sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.provider.e_sqlcipher) | O `e_sqlcipher` provedor é o não oficial e não tem suporte `SQLCipher` . |
| [SQLitePCLRaw. Provider. sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.sqlite3) | O `sqlite3` provedor é fornecido pelo sistema `SQLite` para IOS, MacOS e Linux. |
| [SQLitePCLRaw. Provider. sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.provider.sqlcipher) | O `sqlcipher` provedor é para `SQLCipher` compilações oficiais do `Zetetic` . |
| [SQLitePCLRaw. Provider. winsqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.winsqlite3) | O `winsqlite3` provedor é para ambientes Windows 10. |

Para usar o `sqlite3` provedor, use os seguintes comandos:

### <a name="net-core-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.core
dotnet add package SQLitePCLRaw.provider.sqlite3
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.core
Install-Package SQLitePCLRaw.provider.sqlite3
```

---

Com os pacotes instalados, você define o provedor como a `sqlite3` instância.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SqliteProviderSample/Program.cs)]

## <a name="use-the-dynamic-provider"></a>Usar o provedor dinâmico

Você pode usar sua própria compilação do SQLite aproveitando o `SQLitePCLRaw.provider.dynamic_cdecl` pacote. Nesse caso, você é responsável por implantar a biblioteca nativa com seu aplicativo. Observe que os detalhes da implantação de bibliotecas nativas com seu aplicativo variam consideravelmente dependendo da plataforma .NET e do tempo de execução que você está usando.

Primeiro, você precisará implementar `IGetFunctionPointer` . A implementação no .NET Core é a seguinte:

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_NativeLibraryAdapter)]

Em seguida, configure o `SQLitePCLRaw` provedor. Verifique se isso é feito antes `Microsoft.Data.Sqlite` de ser usado em seu aplicativo. Além disso, evite usar um `SQLitePCLRaw` pacote de pacotes que possa substituir seu provedor.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_SetProvider)]
