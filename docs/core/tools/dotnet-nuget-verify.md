---
title: comando dotnet NuGet Verify
description: O comando dotnet NuGet Verify verifica um pacote assinado.
author: kartheekp-ms
ms.date: 10/08/2020
ms.openlocfilehash: 6cb368e2b6c203f3774b4450c0831c5d6b2dc0e8
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957133"
---
# <a name="dotnet-nuget-verify"></a>verificação do NuGet do dotnet

**Este artigo aplica-se a: ✔️ o** SDK do .NET 5.0.100-RC. 2. x e versões posteriores

## <a name="name"></a>Nome

`dotnet nuget verify` -Verifica um pacote NuGet assinado.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet nuget verify [<package-path(s)>]
    [--all]
    [--certificate-fingerprint <FINGERPRINT>]
    [-v|--verbosity <LEVEL>]

dotnet nuget verify -h|--help
```

## <a name="description"></a>Descrição

O `dotnet nuget verify` comando verifica um pacote NuGet assinado.

## <a name="arguments"></a>Argumentos

- **`package-path(s)`**

  Especifica o caminho de arquivo para os pacotes a serem verificados. Vários argumentos de posição podem ser passados para verificar vários pacotes.

## <a name="options"></a>Opções

- **`--all`**

  Especifica que todas as verificações possíveis devem ser executadas nos pacotes. Por padrão, somente `signatures` são verificados.

> [!NOTE]
> Esse comando atualmente dá suporte apenas à `signature` verificação.

- **`--certificate-fingerprint <FINGERPRINT>`**

  Verifique se o certificado de signatário corresponde a uma das `SHA256` impressões digitais especificadas. Essa opção pode ser fornecida várias vezes para fornecer várias impressões digitais.

* **`-v|--verbosity <LEVEL>`**

  Define o nível de detalhamento do MSBuild. Os valores permitidos são `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`. O padrão é `normal`.

* **`-h|--help`**

  Imprime uma ajuda breve para o comando.

## <a name="examples"></a>Exemplos

- Verifique *foo. nupkg*:

  ```dotnetcli
  dotnet nuget verify foo.nupkg
  ```

- Verifique vários pacotes NuGet- *foo. nupkg* e *todos os arquivos. nupkg no diretório especificado*:

  ```dotnetcli
  dotnet nuget verify foo.nupkg c:\mydir\*.nupkg
  ```

- Verifique se a assinatura *foo. nupkg* corresponde à impressão digital do certificado especificado:

  ```dotnetcli
  dotnet nuget verify foo.nupkg --certificate-fingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039
  ```

- Verifique se a assinatura *foo. nupkg* corresponde a uma das impressões digitais do certificado especificado:

  ```dotnetcli
  dotnet nuget verify foo.nupkg --certificate-fingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 --certificate-fingerprint EC10992GG5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E027
  ```
