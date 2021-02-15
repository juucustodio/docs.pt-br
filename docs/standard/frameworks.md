---
title: Estruturas de destino em projetos em estilo SDK-.NET
description: Saiba mais sobre estruturas de destino para aplicativos e bibliotecas .NET.
ms.date: 11/06/2020
ms.prod: dotnet
ms.custom: updateeachrelease
ms.technology: dotnet-standard
ms.openlocfilehash: 7a3dcd61c330607bacf0d05dbd775c62cfa15b37
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97765053"
---
# <a name="target-frameworks-in-sdk-style-projects"></a>Estruturas de destino em projetos no estilo SDK

Ao destinar a uma estrutura em um aplicativo ou uma biblioteca, você está especificando o conjunto de APIs que deseja disponibilizar para o aplicativo ou a biblioteca. Você especifica a estrutura de destino no arquivo de projeto usando um moniker de estrutura de destino (TFM).

Um aplicativo ou uma biblioteca pode ser destinada a uma versão do [.NET Standard](net-standard.md). As versões do .NET Standard representam conjuntos de APIs padronizadas entre todas as implementações do .NET. Por exemplo, uma biblioteca pode se destinar ao NET Standard 1.6 e obter acesso a APIs que funcionam no .NET Core e .NET Framework usando a mesma base de código.

Um aplicativo ou uma biblioteca também pode se destinar a uma implementação específica do .NET para obter acesso a APIs específicas de implementação. Por exemplo, um aplicativo que se destina ao Xamarin. iOS (por exemplo, `Xamarin.iOS10` ) tem acesso aos wrappers de API do IOS fornecidos pelo Xamarin para IOS 10, ou um aplicativo que tem como alvo plataforma universal do Windows (UWP `uap10.0` ) tem acesso a APIs que são compiladas para dispositivos que executam o Windows 10.

Para algumas estruturas de destino, como .NET Framework, as APIs são definidas pelos assemblies que a estrutura instala em um sistema e podem incluir APIs de estrutura de aplicativo (por exemplo, ASP.NET).

Para estruturas de destino baseadas em pacote (por exemplo, .NET 5, .NET Core e .NET Standard), as APIs são definidas pelos pacotes NuGet incluídos no aplicativo ou na biblioteca.

## <a name="latest-versions"></a>Versões mais recentes

A tabela a seguir define as estruturas de destino mais comuns, como elas são referenciadas e qual versão do [.net Standard](net-standard.md) elas implementam. Estas versões de estrutura de destino são as versões estáveis mais recentes. As versões de pré-lançamento não são mostradas. Um moniker de estrutura de destino (TFM) é um formato de token padronizado para especificar a estrutura de destino de um aplicativo ou biblioteca .NET.

| Estrutura de destino      | Última <br/> versão estável | Moniker da estrutura de destino (TFM) | Implementado <br/> Versão do .NET Standard |
| :-: | :-: | :-: | :-: |
| .NET 5                | 5.0                         | NET 5.0                         | N/D                                     |
| .NET Standard         | 2.1                         | netstandard 2.1                 | N/D                                     |
| .NET Core             | 3.1                         | netcoreapp 3.1                  | 2.1                                     |
| .NET Framework        | 4.8                         | net48                          | 2,0                                     |

## <a name="supported-target-frameworks"></a>Estruturas de destino com suporte

Normalmente, uma estrutura de destino é referenciada por um TFM. A tabela a seguir mostra as estruturas de destino com suporte pelo SDK do .NET e o cliente NuGet. Equivalentes estão mostrados entre colchetes. Por exemplo, `win81` é um TFM equivalente ao `netcore451`.

| Estrutura de Destino           | TFM |
| -------------------------- | --- |
| .NET 5 (e .NET Core)     | netcoreapp1.0<br>netcoreapp1.1<br>netcoreapp2.0<br>netcoreapp2.1<br>netcoreapp2.2<br>netcoreapp 3.0<br>netcoreapp 3.1<br>NET 5.0 * |
| .NET Standard              | netstandard1.0<br>netstandard1.1<br>netstandard1.2<br>netstandard1.3<br>netstandard1.4<br>netstandard1.5<br>netstandard1.6<br>netstandard2.0<br>netstandard 2.1 |
| .NET Framework             | net11<br>net20<br>net35<br>net40<br>net403<br>net45<br>net451<br>net452<br>net46<br>net461<br>net462<br>net47<br>net471<br>net472<br>net48 |
| Windows Store              | netcore [netcore45]<br>netcore45 [win] [win8]<br>netcore451 [win81] |
| .NET Micro Framework       | netmf |
| Silverlight                | sl4<br>sl5 |
| Windows Phone              | wp [wp7]<br>wp7<br>wp75<br>wp8<br>wp81<br>wpa81 |
| Plataforma Universal do Windows | uap [uap10.0]<br>uap10.0 [win10] [netcore50] |

