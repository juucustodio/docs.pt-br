---
title: comando de origem de atualização do NuGet do dotnet
description: O comando dotnet NuGet Update Source atualiza uma fonte existente nos arquivos de configuração do NuGet.
ms.date: 03/20/2020
ms.openlocfilehash: a8658c78c095ad4b9272d97200e1d6466cbe658b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537848"
---
# <a name="dotnet-nuget-update-source"></a>dotnet nuget update source

**Este artigo aplica-se a:** ✔️ SDK 3.1.200 do .NET Core e versões posteriores

## <a name="name"></a>Name

`dotnet nuget update source` -Atualizar uma origem do NuGet.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget update source <NAME> [--source <SOURCE>] [--username <USER>]
    [--password <PASSWORD>] [--store-password-in-clear-text]
    [--valid-authentication-types <TYPES>] [--configfile <FILE>]

dotnet nuget update source -h|--help
```

## <a name="description"></a>Description

O `dotnet nuget update source` comando atualiza uma origem existente nos arquivos de configuração do NuGet.

## <a name="arguments"></a>Argumentos

- **`NAME`**

  Nome da origem.

## <a name="options"></a>Opções

- **`--configfile <FILE>`**

  O arquivo de configuração do NuGet. Se especificado, somente as configurações desse arquivo serão usadas. Se não for especificado, a hierarquia de arquivos de configuração do diretório atual será usada. Para obter mais informações, consulte [configurações comuns do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

- **`-p|--password <PASSWORD>`**

  Senha a ser usada ao conectar-se a uma fonte autenticada.

- **`-s|--source <SOURCE>`**

  Caminho para a origem do pacote.

- **`--store-password-in-clear-text`**

  Habilita o armazenamento de credenciais de origem do pacote portátil desabilitando a criptografia de senha.

- **`-u|--username <USER>`**

  Nome de usuário a ser usado ao conectar a uma fonte autenticada.

- **`--valid-authentication-types <TYPES>`**

  Lista separada por vírgulas de tipos de autenticação válidos para esta fonte. Defina isso como `basic` se o servidor anunciar NTLM ou negociar e suas credenciais devem ser enviadas usando o mecanismo básico, por exemplo, ao usar uma Pat com Azure DevOps Server locais. Outros valores válidos incluem `negotiate` , `kerberos` , `ntlm` e `digest` , mas esses valores são improvável de ser úteis.

## <a name="examples"></a>Exemplos

- Atualize uma fonte com o nome de `mySource` :

  ```dotnetcli
  dotnet nuget update source mySource --source c:\packages
  ```

## <a name="see-also"></a>Confira também

- [Seções de origem do pacote em arquivos NuGet.config](/nuget/reference/nuget-config-file#package-source-sections)

- [comando Sources (nuget.exe)](/nuget/reference/cli-reference/cli-ref-sources)
