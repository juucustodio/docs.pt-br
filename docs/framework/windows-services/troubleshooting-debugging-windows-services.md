---
title: 'Solucionando problemas: depurando Serviços Windows'
description: Introdução à depuração de serviços do Windows. Quando você depurar um aplicativo de serviço Windows, o serviço e o Windows Service Manager interagirão.
ms.date: 03/30/2017
helpviewer_keywords:
- debugging Windows Service applications
- debugging [Visual Studio], Windows services
- troubleshooting service applications
- services, troubleshooting
- troubleshooting debugging, Windows Services
- Windows Service applications, debugging
- services, debugging
- Windows Service applications, troubleshooting
ms.assetid: cf859d4c-f04c-4cb7-81e3-bc7de8bea190
ms.openlocfilehash: 2c1180ef8e3e44c50f10a263d86dcae830d9cd0e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270387"
---
# <a name="troubleshooting-debugging-windows-services"></a>Solucionando problemas: depurando Serviços Windows

Quando você depurar um aplicativo de serviço Windows, o serviço e o **Windows Service Manager** interagirão. O **Service Manager** inicia o serviço chamando o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e, em seguida, espera 30 segundos para que o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> retorne. Se o método não retornar nesse período, o gerenciador mostra um erro indicando que o serviço não pode ser iniciado.  
  
 Ao depurar o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A>, conforme é descrito em [Como depurar aplicativos de Serviço Windows](how-to-debug-windows-service-applications.md), você precisará estar ciente desse período de 30 segundos. Se você colocar um ponto de interrupção no método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e não entrar nele em até 30 segundos, o gerente não iniciará o serviço.  
  
## <a name="see-also"></a>Veja também

- [Como: Depurar aplicativos do serviço Windows](how-to-debug-windows-service-applications.md)
- [Introdução a aplicativos do Serviço Windows](introduction-to-windows-service-applications.md)
