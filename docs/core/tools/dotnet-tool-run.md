---
title: comando de execução da ferramenta dotnet
description: O comando dotnet ferramenta de execução invoca uma ferramenta local.
ms.date: 02/14/2020
ms.openlocfilehash: 116ecb61748a0ca70ed385b279b11b939748f4a8
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634149"
---
# <a name="dotnet-tool-run"></a>dotnet tool run

**Este artigo aplica-se a:** ✔️ SDK do .net Core 3,0 e versões posteriores

## <a name="name"></a>Name

`dotnet tool run` -Invoca uma ferramenta local.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet tool run <COMMAND NAME>

dotnet tool run -h|--help
```

## <a name="description"></a>Description

O `dotnet tool run` comando pesquisa os arquivos de manifesto da ferramenta que estão no escopo do diretório atual. Quando ele encontra uma referência à ferramenta especificada, ele executa a ferramenta. Para obter mais informações, consulte [invocar uma ferramenta local](global-tools.md#invoke-a-local-tool).

## <a name="arguments"></a>Argumentos

- **`COMMAND_NAME`**

  O nome do comando da ferramenta a ser executada.

## <a name="options"></a>Opções

- **`-h|--help`**

  Imprime uma ajuda breve para o comando.

## <a name="example"></a>Exemplo

- **`dotnet tool run dotnetsay`**

  Executa a `dotnetsay` ferramenta local.

## <a name="see-also"></a>Consulte também

- [Ferramentas .NET](global-tools.md)
- [Tutorial: instalar e usar uma ferramenta local do .NET usando a CLI do .NET](local-tools-how-to-use.md)
