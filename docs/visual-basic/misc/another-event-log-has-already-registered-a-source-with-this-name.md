---
description: 'Saiba mais sobre: outro log de eventos já registrou uma origem com este nome'
title: Outro log de eventos já registrou uma fonte com esse nome
ms.date: 07/20/2015
ms.assetid: e6f5cd95-bb3f-4845-84fb-ae623a9bd44e
ms.openlocfilehash: ec6ae0b3ef12452a0135e5bf17dbdd5844c0f478
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787351"
---
# <a name="another-event-log-has-already-registered-a-source-with-this-name"></a>Outro log de eventos já registrou uma fonte com esse nome

Foi feita uma tentativa de gravar uma entrada em um log de eventos em que a origem especificada está registrada com outro log de eventos.  
  
 Você deve definir a <xref:System.Diagnostics.EventLog.Source%2A> propriedade da <xref:System.Diagnostics.EventLog> instância do componente antes que o componente grave uma entrada em um log. Quando isso acontece, o sistema verifica se a fonte que você especificou está registrada com o log de eventos no qual o componente está gravando e chama, <xref:System.Diagnostics.EventLog.CreateEventSource%2A> se necessário.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Remova a associação da origem com o primeiro log usando o <xref:System.Diagnostics.EventLog.DeleteEventSource%2A> <xref:System.Diagnostics.EventLog.DeleteEventSource%2A> método ou.  
  
2. Registre a origem com o novo log.  
  
## <a name="see-also"></a>Consulte também

- [Meu. Application. log](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
