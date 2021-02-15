---
title: 'Alteração significativa: o suporte interno para o WinRT é removido do .NET'
description: Saiba mais sobre a alteração significativa de interoperabilidade no .NET 5,0, em que o suporte interno para o WinRT é removido do .NET.
ms.date: 10/13/2020
ms.openlocfilehash: 61d8e26d06c232a7bfa1891a2159f5232f747b8a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760414"
---
# <a name="built-in-support-for-winrt-is-removed-from-net"></a>O suporte interno para o WinRT é removido do .NET

O suporte interno para consumo de APIs do [tempo de execução do Windows (WinRT)](/uwp/winrt-cref/winrt-type-system) no .net foi removido.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Anteriormente, o CoreCLR poderia consumir [arquivos de metadados do Windows (WinMD)](/uwp/winrt-cref/winmd-files) para ativar e consumir tipos de WinRT. A partir do .NET 5,0, o CoreCLR não pode mais consumir arquivos WinMD diretamente.

Se você tentar fazer referência a um assembly sem suporte, obterá um <xref:System.IO.FileNotFoundException> . Se você ativar uma classe do WinRT, obterá um <xref:System.PlatformNotSupportedException> .

Essa alteração significativa foi feita pelos seguintes motivos:

- Portanto, o WinRT pode ser desenvolvido e aprimorado separadamente do tempo de execução do .NET.
- Para simetria com sistemas de interoperabilidade fornecidos para outros sistemas operacionais, como iOS e Android.
- Para tirar proveito de outros recursos do .NET, como recursos C#, vinculação de IL (linguagem intermediária) e compilação de AOT (antecipadamente de tempo).
- Para simplificar a base de código .NET Runtime.

## <a name="recommended-action"></a>Ação recomendada

- Remova as referências ao [pacote Microsoft. Windows. Sdk. Contracts](https://www.nuget.org/packages/Microsoft.Windows.SDK.Contracts).  Em vez disso, especifique a versão das APIs do Windows que você deseja acessar por meio da `TargetFramework` Propriedade do projeto.  Por exemplo:

  ```xml
  <TargetFramework>net5.0-windows10.0.19041</TargetFramework>
  ```

- Use a cadeia de ferramentas [/WinRT do C#](/windows/uwp/csharp-winrt/) para gerar ou personalizar APIs e tipos do WinRT para .NET 5,0 e versões posteriores.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.IO.WindowsRuntimeStorageExtensions?displayProperty=fullName>
- <xref:System.IO.WindowsRuntimeStreamExtensions?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.WindowsRuntime?displayProperty=fullName>
- <xref:System.WindowsRuntimeSystemExtensions?displayProperty=fullName>
- <xref:Windows.Foundation.Point?displayProperty=fullName>
- <xref:Windows.Foundation.Size?displayProperty=fullName>
- <xref:Windows.UI.Color?displayProperty=fullName>

<!--

### Affected APIs

- `T:System.IO.WindowsRuntimeStorageExtensions`
- `T: System.IO.WindowsRuntimeStreamExtensions`
- `N:System.Runtime.InteropServices.WindowsRuntime`
- `T:System.WindowsRuntimeSystemExtensions`
- `T:Windows.Foundation.Point`
- `T:Windows.Foundation.Size`
- `T:Windows.UI.Color`

### Category

Interop

-->
