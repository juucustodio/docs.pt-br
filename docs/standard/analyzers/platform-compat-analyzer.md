---
title: Analisador de compatibilidade de plataforma
description: Um analisador de Roslyn que pode ajudar a detectar problemas de compatibilidade de plataforma em aplicativos e bibliotecas de plataforma cruzada.
author: buyaa-n
ms.date: 09/17/2020
ms.openlocfilehash: 6ba521110e21e169955c54faf5c2a16c2838335b
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99426990"
---
# <a name="platform-compatibility-analyzer"></a>Analisador de compatibilidade de plataforma

Você provavelmente já ouviu o lema de "um .NET": uma única plataforma unificada para criar qualquer tipo de aplicativo. O SDK do .NET 5,0 inclui ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin e ML.NET, e adicionará suporte para mais plataformas ao longo do tempo. O .NET 5,0 se esforça para fornecer uma experiência em que você não tem de ponderar sobre os diferentes tipos de .NET, mas não tenta abstrair completamente o sistema operacional subjacente (SO). Você continuará a ser capaz de chamar APIs específicas da plataforma, por exemplo, P/Invokes, WinRT ou as associações do Xamarin para iOS e Android.

Mas usar APIs específicas da plataforma em um componente significa que o código não funciona mais em todas as plataformas. Precisávamos de uma maneira de detectar isso em tempo de design para que os desenvolvedores obtenham diagnósticos quando inadvertidamente usam APIs específicas da plataforma. Para atingir esse objetivo, o .NET 5,0 apresenta o [analisador de compatibilidade de plataforma](../../fundamentals/code-analysis/quality-rules/ca1416.md) e APIs complementares para ajudar os desenvolvedores a identificar e usar APIs específicas da plataforma, quando apropriado.

As novas APIs incluem:

