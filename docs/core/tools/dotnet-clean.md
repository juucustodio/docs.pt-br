---
title: Comando dotnet clean
description: O comando dotnet clean limpa o diretório atual.
ms.date: 02/14/2020
ms.openlocfilehash: 1023f13c7662abb7dad613128631c7644ca15bb9
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189597"
---
# <a name="dotnet-clean"></a>dotnet clean

**Este artigo aplica-se a:** ✔️ SDK do .NET Core 2. x e versões posteriores

## <a name="name"></a>Nome

`dotnet clean` – limpa a saída de um projeto.

## <a name="synopsis"></a>Sinopse

```dotnetcli
dotnet clean [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [-f|--framework <FRAMEWORK>] [--interactive]
    [--nologo] [-o|--output <OUTPUT_DIRECTORY>]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [-v|--verbosity <LEVEL>]

dotnet clean -h|--help
```

## <a name="description"></a>Descrição

O comando `dotnet clean` limpará a saída da compilação anterior. Ele é implementado como um [destino de MSBuild](/visualstudio/msbuild/msbuild-targets), para que o projeto seja avaliado durante a execução do comando. Apenas as saídas criadas durante a compilação são limpas. As pastas de saídas intermediária (*obj*) e final (*bin*) serão limpas.

## <a name="arguments"></a>Argumentos

`PROJECT | SOLUTION`

O projeto do MSBuild ou a solução para limpar. Se um arquivo de solução ou projeto não for especificado, o MSBuild pesquisará no diretório de trabalho atual por um arquivo que tenha uma extensão terminada em *proj* ou *sln* e usará esse arquivo.

## <a name="options"></a>Opções

* **`-c|--configuration <CONFIGURATION>`**

  Define a configuração da compilação. O padrão para a maioria dos projetos é `Debug` , mas você pode substituir as definições de configuração de compilação em seu projeto. Essa opção só será exigida na limpeza se você especificá-la durante o momento do build.

* **`-f|--framework <FRAMEWORK>`**

  A [estrutura](../../standard/frameworks.md) que foi especificada no momento da compilação. A estrutura precisa ser definida no [arquivo de projeto](../project-sdk/overview.md). Se você especificou a estrutura no momento da compilação, especifique a estrutura ao limpar.

* **`-h|--help`**

  Imprime uma ajuda breve para o comando.

* **`--interactive`**

  Permite que o comando pare e aguarde entrada ou ação do usuário. Por exemplo, para concluir a autenticação. Disponível desde o SDK do .NET Core 3.0.

* **`--nologo`**

  Não exibe a faixa de inicialização nem a mensagem de direitos autorais. Disponível desde o SDK do .NET Core 3.0.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  O diretório que contém os artefatos de build a serem limpos. Especifique a opção `-f|--framework <FRAMEWORK>` com a opção de diretório de saída se você tiver especificado a estrutura durante a compilação do projeto.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Limpa a pasta de saída do runtime especificado. Isso é usado quando uma [implantação autocontida](../deploying/index.md#publish-self-contained) foi criada.

* **`-v|--verbosity <LEVEL>`**

  Define o nível de detalhamento do MSBuild. Os valores permitidos são `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`. O padrão é `normal`.

## <a name="examples"></a>Exemplos

* Limpe uma compilação padrão do projeto:

  ```dotnetcli
  dotnet clean
  ```

* Limpe um projeto compilado usando a configuração da Versão:

  ```dotnetcli
  dotnet clean --configuration Release
  ```
