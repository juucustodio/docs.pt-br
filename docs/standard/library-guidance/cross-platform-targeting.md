---
title: Direcionamento para bibliotecas do .NET multiplataforma
description: Recomendações de melhores práticas para a criação de bibliotecas do .NET multiplataforma.
ms.date: 08/12/2019
ms.openlocfilehash: 038a03904c4cfe49758562b5748fef06ae1afa4b
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189245"
---
# <a name="cross-platform-targeting"></a>Direcionamento multiplataforma

O .NET moderno dá suporte a vários sistemas operacionais e dispositivos. É importante para as bibliotecas de software livre do .NET dar suporte a desenvolvedores tantos quanto possível, estejam eles criando um site ASP.NET hospedado no Azure ou um jogo .NET no Unity.

## <a name="net-standard"></a>.NET Standard

O .NET standard é a melhor maneira de adicionar suporte multiplataforma a uma biblioteca do .NET. O [.NET Standard](../net-standard.md) é uma especificação de APIs .NET disponíveis em todas as implementações do .NET. O direcionamento de .NET Standard permite que você produza bibliotecas restritas para usar APIs que estão em uma determinada versão do .NET Standard, o que significa que ela pode ser usada por todas as plataformas que implementam essa versão do .NET Standard.

![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")

Ter como destino o .NET Standard e compilar com êxito o projeto não assegura que a biblioteca será executada com êxito em todas as plataformas:

1. APIs específicas da plataforma falharão em outras plataformas. Por exemplo, <xref:Microsoft.Win32.Registry?displayProperty=nameWithType> terá êxito no Windows e gerará <xref:System.PlatformNotSupportedException> em qualquer outro sistema operacional.
2. APIs podem se comportar de maneira diferente. Por exemplo, APIs de reflexão têm diferentes características de desempenho quando um aplicativo usa a compilação antecipada em iOS ou UWP.

> [!TIP]
> A equipe do .NET [oferece um analisador Roslyn](../analyzers/api-analyzer.md) para ajudá-lo a descobrir possíveis problemas.

✔️ FAÇA a inclusão de um destino `netstandard2.0`.

> A maioria das bibliotecas de uso não deve precisar de APIs fora do .NET Standard 2.0. O .NET standard 2.0 é compatível com todas as plataformas modernas e é a maneira recomendada de dar suporte a várias plataformas com um destino.

❌ Evite incluir um `netstandard1.x` destino.

> O .NET standard 1.x é distribuído como um conjunto granular de pacotes do NuGet, que cria um grande grafo de dependência de pacote e resulta em os desenvolvedores baixarem muitos pacotes durante o build. As implementações modernas do .NET dão suporte a .NET Standard 2,0. Você somente deverá direcionar o .NET Standard 1.x se precisar especificamente ter como destino uma plataforma mais antiga.

✔️ FAÇA a inclusão de um destino `netstandard2.0` se você precisar de um `netstandard1.x` destino.

> Todas as plataformas que dão suporte a .NET Standard 2.0 usarão o destino `netstandard2.0` e se beneficiarão de um grafo de pacote menor, enquanto plataformas mais antigas ainda funcionarão e farão fallback usando o destino `netstandard1.x`.

❌ Não inclua um destino .NET Standard se a biblioteca depender de um modelo de aplicativo específico da plataforma.

> Por exemplo, uma biblioteca do kit de ferramentas de controle UWP depende de um modelo de aplicativo disponível apenas em UWP. APIs específicas do modelo de aplicativo não estarão disponíveis no .NET Standard.

## <a name="multi-targeting"></a>Multiplataforma

Às vezes, você precisará acessar APIs específicas da estrutura de suas bibliotecas. A melhor maneira de chamar APIs específicas da estrutura é usando o múltiplos destinos, que compila seu projeto para muitas [estruturas de destino do .NET](../frameworks.md), em vez de apenas uma.

Para proteger seus consumidores de precisarem criar estrutura individuais, você deve se esforçar para ter uma saída do .NET Standard além de uma ou mais saídas específicas da estrutura. Com o destinos múltiplos, todos os assemblies são empacotados dentro de um único pacote NuGet. Os consumidores podem fazer referência o mesmo pacote e o NuGet escolherá a implementação apropriada. Sua biblioteca .NET Standard serve como a biblioteca de fallback usada em todos os lugares, exceto para casos em que o seu pacote do NuGet oferece uma implementação específica do framework. Ter destinos múltiplos permite que você use a compilação condicional em seu código e chame APIs específicas da estrutura.

![Pacote NuGet com vários assemblies](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "Pacote NuGet com vários assemblies")

✔️ CONSIDERE ter como destino implementações do .NET, além do .NET Standard.

> Ter como destinos implementações do .NET permite que você chame APIs específicas da plataforma que estão fora do .NET Standard.
>
> Não remova o suporte para o .NET Standard ao fazer isso. Em vez disso, geram da implementação e oferecem APIs de funcionalidade. Dessa forma, sua biblioteca pode ser usada em qualquer lugar e dá suporte à iluminação em runtime de recursos.

```csharp
public static class GpsLocation
{
    // This project uses multi-targeting to expose device-specific APIs to .NET Standard.
    public static async Task<(double latitude, double longitude)> GetCoordinatesAsync()
    {
#if NET461
        return CallDotNetFramworkApi();
#elif WINDOWS_UWP
        return CallUwpApi();
#else
        throw new PlatformNotSupportedException();
#endif
    }

    // Allows callers to check without having to catch PlatformNotSupportedException
    // or replicating the OS check.
    public static bool IsSupported
    {
        get
        {
#if NET461 || WINDOWS_UWP
            return true;
#else
            return false;
#endif
        }
    }
}
```

❌ EVITE usar multi-targeting, bem como o direcionamento do .NET Standard se o código-fonte for o mesmo para todos os destinos.

> O assembly .NET padrão será usado automaticamente pelo NuGet. Ter como destino implementações do .NET individuais aumenta o tamanho de `*.nupkg` sem nenhum benefício.

✔️ CONSIDERE adicionar um destino para `net461` quando você está oferecendo um destino `netstandard2.0`.

> Usar o .NET Standard 2.0 do .NET Framework tem alguns problemas que foram resolvidos no .NET Framework 4.7.2. Você pode melhorar a experiência para desenvolvedores que ainda estão no .NET Framework 4.6.1 a 4.7.1 oferecendo a eles um binário compilado para .NET Framework 4.6.1.

✔️ FAZER a distribuição de sua biblioteca usando um pacote NuGet.

> O NuGet seleciona o melhor destino para o desenvolvedor e os protege contra a necessidade de escolher a implementação apropriada.

✔️ FAÇA uso da propriedade `TargetFrameworks` de um arquivo de projeto quando tiver vários destinos.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <!-- This project will output netstandard2.0 and net461 assemblies -->
    <TargetFrameworks>netstandard2.0;net461</TargetFrameworks>
  </PropertyGroup>
</Project>
```

✔️ CONSIDERE usar [MSBuild.Sdk.Extras](https://github.com/onovotny/MSBuildSdkExtras) quando ter vários destinos para UWP e Xamarin, o que simplifica muito o seu arquivo de projeto.

## <a name="older-targets"></a>Destinos mais antigos

O .NET dá suporte a versões de direcionamento de .NET Framework que têm muito suporte, bem como plataformas que não são mais comumente usadas. Embora haja valor fazer sua biblioteca funcionar no máximo possível de destinos, precisar contornar APIs ausentes pode adicionar sobrecarga significativa. Acreditamos que não vale mais a pena ter determinadas estruturas como destino, considerando seu alcance e limitações.

❌ Não inclua um destino PCL (biblioteca de classes portátil). Por exemplo, `portable-net45+win8+wpa81+wp8`.

> O .NET standard é a maneira moderna de dar suporte a bibliotecas do .NET multiplataforma e substitui PCLs.

❌ Não inclua destinos para plataformas .NET que não têm mais suporte. Por exemplo, `SL4`, `WP`.

>[!div class="step-by-step"]
>[Anterior](get-started.md) 
> [Avançar](strong-naming.md)
