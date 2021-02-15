---
title: 'Alteração significativa: OutputType definido como WinExe para aplicativos WPF e WinForms'
description: Saiba mais sobre a alteração significativa no SDK do .NET 5.0.100 em que OutputType é definido automaticamente como WinExe para aplicativos Windows Forms.
ms.date: 09/18/2020
ms.openlocfilehash: 38d9b910374f9e44f7e35296808930c6a6d45f0d
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100431458"
---
# <a name="outputtype-set-to-winexe-for-wpf-and-winforms-apps"></a>OutputType definido como WinExe para aplicativos WPF e WinForms

`OutputType` é definido automaticamente como `WinExe` para Windows Presentation Foundation (WPF) e Windows Forms aplicativos. Quando `OutputType` é definido como `WinExe` , uma janela do console não é aberta quando o aplicativo é executado.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do SDK do .NET, o valor especificado para `OutputType` no arquivo de projeto é usado. Por exemplo:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

A partir da versão 5.0.100 do SDK do .NET, quando `OutputType` é definido como `Exe` , ele é automaticamente alterado para `WinExe` para o WPF e Windows Forms aplicativos direcionados a qualquer versão de estrutura, incluindo .NET Framework.

```xml
<PropertyGroup>
  <OutputType>WinExe</OutputType>
</PropertyGroup>
```

 Se `OutputType` não for especificado no arquivo do projeto, o padrão será `Library` e esse valor não será alterado.

## <a name="reason-for-change"></a>Motivo da alteração

Supõe-se que a maioria dos usuários não queira que uma janela do console seja aberta quando um aplicativo do WPF ou Windows Forms é executado. Além disso, [agora que esses tipos de aplicativos usam o SDK do .net](sdk-and-target-framework-change.md) em vez do SDK de área de trabalho do Windows, o padrão correto será definido. Além disso, quando o suporte para o destino do iOS e do Android for adicionado, será mais fácil realizar vários destinos entre várias plataformas se todos usarem o mesmo tipo de saída.

## <a name="version-introduced"></a>Versão introduzida

5.0.100 .NET

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária em sua parte. No entanto, se você quiser reverter para o comportamento antigo, defina a `DisableWinExeOutputInference` propriedade como `true` em seu arquivo de projeto.

```xml
<DisableWinExeOutputInference>true</DisableWinExeOutputInference>
```

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

- Windows Forms
- Windows Presentation Framework (WPF)

-->
