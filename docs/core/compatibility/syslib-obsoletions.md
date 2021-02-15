---
title: Recursos obsoletos no .NET 5 +
description: Saiba mais sobre as APIs que estão marcadas como obsoletas no .NET 5,0 e versões posteriores que produzem avisos do compilador SYSLIB.
ms.date: 10/20/2020
ms.openlocfilehash: 336958c93e3db8f66cfbec89476a666e5e103b70
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593299"
---
# <a name="obsolete-features-in-net-5"></a>Recursos obsoletos no .NET 5

A partir do .NET 5,0, algumas APIs que são marcadas recentemente como obsoletas fazem uso de duas novas propriedades no <xref:System.ObsoleteAttribute> .

- A <xref:System.ObsoleteAttribute.DiagnosticId?displayProperty=nameWithType> propriedade informa ao compilador para gerar avisos de compilação usando uma ID de diagnóstico Personalizada. A ID personalizada permite que o aviso obsoletion seja suprimido especificamente e separadamente um do outro. No caso do .NET 5 + obsoletions, o formato da ID de diagnóstico personalizado é `SYSLIBxxxx` .

- A <xref:System.ObsoleteAttribute.UrlFormat?displayProperty=nameWithType> propriedade informa ao compilador para incluir um link de URL para saber mais sobre o obsoletion.

Se você encontrar avisos de compilação ou erros devido ao uso de uma API obsoleta, siga as diretrizes específicas fornecidas para a ID de diagnóstico listada na seção de [referência](#reference) . Avisos ou erros para essas obsoletions *não podem* ser suprimidos usando a [CS0618 (ID de diagnóstico padrão)](../../csharp/language-reference/compiler-messages/cs0618.md) para tipos ou membros obsoletos; `SYSLIBxxxx` em vez disso, use os valores de ID de diagnóstico personalizados. Para obter mais informações, consulte [suprimir avisos](#suppress-warnings).

## <a name="reference"></a>Referência

A tabela a seguir fornece um índice para o `SYSLIBxxxx` obsoletions no .NET 5 +.

| ID do diagnóstico | Descrição |
| - | - |
| [SYSLIB0001](syslib-warnings/syslib0001.md) | A codificação UTF-7 é insegura e não deve ser usada. Considere usar UTF-8 em vez disso. |
| [SYSLIB0002](syslib-warnings/syslib0002.md) | <xref:System.Security.Permissions.PrincipalPermissionAttribute> Não é respeitado pelo tempo de execução e não deve ser usado. |
| [SYSLIB0003](syslib-warnings/syslib0003.md) | A CAS (segurança de acesso ao código) não tem suporte nem é respeitada pelo tempo de execução. |
| [SYSLIB0004](syslib-warnings/syslib0004.md) | Não há suporte para o recurso CER (região de execução restrita). |
| [SYSLIB0005](syslib-warnings/syslib0005.md) | Não há suporte para o GAC (cache de assembly global). |
| [SYSLIB0006](syslib-warnings/syslib0006.md) | <xref:System.Threading.Thread.Abort?displayProperty=nameWithType> Não é suportado e gera <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0007](syslib-warnings/syslib0007.md) | Não há suporte para a implementação padrão desse algoritmo de criptografia. |
| [SYSLIB0008](syslib-warnings/syslib0008.md) | A <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator> API não é suportada e gera <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0009](syslib-warnings/syslib0009.md) | Os <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType> <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> métodos e não têm suporte e geram <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0010](syslib-warnings/syslib0010.md) | Algumas APIs de comunicação remota não têm suporte e geram <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0011](syslib-warnings/syslib0011.md) | <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> a serialização está obsoleta e não deve ser usada. |
| [SYSLIB0012](syslib-warnings/syslib0012.md) | <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> e <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> são incluídos apenas para .NET Framework compatibilidade. Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> em vez disso. |

## <a name="suppress-warnings"></a>Suprimir avisos

Se você precisar usar as APIs obsoletas e o diagnóstico não for exibido `SYSLIBxxxx` como um erro, poderá suprimir o aviso no código ou no arquivo do projeto.

No código:

```csharp
// Disable the warning.
#pragma warning disable SYSLIB0001
// Code that uses obsolete API.
...
// Re-enable the warning.
#pragma warning restore SYSLIB0001
```

Arquivo de projeto:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
   <TargetFramework>net5.0</TargetFramework>
   <!-- NoWarn below suppresses SYSLIB0001 project-wide -->
   <NoWarn>$(NoWarn);SYSLIB0001</NoWarn>
   <!-- To suppress multiple warnings, you can use multiple NoWarn elements -->
   <NoWarn>$(NoWarn);SYSLIB0002</NoWarn>
   <NoWarn>$(NoWarn);SYSLIB0003</NoWarn>
   <!-- Alternatively, you can suppress multiple warnings by using a semicolon-delimited list -->
   <NoWarn>$(NoWarn);SYSLIB0001;SYSLIB0002;SYSLIB0003</NoWarn>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Suprimir avisos dessa forma apenas desabilita os avisos obsoletion que você especificar. Ele não desabilita nenhum outro aviso, incluindo avisos de obsoletion com diferentes IDs de diagnóstico.
