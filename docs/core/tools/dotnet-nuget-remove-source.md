---
title: comando de remoção de origem do NuGet do dotnet
description: O comando dotnet NuGet remove Source remove uma fonte existente dos arquivos de configuração do NuGet.
ms.date: 03/20/2020
ms.openlocfilehash: b5575c31c0008d6e3e5a2e52906a076614217dd0
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537880"
---
# <a name="dotnet-nuget-remove-source"></a>dotnet nuget remove source

**Este artigo aplica-se a:** ✔️ SDK 3.1.200 do .NET Core e versões posteriores

## <a name="name"></a>Name

`dotnet nuget remove source` -Remover uma origem do NuGet.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget remove source <NAME> [--configfile <FILE>]

dotnet nuget remove source -h|--help
```

## <a name="description"></a>Description

O `dotnet nuget remove source` comando Remove uma fonte existente dos arquivos de configuração do NuGet.

## <a name="arguments"></a>Argumentos

- **`NAME`**

  Nome da origem.

## <a name="options"></a>Opções

- **`--configfile`**

  O arquivo de configuração do NuGet. Se especificado, somente as configurações desse arquivo serão usadas. Se não for especificado, a hierarquia de arquivos de configuração do diretório atual será usada. Para obter mais informações, consulte [configurações comuns do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

## <a name="examples"></a>Exemplos

- Remova uma fonte com o nome de `mySource` :

  ```dotnetcli
  dotnet nuget remove source mySource
  ```

## <a name="see-also"></a>Confira também

- [Seções de origem do pacote em arquivos NuGet.config](/nuget/reference/nuget-config-file#package-source-sections)

- [comando Sources (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
