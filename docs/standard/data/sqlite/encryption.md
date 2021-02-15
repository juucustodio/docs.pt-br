---
title: Criptografia
ms.date: 09/08/2020
description: Saiba como criptografar seu arquivo de banco de dados.
ms.openlocfilehash: 1b33e1510a269aba87caba2cd39faab33791aa55
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203404"
---
# <a name="encryption"></a>Criptografia

O SQLite não dá suporte a criptografia de arquivos de banco de dados por padrão. Em vez disso, você precisa usar uma versão modificada do SQLite, como [Ver](https://www.hwaci.com/sw/sqlite/see.html), [sqlcipher](https://www.zetetic.net/sqlcipher/), [SQLiteCrypt](http://www.sqlite-crypt.com/)ou [wxSQLite3](https://utelle.github.io/wxsqlite3). Este artigo demonstra o uso de uma compilação sem suporte de código-fonte aberto de sqlcipher, mas as informações também se aplicam a outras soluções, pois geralmente seguem o mesmo padrão.

## <a name="installation"></a>Instalação

### <a name="net-core-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

```dotnetcli
dotnet remove package Microsoft.Data.Sqlite
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.bundle_e_sqlcipher
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Remove-Package Microsoft.Data.Sqlite
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.bundle_e_sqlcipher
```

---

Para obter mais informações sobre como usar uma biblioteca nativa diferente para criptografia, consulte [versões personalizadas do SQLite](custom-versions.md).

## <a name="specify-the-key"></a>Especifique a chave

Para habilitar a criptografia em um novo banco de dados, especifique a chave usando a `Password` palavra-chave da cadeia de conexão. Use <xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> para adicionar ou atualizar o valor da entrada do usuário e evitar ataques de injeção de cadeia de conexão.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_ConnectionStringBuilder)]

> [!TIP]
> O método para criptografar e descriptografar bancos de dados existentes varia de acordo com a solução que você está usando. Por exemplo, você precisa usar a `sqlcipher_export()` função em sqlcipher. Verifique a documentação da solução para obter detalhes.

## <a name="rekeying-the-database"></a>Rechaveamento do banco de dados

Se você quiser alterar a chave de um banco de dados criptografado, emita uma `PRAGMA rekey` instrução.

Infelizmente, o SQLite não dá suporte a parâmetros em `PRAGMA` instruções. Em vez disso, use a `quote()` função para impedir a injeção de SQL.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_Rekey)]
