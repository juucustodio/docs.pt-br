---
description: 'Saiba mais sobre: migrar aplicativos de comunicação remota do .NET para o WCF'
title: Migrando aplicativos remotos .NET para o WCF
ms.date: 03/30/2017
helpviewer_keywords:
- ',NET remoting [WCF]'
ms.assetid: 24793465-65ae-4308-8c12-dce4fd12a583
ms.openlocfilehash: 551ad759c11ab24d6ab83a466e8e94b8226bf4d4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733756"
---
# <a name="migrating-net-remoting-applications-to-wcf"></a>Migrando aplicativos remotos .NET para o WCF

**Este tópico é específico para uma tecnologia herdada que é mantida para compatibilidade com versões anteriores com aplicativos existentes e não é recomendada para desenvolvimento novo. Agora, os aplicativos distribuídos devem ser desenvolvidos usando o WCF.**  
  
 Há duas maneiras de aproveitar o WCF com os aplicativos existentes de comunicação remota do .NET: integração e migração. A integração permite que você tenha o .NET Remoting 2,0 e o WCF em execução lado a lado, permitindo que você exponha os mesmos objetos de negócios em ambas as tecnologias simultaneamente, sem a necessidade de modificar seu código .NET Remoting 2,0 existente. A integração requer que você esteja executando o .NET Framework 2,0 ou superior. Se você quiser aproveitar os recursos do WCF e não precisar de compatibilidade de conexão com os sistemas de comunicação remota 2,0, poderá migrar todo o serviço para o WCF. A migração do .NET Remoting 2,0 para o WCF requer alterações na interface do objeto remoto e em suas definições de configuração. Esses dois tópicos são abordados na [comunicação remota com o Windows Communication Foundation](/previous-versions/aa730857(v=vs.80)).  
  
## <a name="see-also"></a>Consulte também

- [Visão geral conceitual](../conceptual-overview.md)
