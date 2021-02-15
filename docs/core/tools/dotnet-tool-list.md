---
title: Comando dotnet tool list
description: O comando dotnet da lista de ferramentas lista as ferramentas .NET que estão instaladas em seu computador.
ms.date: 02/14/2020
ms.openlocfilehash: d884f2c41834dd9704de3a8ca15417ba368fde4b
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634279"
---
# <a name="dotnet-tool-list"></a>dotnet tool list

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="name"></a>Name

`dotnet tool list` -Lista todas as [ferramentas .net](global-tools.md) do tipo especificado atualmente instalado em seu computador.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet tool list -g|--global

dotnet tool list --tool-path <PATH>

dotnet tool list --local

dotnet tool list

dotnet tool list -h|--help
```

## <a name="description"></a>Description

O `dotnet tool list` comando fornece uma maneira de listar todas as ferramentas globais, de caminho de ferramenta ou locais do .net instaladas em seu computador. O comando lista o nome do pacote, a versão instalada e o comando da ferramenta.  Para usar o comando, especifique um dos seguintes:

* Para listar as ferramentas globais instaladas no local padrão, use a `--global` opção
* Para listar as ferramentas globais instaladas em um local personalizado, use a `--tool-path` opção.
* Para listar as ferramentas locais, use a `--local` opção ou omita as `--global` `--tool-path` Opções, e `--local` .

**As ferramentas locais estão disponíveis a partir do SDK do .NET Core 3,0.**

## <a name="options"></a>Opções

- **`-g|--global`**

  Lista as ferramentas globais em todo o usuário. Não pode ser combinada com a opção `--tool-path`. Omitir `--global` e `--tool-path` listar as ferramentas locais.

- **`-h|--help`**

  Imprime uma ajuda breve para o comando.

- **`--local`**

  Lista as ferramentas locais para o diretório atual. Não pode ser combinado com `--global` as `--tool-path` Opções ou. Omitir `--global` e `--tool-path` listar as ferramentas locais, mesmo se `--local` não for especificado.

- **`--tool-path <PATH>`**

  Especifica um local personalizado onde encontrar ferramentas globais. PATH pode ser absoluto ou relativo. Não pode ser combinada com a opção `--global`. Omitir `--global` e `--tool-path` listar as ferramentas locais.

## <a name="examples"></a>Exemplos

- **`dotnet tool list -g`**

  Lista todas as ferramentas globais instaladas por todo o usuário em seu computador (perfil de usuário atual).

- **`dotnet tool list --tool-path c:\global-tools`**

  Lista as ferramentas globais de um diretório específico do Windows.

- **`dotnet tool list --tool-path ~/bin`**

  Lista as ferramentas globais de um diretório específico do Linux/macOS.

- **`dotnet tool list`** or **`dotnet tool list --local`**

  Lista todas as ferramentas locais disponíveis no diretório atual.

## <a name="see-also"></a>Consulte também

- [Ferramentas .NET](global-tools.md)
- [Tutorial: instalar e usar uma ferramenta global do .NET usando a CLI do .NET](global-tools-how-to-use.md)
- [Tutorial: instalar e usar uma ferramenta local do .NET usando a CLI do .NET](local-tools-how-to-use.md)
