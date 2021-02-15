---
description: 'Saiba mais sobre: s_isDebuggerCheckDisabledForTestPurposes campo'
title: Campo de s_isDebuggerCheckDisabledForTestPurposes
ms.date: 03/30/2017
ms.technology: dotnet-wpf
topic_type:
- apiref
api_name:
- System.Windows.Diagnostics.VisualDiagnostics.s_isDebuggerCheckDisabledForTestPurposes
api_location:
- PresentationCore.dll
api_type:
- Assembly
ms.assetid: 9033a513-c255-4f31-b6d7-09b8d8c50e2d
ms.openlocfilehash: a71235c13a7a35872bcf5374be8077bafad5ff9a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802652"
---
# <a name="s_isdebuggercheckdisabledfortestpurposes-field"></a>Campo de s_isDebuggerCheckDisabledForTestPurposes

Esse campo privado na `System.Windows.Diagnostics.VisualDiagnostics` classe é usado pelo Visual Studio para determinar se uma verificação interna de um depurador ativo será executada.

## <a name="syntax"></a>Syntax

```csharp
private static bool s_isDebuggerCheckDisabledForTestPurposes
```

> [!WARNING]
> As APIs na `System.Windows.Diagnostics.VisualDiagnostics` classe só estão disponíveis quando um aplicativo é executado em um depurador. Defina `s_isDebuggerCheckDisabledForTestPurposes` como `true` para acessar as APIs fora de um depurador.
>
> A Microsoft não oferece suporte ao uso deste campo em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Windows.Diagnostics>

**Assembly:** PresentationCore (em PresentationCore.dll)

**.NET Framework versões:** Disponível desde 4,6.
