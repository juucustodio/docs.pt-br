---
title: 'Alteração significativa: as APIs do cache de assembly global estão obsoletas'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que as APIs que lidam com o GAC falham ou não executam nenhuma operação.
ms.date: 11/01/2020
ms.openlocfilehash: 2f74fccc68b7a925d909938d77578df8ebe8d60d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760416"
---
# <a name="global-assembly-cache-apis-are-obsolete"></a>As APIs do cache de assembly global estão obsoletas

O .NET Core e o .NET 5,0 e versões posteriores eliminam o conceito do GAC (cache de assembly global) que estava presente no .NET Framework. Assim, todas as APIs .NET Core e .NET 5 + que lidam com o GAC falham ou não executam nenhuma operação.

Para ajudar os desenvolvedores a se afastar dessas APIs, algumas APIs relacionadas ao GAC são marcadas como obsoletas e geram um `SYSLIB0005` aviso no momento da compilação. Essas APIs podem ser removidas em uma versão futura do .NET.

## <a name="change-description"></a>Descrição das alterações

As seguintes APIs estão marcadas como obsoletas.

| API | Marcado como obsoleto em... |
| - | - |
| <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=nameWithType> | RC1 5,0 |

No .NET Framework 2. x-4. x, a <xref:System.Reflection.Assembly.GlobalAssemblyCache> propriedade retorna `true` se o assembly consultado foi carregado do GAC e `false` se foi carregado a partir de um local diferente no disco. No .NET Core 2. x-3. x, o <xref:System.Reflection.Assembly.GlobalAssemblyCache> sempre retorna `false` , refletindo que o GAC não existe no .NET Core.

```csharp
Assembly asm = typeof(object).Assembly;
// Prints 'True' on .NET Framework, 'False' on .NET Core.
Console.WriteLine(asm.GlobalAssemblyCache);
```

No .NET 5,0 e versões posteriores, a <xref:System.Reflection.Assembly.GlobalAssemblyCache> Propriedade continua sempre retornando `false` . No entanto, o getter da propriedade também é marcado como obsoleto para indicar aos chamadores que eles devem parar de acessar a propriedade. Bibliotecas e aplicativos não devem usar a <xref:System.Reflection.Assembly.GlobalAssemblyCache> API para fazer determinações sobre o comportamento de tempo de execução, como sempre retorna `false` no .NET Core e no .NET 5,0 e versões posteriores.

```csharp
Assembly asm = typeof(object).Assembly;
// Prints 'False' on .NET 5.0+; also produces warning SYSLIB0005 at compile time.
Console.WriteLine(asm.GlobalAssemblyCache);
```

Essa é uma alteração somente em tempo de compilação. Não há nenhuma alteração de tempo de execução de versões anteriores do .NET Core.

## <a name="reason-for-change"></a>Motivo da alteração

O GAC (cache de assembly global) não existe como um conceito no .NET Core e no .NET 5,0 e versões posteriores.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

- Se seu aplicativo consulta a <xref:System.Reflection.Assembly.GlobalAssemblyCache> propriedade, considere remover a chamada. Se você usar o <xref:System.Reflection.Assembly.GlobalAssemblyCache> valor para escolher entre um "assembly no GAC"-Flow versus um "assembly que não está no GAC"-Flow em tempo de execução, reconsidere se o fluxo ainda faz sentido para um aplicativo .NET Core ou .NET 5.0 +.

- Se você precisar continuar a usar as APIs obsoletas, poderá suprimir o `SYSLIB0005` aviso no código.

  ```csharp
  Assembly asm = typeof(object).Assembly;
  #pragma warning disable SYSLIB0005 // Disable the warning.
  // Prints 'False' on .NET 5.0+.
  Console.WriteLine(asm.GlobalAssemblyCache);
  #pragma warning restore SYSLIB0005 // Re-enable the warning.
  ```

  Você também pode suprimir o aviso em seu arquivo de projeto, o que desabilita o aviso para todos os arquivos de origem no projeto.

  ```xml
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
     <TargetFramework>net5.0</TargetFramework>
     <!-- NoWarn below will suppress SYSLIB0005 project-wide -->
     <NoWarn>$(NoWarn);SYSLIB0005</NoWarn>
    </PropertyGroup>
  </Project>
  ```

  Suprimir `SYSLIB0005` desabilita apenas o <xref:System.Reflection.Assembly.GlobalAssemblyCache> aviso obsoletion. Ele não desabilita nenhum outro aviso.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Reflection.Assembly.GlobalAssemblyCache`

-->
