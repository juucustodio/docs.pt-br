---
title: 'Alteração significativa: os métodos de serialização BinaryFormatter são obsoletos e proibidos em aplicativos ASP.NET'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que os métodos serializar e desserializar em BinaryFormatter, Formatter e IFormatter são obsoletos.
ms.date: 11/01/2020
ms.openlocfilehash: 1dca30d33f2aa0a6fe8f05fe728557092f836b2d
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189838"
---
# <a name="binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps"></a>Os métodos de serialização BinaryFormatter são obsoletos e proibidos em aplicativos ASP.NET

`Serialize` e `Deserialize` os métodos em <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> , <xref:System.Runtime.Serialization.Formatter> e <xref:System.Runtime.Serialization.IFormatter> agora são obsoletos como aviso. Além disso, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> a serialização é proibida por padrão para aplicativos ASP.net.

## <a name="change-description"></a>Descrição das alterações

Devido a [vulnerabilidades de segurança](../../../../standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities) no <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> , os métodos a seguir agora são obsoletos e produzem um aviso de tempo de compilação com a ID `SYSLIB0011` . Além disso, no ASP.NET Core 5,0 e em aplicativos posteriores, eles lançarão um <xref:System.NotSupportedException> , a menos que o aplicativo Web tenha reativado a <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> funcionalidade.

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>

Os seguintes métodos de serialização também são obsoletos e produzem aviso `SYSLIB0011` , mas não têm nenhuma alteração comportamental:

- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

Esses métodos são marcados como obsoletos como parte de um esforço para o uso do vento <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> no ecossistema do .net.

## <a name="recommended-action"></a>Ação recomendada

- Pare <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> de usar no seu código. Em vez disso, considere usar <xref:System.Text.Json.JsonSerializer> ou <xref:System.Xml.Serialization.XmlSerializer> . Para obter mais informações, consulte [Guia de segurança do BinaryFormatter](../../../../standard/serialization/binaryformatter-security-guide.md).

- Você pode suprimir temporariamente o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> aviso de tempo de compilação, que é `SYSLIB0011` . Recomendamos que você avalie minuciosamente seu código em busca de riscos antes de escolher essa opção. A maneira mais fácil de suprimir os avisos é envolver o site de chamada individual com `#pragma` diretivas.

  ```csharp
  // Now read the purchase order back from disk
  using (var readStream = new FileStream("myfile.bin", FileMode.Open))
  {
      var formatter = new BinaryFormatter();
  #pragma warning disable SYSLIB0011
      return (PurchaseOrder)formatter.Deserialize(readStream);
  #pragma warning restore SYSLIB0011
  }
  ```

  Você também pode suprimir o aviso no arquivo de projeto.

  ```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <!-- Disable "BinaryFormatter is obsolete" warnings for entire project -->
    <NoWarn>$(NoWarn);SYSLIB0011</NoWarn>
  </PropertyGroup>
  ```

  Se você suprimir o aviso no arquivo de projeto, o aviso será suprimido para todos os arquivos de código no projeto. A supressão `SYSLIB0011` não elimina os avisos causados pelo uso de outras APIs obsoletas.

- Para continuar usando <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> o em aplicativos ASP.net, você pode reabilitá-lo no arquivo de projeto. No entanto, é altamente recomendável não fazer isso. Para obter mais informações, consulte [Guia de segurança do BinaryFormatter](../../../../standard/serialization/binaryformatter-security-guide.md).

  ```xml
  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    <!-- Warning: Setting the following switch is *NOT* recommended in web apps. -->
    <EnableUnsafeBinaryFormatterSerialization>true</EnableUnsafeBinaryFormatterSerialization>
  </PropertyGroup>
  ```

Para obter mais informações sobre as ações recomendadas, consulte [Resolvendo erros de BinaryFormatter obsoletion e de desativação](../../../../standard/serialization/binaryformatter-security-guide.md).

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=fullName>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=fullName>

<!--

#### Category

- Core .NET libraries
- ASP.NET Core

### Affected APIs

- `Overload:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize`
- `Overload:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize`
- `M:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)`
- `M:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)`
- `M:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)`
- `M:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)`

-->
