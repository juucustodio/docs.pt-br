---
title: Estruturas de destino em projetos em estilo SDK-.NET
description: Saiba mais sobre estruturas de destino para aplicativos e bibliotecas .NET.
ms.date: 09/08/2020
ms.custom: updateeachrelease
ms.technology: dotnet-standard
ms.openlocfilehash: 9c5d3605f893072b2a5e84751e3657152ac0213e
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598155"
---
# <a name="target-frameworks-in-sdk-style-projects"></a>Estruturas de destino em projetos no estilo SDK

Ao destinar a uma estrutura em um aplicativo ou uma biblioteca, você está especificando o conjunto de APIs que deseja disponibilizar para o aplicativo ou a biblioteca. Você especifica a estrutura de destino no arquivo de projeto usando monikers de estrutura de destino (TFMs).

Um aplicativo ou uma biblioteca pode ser destinada a uma versão do [.NET Standard](net-standard.md). As versões do .NET Standard representam conjuntos de APIs padronizadas entre todas as implementações do .NET. Por exemplo, uma biblioteca pode se destinar ao NET Standard 1.6 e obter acesso a APIs que funcionam no .NET Core e .NET Framework usando a mesma base de código.

Um aplicativo ou uma biblioteca também pode se destinar a uma implementação específica do .NET para obter acesso a APIs específicas de implementação. Por exemplo, um aplicativo que se destina ao Xamarin. iOS (por exemplo, `Xamarin.iOS10` ) tem acesso aos wrappers de API do IOS fornecidos pelo Xamarin para IOS 10, ou um aplicativo que tem como alvo plataforma universal do Windows (UWP `uap10.0` ) tem acesso a APIs que são compiladas para dispositivos que executam o Windows 10.

Para algumas estruturas de destino (por exemplo, .NET Framework), as APIs são definidas pelos assemblies que a estrutura instala em um sistema e podem incluir APIs de estrutura de aplicativo (por exemplo, ASP.NET).

Para estruturas de destino com base em pacote (por exemplo, .NET Standard e .NET Core), as APIs são definidas pelos pacotes incluídos no aplicativo ou na biblioteca. Um *metapacote* é um pacote NuGet que não tem nenhum conteúdo próprio, mas é uma lista de dependências (outros pacotes). Uma estrutura de destino com base em pacote NuGet especifica implicitamente um metapacote que faz referência a todos os pacotes que, juntos, compõem a estrutura.

## <a name="latest-versions"></a>Versões mais recentes

A tabela a seguir define as estruturas de destino mais comuns, como elas são referenciadas e qual versão do [.NET Standard](net-standard.md) elas implementam. Estas versões de estrutura de destino são as versões estáveis mais recentes. As versões de pré-lançamento não são mostradas. Um moniker de estrutura de destino (TFM) é um formato de token padronizado para especificar a estrutura de destino de um aplicativo ou biblioteca .NET.

| Estrutura de destino      | Última <br/> versão estável | Moniker da estrutura de destino (TFM) | Implementado <br/> Versão do .NET Standard |
| :-: | :-: | :-: | :-: |
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

Você também pode especificar uma versão de so opcional, por exemplo, `net5.0-ios12.0` .

Para obter mais informações sobre o .NET 5 TFMs, consulte [nomes de estrutura de destino no .NET 5](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md).

## <a name="how-to-specify-a-target-framework"></a>Como especificar uma estrutura de destino

As estruturas de destino são especificadas em um arquivo de projeto. Quando uma única estrutura de destino é especificada, use o elemento **TargetFramework**. O arquivo de projeto de aplicativo de console a seguir demonstra como direcionar o .NET 5,0:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

</Project>
```

Ao especificar várias estruturas de destino, você pode fazer referência a assemblies para cada estrutura de destino de forma condicional. Em seu código, você pode condicionalmente compilar em relação a esses assemblies usando símbolos de pré-processador com a lógica *if-then-else*.

O projeto de biblioteca a seguir destina-se a APIs de .NET Standard ( `netstandard1.4` ) e .NET Framework ( `net40` e `net45` ). Use o elemento **TargetFrameworks** plural com várias estruturas de destino. Os `Condition` atributos incluem pacotes específicos de implementação quando a biblioteca é compilada para os dois .NET Framework TFMs:

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

O sistema de compilação reconhece os símbolos de pré-processador que representam as estruturas de destino mostradas na tabela de [versões do Framework de destino com suporte](#supported-target-frameworks) quando você está usando projetos em estilo SDK. Ao usar um símbolo que representa um TFM do .NET Standard ou .NET Core, substitua o ponto por um sublinhado e altere as letras minúsculas por maiúsculas (por exemplo, o símbolo de `netstandard1.4` é `NETSTANDARD1_4`).

A lista completa de símbolos de pré-processador para estruturas de destino do .NET Core é:

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

## <a name="see-also"></a>Confira também

- [Desenvolver bibliotecas com as ferramentas de plataforma cruzada](../core/tutorials/libraries.md)
- [.NET Standard](net-standard.md)
- [Controle de versão do .NET Core](../core/versions/index.md)
- [Repositório GitHub dotnet/standard](https://github.com/dotnet/standard)
- [Repositório GitHub de Ferramentas NuGet](https://github.com/joelverhagen/NuGetTools)
- [Perfis de estrutura no .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)
