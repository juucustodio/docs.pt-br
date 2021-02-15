---
title: comando dotnet habilitar origem do NuGet
description: O comando dotnet habilitar origem do NuGet habilita uma origem existente em seus arquivos de configuração do NuGet.
ms.date: 03/20/2020
ms.openlocfilehash: b727844dd7d7cc82476e94a3f0ec4ecc6559d5ed
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537928"
---
# <a name="dotnet-nuget-enable-source"></a>dotnet nuget enable source

**Este artigo aplica-se a:** ✔️ SDK 3.1.200 do .NET Core e versões posteriores

## <a name="name"></a>Name

`dotnet nuget enable source` -Habilitar uma origem do NuGet.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget enable source <NAME> [--configfile <FILE>]

dotnet nuget enable source -h|--help
```

## <a name="description"></a>Description

O `dotnet nuget enable source` comando habilita uma fonte existente em seus arquivos de configuração do NuGet.

## <a name="arguments"></a>Argumentos

- **`NAME`**

  Nome da origem.

## <a name="options"></a>Opções

- **`--configfile <FILE>`**

  O arquivo de configuração do NuGet. Se especificado, somente as configurações desse arquivo serão usadas. Se não for especificado, a hierarquia de arquivos de configuração do diretório atual será usada. Para obter mais informações, consulte [configurações comuns do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

## <a name="examples"></a>Exemplos

- Habilite uma fonte com o nome de `mySource` :

  ```dotnetcli
  dotnet nuget enable source mySource
  ```

## <a name="see-also"></a>Confira também

- [Seções de origem do pacote em arquivos NuGet.config](/nuget/reference/nuget-config-file#package-source-sections)

- [comando Sources (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
