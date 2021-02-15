---
description: 'Saiba mais sobre: o nome de origem especificado em EventLogname está registrado em um log diferente daquele especificado em EventLogname'
title: O nome da fonte especificado em EventLogSource está registrado em um log diferente daquele especificado em EventLogName
ms.date: 07/20/2015
ms.assetid: 7317e100-098b-408d-86e5-7c74cf8558c7
ms.openlocfilehash: d6b9c1265276f94369d37e6ac55604b761fb9bcc
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100455451"
---
# <a name="source-name-specified-in-eventlogsource-is-registered-to-a-log-other-than-that-specified-in-eventlogname"></a>O nome da fonte especificado em EventLogSource está registrado em um log diferente daquele especificado em EventLogName

O `EventLog` está tentando se referir a uma fonte que está registrada em um log diferente. Se você estiver gravando entradas em um log de eventos, deverá especificar a <xref:System.Diagnostics.EventLog.Source%2A> propriedade. A <xref:System.Diagnostics.EventLog.Source%2A> Propriedade registra seu componente com o log de eventos como uma fonte de entradas válida. Uma única fonte pode ser associada (e, portanto, gravar entradas em) apenas um log de eventos por vez.  
  
 Por padrão, se você tentar gravar uma entrada sem primeiro registrar seu componente como uma fonte válida, o sistema registrará automaticamente a origem com o log de eventos, usando o valor da <xref:System.Diagnostics.EventLog.Source%2A> propriedade como a cadeia de caracteres de origem.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a origem está registrada no log correto. Para fazer isso, use o <xref:System.Diagnostics.EventLog.CreateEventSource%2A> método ou uma de suas sobrecargas para especificar uma cadeia de caracteres que identifica exclusivamente o componente para o log de eventos.  
  
## <a name="see-also"></a>Consulte também

- [Administrando logs de eventos](/previous-versions/visualstudio/visual-studio-2008/4f69axw4(v=vs.90))
- [Referências do log de eventos](/previous-versions/visualstudio/visual-studio-2008/k43k9z2a(v=vs.90))
- [Como: adicionar seu aplicativo como uma fonte de entradas de log de eventos](/previous-versions/visualstudio/visual-studio-2008/xz73e171(v=vs.90))
- [Como: remover uma origem do evento](/previous-versions/visualstudio/visual-studio-2008/k57466fc(v=vs.90))
