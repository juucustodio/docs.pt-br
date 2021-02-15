---
title: Comando dotnet help
description: O comando dotnet help mostra uma documentação mais detalhada online para o comando especificado.
ms.date: 02/14/2020
ms.openlocfilehash: d583142edabb24df972bdf9a06dbfe04688f9d97
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634462"
---
# <a name="dotnet-help-reference"></a>dotnet help reference

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,0 e versões posteriores

## <a name="name"></a>Name

`dotnet help` – mostra uma documentação mais detalhada online para o comando especificado.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet help <COMMAND_NAME> [-h|--help]
```

## <a name="description"></a>Description

O comando `dotnet help` abre a página de referência para oferecer informações mais detalhadas sobre o comando especificado em docs.microsoft.com.

## <a name="arguments"></a>Argumentos

- **`COMMAND_NAME`**

  Nome do comando da CLI do .NET. Para obter uma lista dos comandos válidos da CLI, consulte [CLI commands](index.md#cli-commands) (Comandos da CLI).

## <a name="options"></a>Opções

- **`-h|--help`**

  Imprime uma ajuda breve para o comando.

## <a name="examples"></a>Exemplos

- Abre a página de documentação do comando [dotnet new](dotnet-new.md):

  ```dotnetcli
  dotnet help new
  ```