- <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> anotar APIs como sendo específicas da plataforma e <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> anotar APIs como sem suporte em um sistema operacional específico. Esses atributos podem, opcionalmente, incluir o número de versão e já foram aplicados a algumas APIs específicas da plataforma nas principais bibliotecas do .NET.
- `Is<Platform>()` e `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` métodos estáticos na <xref:System.OperatingSystem?displayProperty=nameWithType> classe para chamar com segurança APIs específicas da plataforma. Por exemplo, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> pode ser usado para proteger uma chamada para uma API específica do Windows e <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> () pode ser usado para proteger uma chamada de API específica do Windows com versão. Veja esses [exemplos](#guard-platform-specific-apis-with-guard-methods) de como esses métodos podem ser usados como proteções de referências de API específicas da plataforma.

> [!TIP]
> O analisador de compatibilidade de plataforma atualiza e substitui o recurso de [detecção de problemas entre plataformas](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) do [analisador de API .net](../../standard/analyzers/api-analyzer.md).

## <a name="prerequisites"></a>Pré-requisitos

O analisador de compatibilidade de plataforma é um dos analisadores de qualidade de código Roslyn. Do .NET 5.0 em diante, esses analisadores estão [incluídos no SDK do .NET](../../fundamentals/code-analysis/overview.md). O analisador de compatibilidade de plataforma é habilitado por padrão somente para projetos direcionados `net5.0` ou para uma versão posterior. No entanto, você pode [habilitá-lo](../../fundamentals/code-analysis/quality-rules/ca1416.md#configure-code-to-analyze) para projetos direcionados a outras estruturas.

## <a name="how-the-analyzer-determines-platform-dependency"></a>Como o analisador determina a dependência da plataforma

- Uma **API** não-atributo é considerada para funcionar em **todas as plataformas de sistema operacional**.
- Uma API marcada com `[SupportedOSPlatform("platform")]` é considerada apenas portátil para o sistema operacional especificado `platform` .
  - O atributo pode ser aplicado várias vezes para indicar **suporte a várias plataformas** ( `[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]` ).
  - O analisador produzirá um **aviso** se as APIs específicas da plataforma forem referenciadas sem um **contexto de plataforma** adequado:
    - **Avisa** se o projeto não visa a plataforma com suporte (por exemplo, uma chamada à API específica do Windows e os destinos do projeto `<TargetFramework>net5.0-ios14.0</TargetFramework>` ).
    - **Avisa** se o projeto tem vários destinos (por exemplo, `<TargetFrameworks>net5.0;netstandard2.0</TargetFrameworks>` ).
    - **Não avisa** se a API específica da plataforma é referenciada em um projeto que se destina a qualquer uma das **plataformas especificadas** (por exemplo, para uma chamada de API específica do Windows e os destinos do projeto `<TargetFramework>net5.0-windows</TargetFramework>` ).
    - **Não avisará** se a chamada à API específica da plataforma for protegida por métodos de verificação de plataforma correspondentes (por exemplo, `if(OperatingSystem.IsWindows())` ).
    - **Não avisa** se a API específica da plataforma é referenciada do mesmo contexto específico da plataforma (o **site de chamada também é atribuído** com `[SupportedOSPlatform("platform")` ).
- Uma API marcada com `[UnsupportedOSPlatform("platform")]` é considerada não suportada apenas no sistema operacional especificado `platform` , mas com suporte para todas as outras plataformas.
  - O atributo pode ser aplicado várias vezes com diferentes plataformas, por exemplo, `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]` .
  - O analisador produzirá um **aviso** somente se o `platform` estiver em vigor para o site de chamada:
    - **Avisa** se o projeto se destina à plataforma que é atribuída como sem suporte (por exemplo, se a API for atribuída com `[UnsupportedOSPlatform("windows")]` e os destinos do site de chamada `<TargetFramework>net5.0-windows</TargetFramework>` ).
    - **Avisa** se o projeto tem vários destinos e se `platform` está incluído no grupo de itens padrão [do `<SupportedPlatform>` MSBuild](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) ou `platform` se está incluído manualmente dentro do grupo de `MSBuild` \<SupportedPlatform> itens:

      ```XML
      <ItemGroup>
          <SupportedPlatform Include="platform" />
      </ItemGroup>
      ```

    - **Não avisará** se você estiver criando um aplicativo que não tem como alvo a plataforma sem suporte ou que tem vários destinos e a plataforma não está incluída no grupo de itens padrão do [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) .
- Ambos os atributos podem ser instanciados com ou sem números de versão como parte do nome da plataforma.
  - Os números de versão estão no formato de `major.minor[.build[.revision]]` ; `major.minor` é necessário e `build` as `revision` partes e são opcionais. Por exemplo, "Windows 7.0" indica a versão 7,0 do Windows, mas "Windows" é interpretado como Windows 0,0.

Para obter mais informações, consulte [exemplos de como os atributos funcionam e quais diagnósticos eles causam](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).

### <a name="advanced-scenarios-for-combining-attributes"></a>Cenários avançados para combinar atributos

- Se uma combinação de `[SupportedOSPlatform]` `[UnsupportedOSPlatform]` atributos e estiver presente, todos os atributos serão agrupados pelo identificador de plataforma do sistema operacional:
  - **Lista somente com suporte**. Se a versão mais baixa de cada plataforma do sistema operacional for um `[SupportedOSPlatform]` atributo, a API será considerada como somente tendo suporte nas plataformas listadas e sem suporte por todas as outras plataformas. Os atributos opcionais `[UnsupportedOSPlatform]` para cada plataforma só podem ter uma versão mais alta da versão mínima com suporte, o que denota que a API é removida a partir da versão especificada.

    ```csharp
    // The API only supported on Windows 8.0 and later, not supported for all other.
    // The API is removed/unsupported from version 10.0.19041.0.
    [SupportedOSPlatform("windows8.0")]
    [UnsupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows80SupportFromCertainVersion();
    ```

  - **Lista somente sem suporte**. Se a versão mais baixa de cada plataforma do sistema operacional for um `[UnsupportedOSPlatform]` atributo, a API será considerada como sem suporte nas plataformas listadas e com suporte de todas as outras plataformas. A lista pode ter `[SupportedOSPlatform]` um atributo com a mesma plataforma, mas uma versão superior, que indica que a API tem suporte a partir dessa versão.

    ```csharp
    // The API was unsupported on Windows until version 10.0.19041.0.
    // The API is considered supported everywhere else without constraints.
    [UnsupportedOSPlatform("windows")]
    [SupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows8UnsupportFromWindows10();
    ```

  - **Lista inconsistente**. Se a versão mais baixa de algumas plataformas for `[SupportedOSPlatform]` `[UnsupportedOSPlatform]` para outras plataformas, será considerada inconsistente, o que não tem suporte para o analisador.
  - Se as versões mais baixas `[SupportedOSPlatform]` dos `[UnsupportedOSPlatform]` atributos e forem iguais, o analisador considerará a plataforma como parte da **lista somente com suporte**.
- Atributos de plataforma podem ser aplicados a tipos, Membros (métodos, campos, propriedades e eventos) e assemblies com diferentes nomes de plataforma ou versões.
  - Os atributos aplicados no nível superior `target` afetam todos os seus membros e tipos.
  - Os atributos de nível filho só se aplicam se eles aderem à regra "as anotações filhas podem restringir o suporte a plataformas, mas não podem ampliá-la".
    - Quando o pai tem **suporte apenas para** a lista, os atributos de membro filho não podem adicionar um novo suporte de plataforma, pois isso estaria estendendo o suporte pai. O suporte para uma nova plataforma só pode ser adicionado ao próprio pai. Mas o filho pode ter o `Supported` atributo para a mesma plataforma com versões posteriores que reduz o suporte. Além disso, o filho pode ter o `Unsupported` atributo com a mesma plataforma que também limita o suporte pai.
    - Quando o pai tem uma lista **somente sem suporte** , os atributos de membro filho podem adicionar suporte para uma nova plataforma, pois isso limita o suporte pai. Mas ele não pode ter o `Supported` atributo para a mesma plataforma que o pai, pois isso estende o suporte pai. O suporte para a mesma plataforma só pode ser adicionado ao pai em que o `Unsupported` atributo original foi aplicado.
  - Se `[SupportedOSPlatform("platformVersion")]` for aplicado mais de uma vez para uma API com o mesmo `platform` nome, o analisador apenas considerará aquela com a versão mínima.
  - Se `[UnsupportedOSPlatform("platformVersion")]` for aplicado mais de duas vezes para uma API com o mesmo `platform` nome, o analisador apenas considerará as duas com as versões mais antigas.

  > [!NOTE]
  > Uma API que era suportada inicialmente, mas sem suporte (removida) em uma versão posterior não é esperada para ser suportada novamente em uma versão posterior.

### <a name="examples-of-how-the-attributes-work-and-what-diagnostics-they-produce"></a>Exemplos de como os atributos funcionam e quais diagnósticos eles produzem

  ```csharp
  // An API supported only on Windows.
  [SupportedOSPlatform("Windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  public void Caller()
  {
      WindowsOnlyApi(); // warns: 'WindowsOnlyApi' is supported on 'windows'

      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Windows'
      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Linux'
      SupportedOnWindowsAndLinuxOnly();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 8.0 and later
      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // for same platform analyzer only warn for the latest version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  public void Caller2()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'android'

      // warns:'StartedWindowsSupportFromVersion8' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFromVersion8' is supported on 'windows' 8.0 and later
      StartedWindowsSupportFromVersion8();

      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is supported on 'windows' 8.0 and later
      // even there were 3 diagnostics found analyzer warn only for the first 2.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

## <a name="handle-reported-warnings"></a>Manipular avisos relatados

A maneira recomendada de lidar com esses diagnósticos é certificar-se de que você só chame APIs específicas da plataforma ao executar em uma plataforma apropriada. A seguir estão as opções que você pode usar para resolver os avisos; Escolha o que for mais apropriado para sua situação:

- **Proteja a chamada**. Você pode conseguir isso chamando condicionalmente o código em tempo de execução. Verifique se você está executando o em um desejado `Platform` usando um dos métodos de verificação de plataforma, por exemplo, `OperatingSystem.Is<Platform>()` ou `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` .

- **Marque o local de chamada como específico da plataforma**. Você também pode optar por marcar suas próprias APIs como sendo específicas da plataforma, apenas encaminhando efetivamente os requisitos para seus chamadores. Marque o método ou tipo recipiente ou o assembly inteiro com os mesmos atributos que a chamada dependente de plataforma referenciada. [Exemplos](#mark-call-site-as-platform-specific).

- **Declare o site de chamada com verificação de plataforma**. Se você não quiser a sobrecarga de uma `if` instrução adicional em tempo de execução, use <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> . [Exemplo](#assert-the-call-site-with-platform-check).

- **Exclua o código**. Geralmente, não é o que você deseja porque isso significa que você perde a fidelidade quando seu código é usado por usuários do Windows. Para casos em que existe uma alternativa de plataforma cruzada, você provavelmente é melhor usá-la em APIs específicas da plataforma.

- **Suprimir o aviso**. Você também pode simplesmente suprimir o aviso, seja por meio de uma entrada EditorConfig ou `#pragma warning disable ca1416` . No entanto, essa opção deve ser um último recurso ao usar APIs específicas da plataforma.

### <a name="guard-platform-specific-apis-with-guard-methods"></a>Proteger APIs específicas da plataforma com métodos de proteção

O nome da plataforma do método de proteção deve corresponder ao nome da plataforma de API dependente de plataforma de chamada. Se a cadeia de caracteres de plataforma da API de chamada incluir a versão:

- Para o `[SupportedOSPlatform("platformVersion")]` atributo, a plataforma do método de proteção `version` deve ser maior ou igual às plataformas de chamada `Version` .
- Para o `[UnsupportedOSPlatform("platformVersion")]` atributo, a plataforma do método de proteção `version` deve ser menor ou igual ao da plataforma de chamada `Version` .

  ```csharp
  public void CallingSupportedOnlyApis() // Allow list calls
  {
      if (OperatingSystem.IsWindows())
      {
          WindowsOnlyApi(); // will not warn
      }

      if (OperatingSystem.IsLinux())
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn, within one of the supported context
      }

      // Can use &&, || logical operators to guard combined attributes
      if (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10.0.19041)))
      {
          ApiSupportedFromWindows8UnsupportFromWindows10();
      }

      if (OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903))
      {
          AssemblySupportedOnWindowsApiSupportedFromWindows10(); // Only need to check latest supported version
      }
  }

  public void CallingUnsupportedApis()
  {
      if (!OperatingSystem.IsAndroid())
      {
          DoesNotWorkOnAndroid(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || OperatingSystem.IsWindowsVersionAtLeast(8))
      {
          StartedWindowsSupportFromVersion8(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || // supported all other platforms
         (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903)))
      {
          StartedWindowsSupportFrom8UnsupportedFrom10(); // will not warn
      }
  }
  ```

- Se você precisar proteger código direcionado `netstandard` ou `netcoreapp` onde novas <xref:System.OperatingSystem> APIs não estão disponíveis, a <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> API poderá ser usada e será respeitada pelo analisador. Mas não é tão otimizado quanto as novas APIs adicionadas no <xref:System.OperatingSystem> . Se a plataforma não tiver suporte na <xref:System.Runtime.InteropServices.OSPlatform> estrutura, você poderá chamar <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> e passar o nome da plataforma, que o analisador também respeita.

  ```csharp
  public void CallingSupportedOnlyApis()
  {
      if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn
      }

      if (RuntimeInformation.IsOSPlatform(OSPlatform.Create("browser")))
      {
          ApiOnlySupportedOnBrowser(); // call of browser specific API
      }
  }
  ```

### <a name="mark-call-site-as-platform-specific"></a>Marcar site de chamada como específico da plataforma

Os nomes de plataforma devem corresponder à API dependente de plataforma de chamada. Se a cadeia de caracteres da plataforma incluir uma versão:

- Para o `[SupportedOSPlatform("platformVersion")]` atributo, a plataforma do site de chamada `version` deve ser maior ou igual ao da plataforma de chamada `Version`
- Para o `[UnsupportedOSPlatform("platformVersion")]` atributo, a plataforma do site de chamada `version` deve ser menor ou igual ao da plataforma de chamada `Version`

  ```csharp
  // an API supported only on Windows.
  [SupportedOSPlatform("windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  [SupportedOSPlatform("windows8.0")] // call site attributed Windows 8.0 or above.
  public void Caller()
  {
      WindowsOnlyApi(); // will not warn as call site is for Windows.

      // will not warn as call site is for Windows.
      SupportedOnWindowsAndLinuxOnly();

      // will not warn for the API's [SupportedOSPlatform("windows8.0")] attribute.
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // as the call site version is lower than calling version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows11.0")] // call site attributed with windows 11.0 or above.
  public void Caller2()
  {
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // will not warn as call site version higher than calling API.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")] // call site supports Windows from version 8.0 to 10.0.19041.0.
  public void Caller3()
  {
      // will not warn as caller has exact same attributes.
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // As call site stopped support from that version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on Android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  [UnsupportedOSPlatform("windows")] // Caller no support Windows for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'Android'.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }

  [UnsupportedOSPlatform("windows")]
  [UnsupportedOSPlatform("android")] // Caller not support Windows and Android for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // will not warn as call site not supports Android.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

### <a name="assert-the-call-site-with-platform-check"></a>Declarar o site de chamada com verificação de plataforma

Todas as verificações condicionais usadas nos [exemplos do Platform Guard](#guard-platform-specific-apis-with-guard-methods) também podem ser usadas como a condição para <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> .

  ```csharp
  // An API supported only on Linux.
  [SupportedOSPlatform("linux")]
  public void LinuxOnlyApi() { }

  public void Caller()
  {
      Debug.Assert(OperatingSystem.IsLinux());

      LinuxOnlyApi(); // will not warn
  }
  ```

## <a name="see-also"></a>Confira também

- [Nomes de estrutura de destino no .NET 5](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [Anotando APIs específicas da plataforma e detectando seu uso](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-checks/platform-checks.md)
- [Anotando APIs como sem suporte em plataformas específicas](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-exclusion/platform-exclusion.md)
- [Analisador de compatibilidade de plataforma CA1416](../../fundamentals/code-analysis/quality-rules/ca1416.md)
- [Analisador de API do .NET](../../standard/analyzers/api-analyzer.md)
