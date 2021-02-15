---
title: Comando dotnet remove package
description: O comando dotnet remove package fornece uma opção conveniente para remover uma referência de pacote NuGet de um projeto.
ms.date: 02/14/2020
ms.openlocfilehash: fc74ac1364a0ed027b83dab270d382f238dc00e5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2020
ms.locfileid: "81463450"
---
# <a name="dotnet-remove-package"></a>dotnet remove package

**Este artigo aplica-se a:** ✔️ SDK do .NET Core 2. x e versões posteriores

## <a name="name"></a>Nome

`dotnet remove package` – remove a referência de pacote de um arquivo de projeto.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet remove [<PROJECT>] package <PACKAGE_NAME>

dotnet remove package -h|--help
```

## <a name="description"></a>Descrição

O comando `dotnet remove package` fornece uma opção conveniente para remover uma referência de pacote NuGet de um projeto.

## <a name="arguments"></a>Argumentos

`PROJECT`

Especifica o arquivo do projeto. Se não for especificado, o comando pesquisará um no diretório atual.

`PACKAGE_NAME`

A referência de pacote a ser removida.

## <a name="options"></a>Opções

- **`-h|--help`**

  Imprime uma ajuda breve para o comando.

## <a name="examples"></a>Exemplos

- Remova `Newtonsoft.Json` o pacote NuGet de um projeto no diretório atual:

  ```dotnetcli
  dotnet remove package Newtonsoft.Json
  ```