\* O .NET 5,0 e versões posteriores TFMs incluem variações específicas do sistema operacional. Para obter mais informações, consulte a seguinte seção, [TFMs específica do sistema operacional .NET 5](#net-5-os-specific-tfms).

### <a name="net-5-os-specific-tfms"></a>TFMs específico do .NET 5 OS

Para cada .NET 5,0 e TFM posterior, por exemplo, `net5.0` há variações de TFM que incluem associações específicas do sistema operacional. Essas variações são mostradas na tabela a seguir.

| Formato específico do sistema operacional | Exemplo        |
|--------------------|----------------|
| \<base-tfm>-Android | NET 5.0 – Android |
| \<base-tfm>-Ios     | NET 5.0-Ios     |
| \<base-tfm>-MacOS   | NET 5.0 – MacOS   |
| \<base-tfm>-TVOs    | NET 5.0-TVOs    |
| \<base-tfm>-watchos | NET 5.0-watchos |
| \<base-tfm>-7.5.0 | NET 5.0-Windows |

O `net5.0` TFM inclui apenas tecnologias que funcionam entre plataformas. A especificação de um TFM específico do sistema operacional torna APIs específicas a um sistema operacionais disponíveis para seu aplicativo, por exemplo, Windows Forms ou associações do iOS. OS TFMs específicos do so também herdam todas as APIs disponíveis para o `net5.0` TFM.

Para tornar seu aplicativo portável em diferentes plataformas, você pode direcionar vários TFMs específicos do sistema operacional e adicionar a plataforma guardas ao redor de chamadas de API específicas do sistema operacional usando `#if` diretivas de pré-processador.

A tabela a seguir mostra a compatibilidade do .NET 5 TFMs com o TFMs para versões anteriores do .NET.

| TFM             | Compatível com                                            | Observações |
|-----------------|------------------------------------------------------------|-|
| NET 5.0          | net1.. 4 (com aviso NU1701)<br />netcoreapp1.. 3,1 (aviso quando o WinForms ou o WPF é referenciado)<br />netstandard1.. 2,1 | |
| NET 5.0 – Android  | xamarin. Android (além de tudo o mais herdado `net5.0` ) | |
| NET 5.0-Ios      | xamarin. Ios (além de tudo o mais herdado `net5.0` ) | |
| NET 5.0 – MacOS    | xamarin. Mac (além de tudo o mais herdado `net5.0` ) | |
| NET 5.0-TVOs     | xamarin. TVOs (além de tudo o mais herdado `net5.0` ) | |
| NET 5.0-watchos  | xamarin. watchos (além de tudo o mais herdado `net5.0` ) | |
| NET 5.0-Windows  | netcoreapp1.. 3,1 (além de tudo o mais herdado `net5.0` ) | Inclui as APIs WinForms, WPF e UWP.<br />Para obter informações, consulte [chamar APIs de Windows Runtime em aplicativos da área de trabalho](/windows/apps/desktop/modernize/desktop-to-uwp-enhance). |

#### <a name="suggested-targets"></a>Destinos sugeridos

Use estas diretrizes para determinar qual TFM usar em seu aplicativo:

- Os aplicativos que são portáteis para várias plataformas devem ter como destino `net5.0` . Isso inclui a maioria das bibliotecas, mas também ASP.NET Core e Entity Framework.

- Bibliotecas específicas da plataforma devem ter como destino tipos específicos da plataforma. Por exemplo, os WinForms e projetos do WPF devem ter como destino `net5.0-windows` .

- Os modelos de aplicativos de plataforma cruzada (Xamarin Forms, ASP.NET Core) e os pacotes de ponte (Xamarin Essentials) devem ter pelo menos o destino `net5.0` , mas também podem ter outros tipos específicos de plataforma para liberar mais APIs ou recursos.

#### <a name="os-version-in-tfms"></a>Versão do so em TFMs

Você também pode especificar uma versão de sistema operacional opcional no final do TFM, por exemplo, `net5.0-ios13.0` , que indica quais APIs estão disponíveis para seu aplicativo. (O SDK do .NET 5 será atualizado para incluir suporte para versões mais recentes do sistema operacional à medida que elas forem lançadas.) Para obter acesso a APIs recentemente lançadas, aumente a versão do sistema operacional no TFM. Você ainda pode tornar seu aplicativo compatível com versões anteriores do sistema operacional (e adicionar proteções em chamadas para as APIs de versão posterior) adicionando o `SupportedOSPlatformVersion` elemento ao arquivo do projeto. O `SupportedOSPlatformVersion` elemento indica a versão mínima do sistema operacional necessária para executar seu aplicativo.

Por exemplo, o trecho de arquivo de projeto a seguir especifica que as APIs do iOS 14 estão disponíveis para o aplicativo, mas podem ser executadas em computadores iOS 13 ou posteriores.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0-ios14.0</TargetFramework>
    <SupportedOSPlatformVersion>13.0</SupportedOSPlatformVersion> (minimum os platform version)
  </PropertyGroup>

  ...

</Project>
```

## <a name="how-to-specify-a-target-framework"></a>Como especificar uma estrutura de destino

As estruturas de destino são especificadas em um arquivo de projeto. Quando uma estrutura de destino única for especificada, use o [elemento TargetFramework](../core/project-sdk/msbuild-props.md#targetframework). O arquivo de projeto de aplicativo de console a seguir demonstra como direcionar o .NET 5,0:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

</Project>
```

Ao especificar várias estruturas de destino, você pode fazer referência a assemblies para cada estrutura de destino de forma condicional. Em seu código, você pode condicionalmente compilar em relação a esses assemblies usando símbolos de pré-processador com a lógica *if-then-else*.

O projeto de biblioteca a seguir destina-se a APIs de .NET Standard ( `netstandard1.4` ) e .NET Framework ( `net40` e `net45` ). Use o [elemento TargetFrameworks](../core/project-sdk/msbuild-props.md#targetframeworks) do plural com várias estruturas de destino. Os `Condition` atributos incluem pacotes específicos de implementação quando a biblioteca é compilada para os dois .NET Framework TFMs:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.0 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net40' ">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.5 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net45' ">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>

</Project>
```

Em sua biblioteca ou aplicativo, você escreve o código condicional usando [diretivas de pré-processador](../csharp/language-reference/preprocessor-directives/preprocessor-if.md) para compilar para cada estrutura de destino:

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

O sistema de compilação reconhece os símbolos de pré-processador que representam as estruturas de destino mostradas na tabela de [versões do Framework de destino com suporte](#supported-target-frameworks) quando você está usando projetos em estilo SDK. Ao usar um símbolo que representa um .NET Standard, .NET Core ou .NET 5 TFM, substitua pontos e hifens por um sublinhado e altere as letras minúsculas para maiúsculas (por exemplo, o símbolo de `netstandard1.4` é `NETSTANDARD1_4` ).

A lista completa de símbolos de pré-processador para estruturas de destino do .NET é:

[!INCLUDE [Preprocessor symbols](../../includes/preprocessor-symbols.md)]

## <a name="deprecated-target-frameworks"></a>Estruturas de destino preteridas

As seguintes estruturas de destino estão preteridas. Os pacotes direcionados a essas estruturas de destino devem migrar para as substituições indicadas.

| TFM preterido                                                                             | Substituição |
| ------------------------------------------------------------------------------------------ | ----------- |
| aspnet50<br>aspnetcore50<br>dnxcore50<br>dnx<br>dnx45<br>dnx451<br>dnx452                  | netcoreapp  |
| dotnet<br>dotnet50<br>dotnet51<br>dotnet52<br>dotnet53<br>dotnet54<br>dotnet55<br>dotnet56 | netstandard |
| netcore50                                                                                  | uap10.0     |
| win                                                                                        | netcore45   |
| win8                                                                                       | netcore45   |
| win81                                                                                      | netcore451  |
| win10                                                                                      | uap10.0     |
| winrt                                                                                      | netcore45   |

## <a name="see-also"></a>Veja também

- [Nomes de estrutura de destino no .NET 5](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [Desenvolver bibliotecas com as ferramentas de plataforma cruzada](../core/tutorials/libraries.md)
- [.NET Standard](net-standard.md)
- [Controle de versão do .NET Core](../core/versions/index.md)
- [Repositório GitHub dotnet/standard](https://github.com/dotnet/standard)
- [Repositório GitHub de Ferramentas NuGet](https://github.com/joelverhagen/NuGetTools)
- [Perfis de estrutura no .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)
- [Analisador de compatibilidade de plataforma](analyzers/platform-compat-analyzer.md)
