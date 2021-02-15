---
title: Comando dotnet tool uninstall
description: O comando dotnet ferramenta de desinstalação desinstala a ferramenta .NET especificada do seu computador.
ms.date: 02/14/2020
ms.openlocfilehash: 34dffde8f9c930327c6b42d1d89bb4f511959fb2
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634084"
---
# <a name="dotnet-tool-uninstall"></a>dotnet tool uninstall

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="name"></a>Name

`dotnet tool uninstall` -Desinstala a [ferramenta .net](global-tools.md) especificada do seu computador.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet tool uninstall <PACKAGE_NAME> -g|--global

dotnet tool uninstall <PACKAGE_NAME> --tool-path <PATH>

dotnet tool uninstall <PACKAGE_NAME>

dotnet tool uninstall -h|--help
```

## <a name="description"></a>Description

O `dotnet tool uninstall` comando fornece uma maneira de desinstalar as ferramentas .net do seu computador. Para usar o comando, especifique uma das seguintes opções:

* Para desinstalar uma ferramenta global que foi instalada no local padrão, use a `--global` opção.
* Para desinstalar uma ferramenta global que foi instalada em um local personalizado, use a `--tool-path` opção.
* Para desinstalar uma ferramenta local, omita as `--global` `--tool-path` Opções e.

**As ferramentas locais estão disponíveis a partir do SDK do .NET Core 3,0.**

## <a name="arguments"></a>Argumentos

- **`PACKAGE_NAME`**

  Nome/ID do pacote NuGet que contém a ferramenta .NET a ser desinstalada. Encontre o nome do pacote usando o comando [dotnet tool list](dotnet-tool-list.md).

## <a name="options"></a>Opções

- **`-g|--global`**

  Especifica que a ferramenta a ser removida pertence a uma instalação de todos os usuários. Não pode ser combinada com a opção `--tool-path`. Omitir ambos `--global` e `--tool-path` especifica que a ferramenta a ser removida é uma ferramenta local.

- **`-h|--help`**

  Imprime uma ajuda breve para o comando.

- **`--tool-path <PATH>`**

  Especifica o local onde a ferramenta será desinstalada. PATH pode ser absoluto ou relativo. Não pode ser combinada com a opção `--global`. Omitir ambos `--global` e `--tool-path` especifica que a ferramenta a ser removida é uma ferramenta local.

## <a name="examples"></a>Exemplos

- **`dotnet tool uninstall -g dotnetsay`**

  Desinstala a ferramenta global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) .

- **`dotnet tool uninstall dotnetsay --tool-path c:\global-tools`**

  Desinstala a ferramenta global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) de um diretório específico do Windows.

- **`dotnet tool uninstall dotnetsay --tool-path ~/bin`**

  Desinstala a ferramenta global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) de um diretório específico do linux/MacOS.

- **`dotnet tool uninstall dotnetsay`**

  Desinstala a ferramenta local [dotnetsay](https://www.nuget.org/packages/dotnetsay/) do diretório atual.

## <a name="see-also"></a>Consulte também

- [Ferramentas .NET](global-tools.md)
- [Tutorial: instalar e usar uma ferramenta global do .NET usando a CLI do .NET](global-tools-how-to-use.md)
- [Tutorial: instalar e usar uma ferramenta local do .NET usando a CLI do .NET](local-tools-how-to-use.md)
