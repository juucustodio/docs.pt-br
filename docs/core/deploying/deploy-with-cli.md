---
title: Publicar aplicativos com a CLI do .NET
description: Aprenda a publicar um aplicativo .NET usando os comandos da CLI do .NET.
author: adegeo
ms.author: adegeo
ms.date: 02/05/2021
dev_langs:
- csharp
- vb
ms.openlocfilehash: af2198360670360f94f7fdf30d2890bc7dfd436d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773856"
---
# <a name="publish-net-apps-with-the-net-cli"></a>Publicar aplicativos .NET com a CLI do .NET

Este artigo demonstra como você pode publicar seu aplicativo .NET na linha de comando. O .NET fornece três maneiras de publicar seus aplicativos. A implantação dependente de estrutura produz um arquivo. dll de plataforma cruzada que usa o tempo de execução .NET instalado localmente. O executável dependente da estrutura produz um executável específico da plataforma que usa o tempo de execução .NET instalado localmente. O executável independente produz um executável específico da plataforma e inclui uma cópia local do tempo de execução do .NET.

Para obter uma visão geral desses modos de publicação, consulte [implantação de aplicativos .net](index.md).

Procurando uma ajuda rápida de como usar a CLI? A tabela a seguir mostra alguns exemplos de como publicar o aplicativo. Especifique a estrutura de destino com o parâmetro `-f <TFM>` ou editando o arquivo de projeto. Para obter mais informações, confira [Noções básicas de publicação](#publishing-basics).

| Modo de publicação                   | Versão do SDK | Comando                                                     |
|--------------------------------|-------------|-------------------------------------------------------------|
| [Implantação dependente de estrutura](#framework-dependent-deployment) | 2.1         | `dotnet publish -c Release`                                 |
|                                | 3.1         | `dotnet publish -c Release -p:UseAppHost=false`             |
|                                | 5.0         | `dotnet publish -c Release -p:UseAppHost=false`             |
| [Executável dependente de estrutura](#framework-dependent-executable) | 3.1         | `dotnet publish -c Release -r <RID> --self-contained false`<br>`dotnet publish -c Release` |
|                                | 5.0         | `dotnet publish -c Release -r <RID> --self-contained false`<br>`dotnet publish -c Release` |
| [Implantação independente](#self-contained-deployment)      | 2.1         | `dotnet publish -c Release -r <RID> --self-contained true`  |
|                                | 3.1         | `dotnet publish -c Release -r <RID> --self-contained true`  |
|                                | 5.0         | `dotnet publish -c Release -r <RID> --self-contained true`  |

\* Ao usar o **SDK versão 3,1** ou superior, o executável dependente de estrutura é o modo de publicação padrão ao executar o `dotnet publish` comando básico.

> [!NOTE]
> O `-c Release` parâmetro não é obrigatório. Ele é fornecido como um lembrete para publicar a compilação de **versão** do seu aplicativo.

## <a name="publishing-basics"></a>Noções básicas de publicação

A configuração `<TargetFramework>` do arquivo de projeto especifica a estrutura de destino padrão quando o aplicativo é publicado. Altere a estrutura de destino para qualquer [TFM](../../standard/frameworks.md) (Moniker da Estrutura de Destino) válido. Por exemplo, se o projeto usar `<TargetFramework>netcoreapp2.1</TargetFramework>` , um binário direcionado ao .NET Core 2,1 será criado. O TFM especificado nessa configuração é o destino padrão usado pelo [`dotnet publish`](../tools/dotnet-publish.md) comando.

Se você quiser direcionar mais de uma estrutura, poderá definir a `<TargetFrameworks>` configuração para vários valores de TFM, separados por um ponto-e-vírgula. Quando você cria seu aplicativo, uma compilação é produzida para cada estrutura de destino. No entanto, ao publicar seu aplicativo, você deve especificar a estrutura de destino com o `dotnet publish -f <TFM>` comando.

A menos que definido de outra forma, o diretório de saída do [`dotnet publish`](../tools/dotnet-publish.md) comando é `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/` . O modo **CONFIGURAÇÃO DE BUILD** padrão é **Depuração**, a menos que seja alterado com o parâmetro `-c`. Por exemplo, `dotnet publish -c Release -f netcoreapp2.1` publica em `./bin/Release/netcoreapp2.1/publish/`.

Se você usar o SDK do .NET Core 3,1 ou posterior, o modo de publicação padrão será _executável_ dependente da estrutura.

Se você usar SDK do .NET Core 2,1, o modo de publicação padrão será a _implantação_ dependente da estrutura.

### <a name="native-dependencies"></a>Dependências nativas

Se o aplicativo tiver dependências nativas, ele poderá não ser executado em um sistema operacional diferente. Por exemplo, se o aplicativo usar a API nativa do Windows, ele não será executado no macOS nem no Linux. Você precisará fornecer um código específico da plataforma e compilar um executável para cada plataforma.

Considere também que, se uma biblioteca referenciada tiver uma dependência nativa, o aplicativo poderá não ser executado em todas as plataformas. No entanto, é possível que um pacote NuGet referenciado tenha incluído versões específicas da plataforma para lidar com as dependências nativas necessárias para você.

Ao distribuir um aplicativo com dependências nativas, talvez você precise usar a opção `dotnet publish -r <RID>` para especificar a plataforma de destino na qual deseja publicar. Para obter uma lista de identificadores de runtime, confira o [Catálogo do RID (Identificador de Runtime)](../rid-catalog.md).

Mais informações sobre binários específicos da plataforma são abordadas nas seções [Executável dependente de estrutura](#framework-dependent-executable) e [Implantação autossuficiente](#self-contained-deployment).

## <a name="sample-app"></a>Aplicativo de exemplo

Você pode usar o aplicativo a seguir para explorar os comandos de publicação. O aplicativo é criado pela execução dos seguintes comandos no terminal:

```dotnetcli
mkdir apptest1
cd apptest1
dotnet new console
dotnet add package Figgle
```

O arquivo `Program.cs` ou `Program.vb` gerado pelo modelo de console precisa ser alterado para o seguinte:

```csharp
using System;

namespace apptest1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"));
        }
    }
}
```

```vb
Module Program
    Sub Main(args As String())
        Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"))
    End Sub
End Module
```

Quando você executa o aplicativo ( [`dotnet run`](../tools/dotnet-run.md) ), a seguinte saída é exibida:

```terminal
  _   _      _ _         __        __         _     _ _
 | | | | ___| | | ___    \ \      / /__  _ __| | __| | |
 | |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
 |  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
 |_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
                     |/
```

## <a name="framework-dependent-deployment"></a>Implantação dependente de estrutura

Para a CLI do SDK do .NET Core 2,1, a implantação dependente da estrutura (FDD) é o modo padrão para o `dotnet publish` comando básico. Em SDKs mais recentes, o [executável dependente da estrutura](#framework-dependent-executable) é o padrão.

Quando você publica o aplicativo como uma FDD, um arquivo `<PROJECT-NAME>.dll` é criado na pasta `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/`. Para executar o aplicativo, navegue para a pasta de saída e use o comando `dotnet <PROJECT-NAME>.dll`.

Seu aplicativo está configurado para ter como destino uma versão específica do .NET. Esse tempo de execução do .NET direcionado deve estar em qualquer computador onde seu aplicativo é executado. Por exemplo, se seu aplicativo for destinado ao .NET Core 3,1, qualquer computador em que seu aplicativo é executado deve ter o tempo de execução do .NET Core 3,1 instalado. Conforme indicado na seção [Noções básicas de publicação](#publishing-basics), você pode editar o arquivo de projeto para alterar a estrutura de destino padrão ou para definir mais de uma estrutura como destino.

A publicação de um FDD cria um aplicativo que avança automaticamente para o patch de segurança do .NET mais recente disponível no sistema que executa o aplicativo. Para obter mais informações sobre a associação de versão no momento da compilação, consulte [selecionar a versão do .net a ser usada](../versions/selection.md#framework-dependent-apps-roll-forward).

| Modo de publicação                   | Versão do SDK | Comando                                                     |
|--------------------------------|-------------|-------------------------------------------------------------|
| Implantação dependente de estrutura | 2.1         | `dotnet publish -c Release`                                 |
|                                | 3.1         | `dotnet publish -c Release -p:UseAppHost=false`             |
|                                | 5.0         | `dotnet publish -c Release -p:UseAppHost=false`             |

## <a name="framework-dependent-executable"></a>Executável dependente de estrutura

Para a CLI do SDK do .NET 5 (e .NET Core 3,1), o executável dependente da estrutura (FDE) é o modo padrão para o `dotnet publish` comando básico. Você não precisa especificar nenhum outro parâmetro, desde que queira direcionar o sistema operacional atual.

Nesse modo, um host do executável específico da plataforma é criado para hospedar o aplicativo multiplataforma. Esse modo é semelhante a FDD, pois FDD requer um host na forma do `dotnet` comando. O nome de arquivo executável do host varia de acordo com a plataforma e tem um nome semelhante a `<PROJECT-FILE>.exe` . Você pode executar esse executável diretamente em vez de chamar `dotnet <PROJECT-FILE>.dll` , o que ainda é uma maneira aceitável de executar o aplicativo.

Seu aplicativo está configurado para ter como destino uma versão específica do .NET. Esse tempo de execução do .NET direcionado deve estar em qualquer computador onde seu aplicativo é executado. Por exemplo, se seu aplicativo for destinado ao .NET Core 3,1, qualquer computador em que seu aplicativo é executado deve ter o tempo de execução do .NET Core 3,1 instalado. Conforme indicado na seção [Noções básicas de publicação](#publishing-basics), você pode editar o arquivo de projeto para alterar a estrutura de destino padrão ou para definir mais de uma estrutura como destino.

A publicação de um FDE cria um aplicativo que avança automaticamente para o patch de segurança do .NET mais recente disponível no sistema que executa o aplicativo. Para obter mais informações sobre a associação de versão no momento da compilação, consulte [selecionar a versão do .net a ser usada](../versions/selection.md#framework-dependent-apps-roll-forward).

Para o .NET 2,1, você deve usar as seguintes opções com o `dotnet publish` comando para publicar um FDE:

- `-r <RID>` Essa opção usa um RID (identificador) para especificar a plataforma de destino. Para obter uma lista de identificadores de runtime, confira o [Catálogo do RID (Identificador de Runtime)](../rid-catalog.md).

- `--self-contained false` Essa opção instrui o SDK do .NET Core a criar um executável como um FDE.

| Modo de publicação                   | Versão do SDK | Comando                                                     |
|--------------------------------|-------------|-------------------------------------------------------------|
| Executável dependente de estrutura | 3.1         | `dotnet publish -c Release -r <RID> --self-contained false`<br>`dotnet publish -c Release` |
|                                | 5.0         | `dotnet publish -c Release -r <RID> --self-contained false`<br>`dotnet publish -c Release` |

Sempre que você usa a opção `-r`, o caminho da pasta de saída é alterado para: `./bin/<BUILD-CONFIGURATION>/<TFM>/<RID>/publish/`

Se você usar o [aplicativo de exemplo](#sample-app), execute `dotnet publish -f net5.0 -r win10-x64 --self-contained false`. Esse comando cria o seguinte executável: `./bin/Debug/net5.0/win10-x64/publish/apptest1.exe`

> [!NOTE]
> Reduza o tamanho total da implantação habilitando o **modo invariável de globalização**. Esse modo é útil para aplicativos que não têm reconhecimento global e que podem usar as convenções de formatação, as convenções de uso de maiúsculas, a comparação de cadeia de caracteres e a ordem de classificação da [cultura invariável](xref:System.Globalization.CultureInfo.InvariantCulture). Para obter mais informações sobre o **modo invariável de globalização** e como habilitá-lo, consulte [modo invariável de globalização do .net](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).

## <a name="self-contained-deployment"></a>Implantação autocontida

Quando você publica uma SCD (implantação autônoma), o SDK do .NET cria um executável específico da plataforma. A publicação de uma SCD inclui todos os arquivos .NET necessários para executar seu aplicativo, mas não inclui as [dependências nativas do .net](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md). Essas dependências precisam estar presentes no sistema antes da execução do aplicativo.

A publicação de uma SCD cria um aplicativo que não avança para o patch de segurança .NET mais recente disponível. Para obter mais informações sobre a associação de versão no momento da compilação, consulte [selecionar a versão do .net a ser usada](../versions/selection.md#self-contained-deployments-include-the-selected-runtime).

É necessário usar as seguintes opções com o comando `dotnet publish` para publicar uma SCD:

- `-r <RID>` Essa opção usa um RID (identificador) para especificar a plataforma de destino. Para obter uma lista de identificadores de runtime, confira o [Catálogo do RID (Identificador de Runtime)](../rid-catalog.md).

- `--self-contained true` Essa opção instrui o SDK do .NET Core a criar um executável como uma SCD.

| Modo de publicação                   | Versão do SDK | Comando                                                     |
|--------------------------------|-------------|-------------------------------------------------------------|
| Implantação autocontida      | 2.1         | `dotnet publish -c Release -r <RID> --self-contained true`  |
|                                | 3.1         | `dotnet publish -c Release -r <RID> --self-contained true`  |
|                                | 5.0         | `dotnet publish -c Release -r <RID> --self-contained true`  |

> [!NOTE]
> Reduza o tamanho total da implantação habilitando o **modo invariável de globalização**. Esse modo é útil para aplicativos que não têm reconhecimento global e que podem usar as convenções de formatação, as convenções de uso de maiúsculas, a comparação de cadeia de caracteres e a ordem de classificação da [cultura invariável](xref:System.Globalization.CultureInfo.InvariantCulture). Para obter mais informações sobre o **modo invariável de globalização** e como habilitá-lo, consulte [modo invariável de globalização do .NET Core](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).

## <a name="see-also"></a>Consulte também

- [Visão geral da implantação de aplicativos .NET](index.md)
- [Catálogo do RID (.NET Runtime IDentifier)](../rid-catalog.md)
