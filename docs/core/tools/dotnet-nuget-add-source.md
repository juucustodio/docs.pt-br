---
title: dotnet NuGet Adicionar comando de origem
description: O comando dotnet NuGet Add Source adiciona uma nova origem de pacote aos arquivos de configuração do NuGet.
ms.date: 03/20/2020
ms.openlocfilehash: b847d987de2d88cb3452d32d1bc84232a1e20b6e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537967"
---
# <a name="dotnet-nuget-add-source"></a>dotnet nuget add source

**Este artigo aplica-se a:** ✔️ SDK 3.1.200 do .NET Core e versões posteriores

## <a name="name"></a>Name

`dotnet nuget add source` -Adicionar uma origem do NuGet.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget add source <PACKAGE_SOURCE_PATH> [--name <SOURCE_NAME>] [--username <USER>]
    [--password <PASSWORD>] [--store-password-in-clear-text]
    [--valid-authentication-types <TYPES>] [--configfile <FILE>]

dotnet nuget add source -h|--help
```

## <a name="description"></a>Description

O `dotnet nuget add source` comando adiciona uma nova origem de pacote aos arquivos de configuração do NuGet.

## <a name="arguments"></a>Argumentos

- **`PACKAGE_SOURCE_PATH`**

  Caminho para a origem do pacote.

## <a name="options"></a>Opções

- **`--configfile <FILE>`**

  O arquivo de configuração do NuGet. Se especificado, somente as configurações desse arquivo serão usadas. Se não for especificado, a hierarquia de arquivos de configuração do diretório atual será usada. Para obter mais informações, consulte [configurações comuns do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

- **`-n|--name <SOURCE_NAME>`**

  Nome da origem.

- **`-p|--password <PASSWORD>`**

  Senha a ser usada ao conectar-se a uma fonte autenticada.

- **`--store-password-in-clear-text`**

  Habilita o armazenamento de credenciais de origem do pacote portátil desabilitando a criptografia de senha.

- **`-u|--username <USER>`**

  Nome de usuário a ser usado ao conectar a uma fonte autenticada.

- **`--valid-authentication-types <TYPES>`**

  Lista separada por vírgulas de tipos de autenticação válidos para esta fonte. Defina isso como `basic` se o servidor anunciar NTLM ou negociar e suas credenciais devem ser enviadas usando o mecanismo básico, por exemplo, ao usar uma Pat com Azure DevOps Server locais. Outros valores válidos incluem `negotiate` , `kerberos` , `ntlm` e `digest` , mas esses valores são improvável de ser úteis.

## <a name="examples"></a>Exemplos

- Adicionar `nuget.org` como uma fonte:

  ```dotnetcli
  dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org
  ```

- Adicionar `c:\packages` como uma fonte local:

  ```dotnetcli
  dotnet nuget add source c:\packages
  ```

- Adicione uma fonte que precisa de autenticação:

  ```dotnetcli
  dotnet nuget add source https://someServer/myTeam -n myTeam -u myUsername -p myPassword --store-password-in-clear-text
  ```

- Adicione uma fonte que precisa de autenticação (em seguida, instale o provedor de credenciais):

  ```dotnetcli
  dotnet nuget add source https://azureartifacts.microsoft.com/myTeam -n myTeam
  ```

## <a name="see-also"></a>Confira também

- [Seções de origem do pacote em arquivos NuGet.config](/nuget/reference/nuget-config-file#package-source-sections)

- [comando Sources (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
