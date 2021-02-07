---
description: 'Saiba mais sobre: registros de controle personalizados'
title: Registros de rastreamento personalizadas
ms.date: 03/30/2017
ms.assetid: 24284565-c68b-40bf-b7f1-e148d151a6fc
ms.openlocfilehash: 9d6988465fa3afca4302c86e0c2cad2778f2beae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742687"
---
# <a name="custom-tracking-records"></a>Registros de rastreamento personalizadas

Este tópico demonstra como criar registros personalizados de rastreamento e populá-los com os dados a serem emitidos juntamente com os registros.

## <a name="emitting-custom-tracking-records"></a>Emitindo registros de rastreamento personalizadas

Os registros personalizados de rastreamento podem ser emitidos de uma atividade do código conforme mostrado no exemplo o seguir.

```csharp
protected override void Execute(CodeActivityContext context)
{
…
            CustomTrackingRecord customRecord = new CustomTrackingRecord("CustomEmailSentEvent");
            customRecord.Data.Add("SendTime", sendTime);
            context.Track(customRecord);
}
```

<xref:System.Activities.Tracking.CustomTrackingRecord> é emitido em uma atividade de código chamando o método de <xref:System.Activities.NativeActivityContext.Track%2A> em `ActivityContext`.

## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
