---
title: 'Alteração significativa: a conversão de RCW para `InterfaceIsIInspectable` gera exceção'
description: Saiba mais sobre a alteração significativa de interoperabilidade no .NET 5,0 em que a conversão de um RCW em uma `InterfaceIsIInspectable` interface gera um PlatformNotSupportedException.
ms.date: 09/13/2020
ms.openlocfilehash: 7c0f37057aebcc41d0c00d949b921ec3a4bdf012
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760412"
---
# <a name="casting-rcw-to-an-interfaceisiinspectable-interface-throws-platformnotsupportedexception"></a>A conversão de RCW em uma `InterfaceIsIInspectable` interface gera PlatformNotSupportedException

A conversão de um RCW (Runtime Callable Wrapper) em uma interface marcada como <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> agora gera um <xref:System.PlatformNotSupportedException> . Essa alteração é um acompanhamento da [remoção do suporte do WinRT do .net](built-in-support-for-winrt-removed.md).

## <a name="version-introduced"></a>Versão introduzida

5,0 RC2

## <a name="change-description"></a>Descrição das alterações

Em versões do .NET anteriores ao .NET 5,0 Preview 6, a conversão de um RCW em uma interface marcada como <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> funciona conforme o esperado. Nas visualizações do .NET 5,0 6-8 e RC1, você pode converter com êxito um RCW em uma <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> interface. No entanto, você pode obter violações de acesso ao executar métodos na interface, porque o suporte subjacente no tempo de execução [foi removido no .net 5,0 Preview 6](built-in-support-for-winrt-removed.md).

No .NET 5,0 RC2 e versões posteriores, converter um RCW em uma interface marcada como <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> lança um <xref:System.PlatformNotSupportedException> no momento da conversão.

## <a name="reason-for-change"></a>Motivo da alteração

O suporte para <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> foi [removido em uma versão prévia anterior do .NET 5,0](built-in-support-for-winrt-removed.md). No entanto, a conversão para uma <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> interface foi acidentalmente ignorada. Como o suporte subjacente no tempo de execução não existe mais, lançar um <xref:System.PlatformNotSupportedException> habilita um caminho de falha normal. Gerar uma exceção também o torna mais detectável que esse recurso não é mais suportado.

## <a name="recommended-action"></a>Ação recomendada

- Se você puder definir a interface em um arquivo de metadados do tempo de execução do Windows (WinMD), use a ferramenta/WinRT do C# em vez disso.

- Caso contrário, marque a interface como <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIUnknown> em vez de <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> e adicione três entradas fictícias ao início da interface para os <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> métodos. O trecho de código a seguir mostra um exemplo.

  ```csharp
  [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
  interface IMine
  {
      // Do not call these three methods.
      // They're exclusively to fill in the slots in the vtable.
      void GetIIdsSlot();
      void GetRuntimeClassNameSlot();
      void GetTrustLevelSlot();

      // The original members of the IMine interface go here.
      ...
  }
  ```

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable?displayProperty=fullName>

<!--

### Affected APIs

- `F:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable`

### Category

Interop

-->
