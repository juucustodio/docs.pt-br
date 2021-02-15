---
title: comando de origem de lista de NuGet do dotnet
description: O comando dotnet do código-fonte do NuGet lista todas as fontes existentes dos arquivos de configuração do NuGet.
ms.date: 03/20/2020
ms.openlocfilehash: 071061e32aa1bf888e197ec6bf97f4e4f6859f0b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537881"
---
# <a name="dotnet-nuget-list-source"></a>dotnet nuget list source

**Este artigo aplica-se a:** ✔️ SDK 3.1.200 do .NET Core e versões posteriores

## <a name="name"></a>Name

`dotnet nuget list source` -Lista todas as fontes do NuGet configuradas.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget list source [--format [Detailed|Short]] [--configfile <FILE>]

dotnet nuget list source -h|--help
```

## <a name="description"></a>Description

O `dotnet nuget list source` comando lista todas as fontes existentes dos arquivos de configuração do NuGet.

## <a name="options"></a>Opções

- **`--configfile <FILE>`**

  O arquivo de configuração do NuGet. Se especificado, somente as configurações desse arquivo serão usadas. Se não for especificado, a hierarquia de arquivos de configuração do diretório atual será usada. Para obter mais informações, consulte [configurações comuns do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

- **`--format [Detailed|Short]`**

  O formato da saída do comando de lista: `Detailed` (o padrão) e `Short` .

## <a name="examples"></a>Exemplos

- Listar fontes configuradas do diretório atual:

  ```dotnetcli
  dotnet nuget list source
  ```

## <a name="see-also"></a>Confira também

- [Seções de origem do pacote em arquivos NuGet.config](/nuget/reference/nuget-config-file#package-source-sections)

- [comando Sources (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
