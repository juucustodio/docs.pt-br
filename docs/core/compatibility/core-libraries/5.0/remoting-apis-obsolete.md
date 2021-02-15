---
title: 'Alteração significativa: as APIs de comunicação remota estão obsoletas'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que algumas APIs relacionadas à comunicação remota são marcadas como obsoletas e geram um aviso com uma ID de diagnóstico Personalizada.
ms.date: 11/01/2020
ms.openlocfilehash: 5687b1471028b077674cfd31cb77ce95dc51bef5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760387"
---
# <a name="remoting-apis-are-obsolete"></a>As APIs de comunicação remota estão obsoletas

Algumas APIs relacionadas a comunicação remota são marcadas como obsoletas e geram um `SYSLIB0010` aviso no momento da compilação. Essas APIs podem ser removidas em uma versão futura do .NET.

## <a name="change-description"></a>Descrição das alterações

As seguintes APIs de comunicação remota estão marcadas como obsoletas.

| API | Marcado como obsoleto em... |
| - | - |
| <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType> | RC1 5,0 |
| <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType> | RC1 5,0 |

No .NET Framework 2. x-4. x, os <xref:System.MarshalByRefObject.GetLifetimeService> <xref:System.MarshalByRefObject.InitializeLifetimeService> métodos e controlam o tempo de vida das instâncias envolvidas com a comunicação remota do .net. No .NET Core 2. x-3. x, esses métodos sempre lançam um <xref:System.PlatformNotSupportedException> em tempo de execução.

No .NET 5,0 e versões posteriores, <xref:System.MarshalByRefObject.GetLifetimeService> os <xref:System.MarshalByRefObject.InitializeLifetimeService> métodos e são marcados como obsoletos como aviso, mas continuam a gerar um <xref:System.PlatformNotSupportedException> em tempo de execução.

```csharp
// MemoryStream, like all Stream instances, subclasses MarshalByRefObject.
MemoryStream stream = new MemoryStream();
// Throws PlatformNotSupportedException; also produces warning SYSLIB0010.
obj.InitializeLifetimeService();
```

Essa é uma alteração somente em tempo de compilação. Não há nenhuma alteração de tempo de execução de versões anteriores do .NET Core.

## <a name="reason-for-change"></a>Motivo da alteração

O [.NET Remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) é uma tecnologia herdada. Ele permite instanciar um objeto em outro processo (potencialmente mesmo em um computador diferente) e interagir com esse objeto como se fosse uma instância de objeto .NET comum e em processo. A infraestrutura de comunicação remota do .NET só existe no .NET Framework 2. x-4. x. O .NET Core e o .NET 5,0 e versões posteriores não têm suporte para a comunicação remota do .NET e as APIs de comunicação remota não existem ou sempre geram exceções nesses tempos de execução.

Para ajudar os desenvolvedores a se afastar dessas APIs, estamos obsoletingndo as APIs relacionadas à comunicação remota. Essas APIs podem ser totalmente removidas em uma versão futura do .NET.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

- Considere usar o WCF ou serviços REST baseados em HTTP para se comunicar com objetos em outros aplicativos ou entre computadores. Para obter mais informações, consulte [.NET Framework Technologies indisponíveis no .NET Core](../../../porting/net-framework-tech-unavailable.md).

- Se você precisar continuar a usar as APIs obsoletas, poderá suprimir o `SYSLIB0010` aviso no código.

  ```csharp
  MarshalByRefObject obj = GetMarshalByRefObj();
  #pragma warning disable SYSLIB0010 // Disable the warning.
  obj.InitializeLifetimeService(); // Still throws PNSE.
  obj.GetLifetimeService(); // Still throws PNSE.
  #pragma warning restore SYSLIB0010 // Reenable the warning.
  ```

  Você também pode suprimir o aviso em seu arquivo de projeto, o que desabilita o aviso para todos os arquivos de origem no projeto.

  ```xml
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
     <TargetFramework>net5.0</TargetFramework>
     <!-- NoWarn below will suppress SYSLIB0010 project-wide -->
     <NoWarn>$(NoWarn);SYSLIB0010</NoWarn>
    </PropertyGroup>
  </Project>
  ```

  Suprimir `SYSLIB0010` desabilita apenas os avisos do obsoletion da API de comunicação remota. Ele não desabilita nenhum outro aviso. Além disso, ele não altera o comportamento de tempo de execução codificado de sempre lançamento <xref:System.PlatformNotSupportedException> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=fullName>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `M:System.MarshalByRefObject.GetLifetimeService`
- `M:System.MarshalByRefObject.InitializeLifetimeService`

-->
