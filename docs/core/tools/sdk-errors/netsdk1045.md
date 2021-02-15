---
title: "NETSDK1045: o SDK do .NET atual não dá suporte à ' versão mais recente ' como um destino."
description: Saiba mais sobre o erro NETSDK1045 do SDK do .NET, que ocorre quando as ferramentas de compilação não podem localizar a versão solicitada do SDK do .NET.
ms.topic: error-reference
ms.date: 02/12/2021
f1_keywords:
- NETSDK1045
ms.openlocfilehash: 900402ae01f945b1096170ea4fc79d00ea789b62
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488275"
---
# <a name="netsdk1045-the-current-net-sdk-does-not-support-newer-version-as-a-target"></a>NETSDK1045: o SDK do .NET atual não dá suporte à ' versão mais recente ' como um destino.

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

Esse erro ocorre quando as ferramentas de compilação não conseguem localizar a versão do SDK do .NET necessária para criar um projeto. Isso normalmente ocorre devido a um problema de instalação SDK do .NET Core ou configuração. A mensagem de erro completa é semelhante ao exemplo a seguir:

> NETSDK1045: o SDK do .NET atual não dá suporte à ' versão mais recente ' como um destino. Use ' versão mais antiga ' ou uma versão do SDK do .NET que dê suporte à ' versão mais recente '.

As seções a seguir descrevem alguns dos motivos possíveis para esse erro. Verifique cada um deles e veja qual deles se aplica a você. Tenha em mente que, ao fazer alterações no ambiente ou nos arquivos de configuração, talvez seja necessário reiniciar o Windows de comando, reiniciar o Visual Studio ou reinicializar o computador para que as alterações entrem em vigor.

## <a name="net-sdk-version"></a>Versão do SDK do .NET

Abra o arquivo de projeto (. csproj,. vbproj ou. fsproj) e verifique a estrutura de destino. Esta é a versão do Framework que seu aplicativo está tentando usar.

```xml
<TargetFramework>netcoreapp3.0</TargetFramework>
```

Verifique se a versão do .NET listada está instalada no computador. Você pode listar as versões instaladas usando o comando a seguir (abrir um Prompt de Comando do Desenvolvedor e executar este comando):

```dotnetcli
dotnet --list-sdks
```

### <a name="x86-or-x64-architecture"></a>arquitetura x86 ou x64

Cada versão do SDK do .NET está disponível na arquitetura x86 e x64. O projeto pode estar tentando encontrar o SDK do .NET para a arquitetura incorreta ou o SDK do .NET para a arquitetura de que seu projeto precisa pode não estar instalado. Verifique as pastas de instalação para a arquitetura de que você precisa. Por exemplo, no Windows, a versão x86 do SDK do .NET é instalada em *c:\Arquivos de programas (x86) \DotNet* e a versão x64 é instalada em *c:\Program Files\dotnet*. Veja [como verificar se o .net já está instalado](../../install/how-to-detect-installed-versions.md) e escolha seu sistema operacional para descobrir como detectar o que está instalado em seu computador.

Se a versão que você precisa não estiver instalada, baixe-a [aqui](https://dotnet.microsoft.com/download/dotnet-core).

## <a name="preview-not-enabled"></a>Visualização não habilitada

Se você tiver uma visualização instalada da versão solicitada do SDK do .NET, também precisará definir a opção para habilitar as visualizações no Visual Studio. Vá para **ferramentas**  >  **Opções**  >    >  **recursos de visualização** de ambiente e verifique se **a opção usar visualizações do SDK do .NET Core** está marcada.

## <a name="visual-studio-version"></a>Versão do Visual Studio

Por exemplo, o .NET Core 3,0 e posterior exigem o Visual Studio 2019. Atualize para o [Visual Studio 2019 versão 16,3](https://visualstudio.microsoft.com/downloads) ou posterior para compilar seu projeto.

## <a name="path-environment-variable"></a>Variável de ambiente PATH

As ferramentas de compilação usam a variável de ambiente PATH para encontrar a versão correta das ferramentas de Build do .NET. Se a variável de ambiente PATH contiver caminhos diretos para ferramentas de Build mais antigas, essa mensagem de erro poderá ser exibida. Verifique se o único caminho para as ferramentas .NET na variável de ambiente PATH é para a pasta *dotnet* de nível superior, por exemplo, *C:\Program Files\dotnet*. Um exemplo de um caminho incorreto seria algo como *C:\Program Files\dotnet\2.1.0\sdks*.

## <a name="msbuildsdkpath-environment-variable"></a>Variável de ambiente MSBuildSDKPath

Verifique a variável de ambiente MSBuildSDKPath. Essa variável de ambiente opcional é reconhecida pelo MSBuild e, se definida, substitui o valor padrão. Ele pode ser definido como uma versão específica anterior do SDK do .NET. Se ele estiver definido, tente excluí-lo e recompilar seu projeto.

## <a name="globaljson-file"></a>Arquivo global.json

Verifique se há um *global.jsno* arquivo na pasta raiz do seu projeto e na cadeia de diretórios até a raiz do volume, pois ele pode estar em qualquer lugar na estrutura de pastas. Se ele contiver uma versão do SDK, exclua o `sdk` nó e todos os seus filhos ou atualize-o para a versão do .NET Core mais recente desejada.

```json
{
  "sdk": {
    "version": "2.1.0"
  }
}
```

O *global.jsno* arquivo não é necessário, portanto, se ele não contiver nada além do `sdk` nó, você poderá excluir o arquivo inteiro.

## <a name="directorybuildprops-file"></a>Arquivo Directory. Build. props

O arquivo *Directory. Build. props* é um arquivo MSBuild opcional que pode definir propriedades globais. Verifique se esses arquivos estão na pasta da solução e na cadeia de diretórios na raiz do volume, pois eles podem estar em qualquer lugar na estrutura de pastas. Procure `TargetFramework` elementos ou configurações de `MSBuildSDKPath` que podem substituir as configurações desejadas.

## <a name="see-also"></a>Consulte também

- [O SDK do .NET atual não dá suporte ao direcionamento do .NET Core 3,0 – correção](https://www.ryadel.com/current-net-sdk-not-support-net-core-3-0-fix/)
