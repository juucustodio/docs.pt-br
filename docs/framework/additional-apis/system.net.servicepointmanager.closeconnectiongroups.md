---
description: 'Saiba mais sobre: método ServicePointManager. CloseConnectionGroups'
title: Método ServicePointManager. CloseConnectionGroups (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.ServicePointManager.CloseConnectionGroups
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 8cd1a1f0f4dbdaeaee117e6a7ae4219680363a6e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699552"
---
# <a name="servicepointmanagercloseconnectiongroups-method"></a>Método ServicePointManager. CloseConnectionGroups

Itera em todos os pontos de serviço e fecha os grupos de conexão que têm o nome especificado.

```csharp
internal static void CloseConnectionGroups(string connectionGroupName)
```

> [!WARNING]
> Esse método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="parameters"></a>Parâmetros

`connectionGroupName` <xref:System.String>

O nome do grupo de conexões a ser fechado.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
