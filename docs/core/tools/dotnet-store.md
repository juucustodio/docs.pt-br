---
title: Comando dotnet store
description: O comando "dotnet store" armazena os assemblies especificados no repositório de pacotes de runtime.
ms.date: 02/14/2020
ms.openlocfilehash: 8efb11c6bf648bc7787d5627e02b180abb8a0afd
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634331"
---
# <a name="dotnet-store"></a>dotnet store

**Este artigo aplica-se a:** ✔️ SDK do .NET Core 2. x e versões posteriores

## <a name="name"></a>Name

`dotnet store` – Armazena os assemblies especificados no [repositório de pacotes de runtime](../deploying/runtime-store.md).

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet store -m|--manifest <PATH_TO_MANIFEST_FILE>
    -f|--framework <FRAMEWORK_VERSION> -r|--runtime <RUNTIME_IDENTIFIER>
    [--framework-version <FRAMEWORK_VERSION>] [--output <OUTPUT_DIRECTORY>]
    [--skip-optimization] [--skip-symbols] [-v|--verbosity <LEVEL>]
    [--working-dir <WORKING_DIRECTORY>]

dotnet store -h|--help
```

## <a name="description"></a>Description

`dotnet store` armazena os assemblies especificados no [repositório de pacotes de runtime](../deploying/runtime-store.md). Por padrão, os assemblies são otimizados para a estrutura e o runtime de destino. Para obter mais informações, consulte o tópico [repositório de pacotes de runtime](../deploying/runtime-store.md).

## <a name="required-options"></a>Opções obrigatórias

- **`-f|--framework <FRAMEWORK>`**

  Especifica a [estrutura de destino](../../standard/frameworks.md). A estrutura de destino deve ser especificada no arquivo de projeto.

- **`-m|--manifest <PATH_TO_MANIFEST_FILE>`**

  O *arquivo de manifesto do repositório de pacotes* é um arquivo XML que contém a lista de pacotes a serem armazenados. O formato do arquivo de manifesto é compatível com o formato de projeto de estilo SDK. Portanto, um arquivo de projeto que referencia os pacotes desejados pode ser usado com a opção `-m|--manifest` para armazenar assemblies no repositório de pacotes de runtime. Para especificar vários arquivos de manifesto, repita a opção e o caminho para cada arquivo. Por exemplo: `--manifest packages1.csproj --manifest packages2.csproj`.

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  O [identificador de tempo de execução](../rid-catalog.md) para o destino.

## <a name="optional-options"></a>Opções opcionais

- **`--framework-version <FRAMEWORK_VERSION>`**

  Especifica a versão do SDK do .NET. Essa opção permite que você selecione uma versão da estrutura específica, além da estrutura especificada pela opção `-f|--framework`.

- **`-h|--help`**

  Mostra informações de ajuda.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  Especifica o caminho para o repositório de pacotes de runtime. Se não for especificado, o padrão será o subdiretório de *armazenamento* do diretório de instalação .net do perfil do usuário.

- **`--skip-optimization`**

  Ignora a fase de otimização.

- **`--skip-symbols`**

  Ignora a geração de símbolos. No momento, só é possível gerar símbolos no Windows e no Linux.

- **`-v|--verbosity <LEVEL>`**

  Define o nível de detalhes do comando. Os valores permitidos são `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

- **`-w|--working-dir <WORKING_DIRECTORY>`**

  O diretório de trabalho usado pelo comando. Se não for especificado, ele usará o subdiretório *obj* do diretório atual.

## <a name="examples"></a>Exemplos

- Armazene os pacotes especificados no arquivo de projeto *packages.csproj* para .NET Core 2.0.0:

  ```dotnetcli
  dotnet store --manifest packages.csproj --framework-version 2.0.0
  ```

- Armazene os pacotes especificados no *packages.csproj* sem otimização:

  ```dotnetcli
  dotnet store --manifest packages.csproj --skip-optimization
  ```

## <a name="see-also"></a>Consulte também

- [Repositório de pacotes de runtime](../deploying/runtime-store.md)
