---
description: 'Saiba mais sobre: registrar em log informações do aplicativo (Visual Basic)'
title: Registrando informações em log a partir do aplicativo
ms.date: 07/20/2015
helpviewer_keywords:
- Log object
- My.Log object
- applications [Visual Basic], logging information from
- logging
- My.Application.Log object
- examples [Visual Basic], logging application information
ms.assetid: 8bf4f047-22d6-48d6-aec5-93b98ad5b8e8
ms.openlocfilehash: 6e0adf45c12d98c8bc6d177d85accf9bee347f75
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99775065"
---
# <a name="logging-information-from-the-application-visual-basic"></a>Registrando informações em log a partir do aplicativo (Visual Basic)

Esta seção contém tópicos que abordam como registrar informações em log do aplicativo usando os objetos `My.Application.Log` ou `My.Log` e como estender os recursos de registro em log do aplicativo.  
  
 O objeto `Log` fornece métodos para gravar informações nos ouvintes de log do aplicativo e a propriedade avançada `TraceSource` do objeto `Log` fornece informações detalhadas de configuração. O objeto `Log` será configurado pelo arquivo de configuração de aplicativo.  
  
 O objeto `My.Log` está disponível somente para aplicativos do ASP.NET. Para aplicativos cliente, use `My.Application.Log`. Para obter mais informações, consulte <xref:Microsoft.VisualBasic.Logging.Log>.  
  
## <a name="tasks"></a>Tarefas  
  
|Para|Consulte|  
|--------|---------|  
|Gravar informações de evento em logs do aplicativo.|[Como: gravar mensagens de log](how-to-write-log-messages.md)|  
|Gravar informações de exceção em logs do aplicativo.|[Como: registrar exceções em log](how-to-log-exceptions.md)|  
|Gravar informações de rastreamento em logs do aplicativo quando o aplicativo for inicializado e desligado.|[Como: registrar mensagens em log quando o aplicativo é iniciado ou encerrado](how-to-log-messages-when-the-application-starts-or-shuts-down.md)|  
|Configure `My.Application.Log` para gravar informações em um arquivo de texto.|[Como: gravar informações de evento em um arquivo de texto](how-to-write-event-information-to-a-text-file.md)|  
|Configure `My.Application.Log` para gravar informações em um log de eventos.|[Como: gravar em um Log de Eventos do Aplicativo](how-to-write-to-an-application-event-log.md)|  
|Altere o local em que `My.Application.Log` grava as informações.|[Passo a passo: alterar o local no qual My.Application.Log grava informações](walkthrough-changing-where-my-application-log-writes-information.md)|  
|Determine o local em que `My.Application.Log` grava as informações.|[Passo a passo: determinar o local no qual My.Application.Log grava informações](walkthrough-determining-where-my-application-log-writes-information.md)|  
|Crie um ouvinte de log personalizado para `My.Application.Log`.|[Passo a passo: criar ouvintes de log personalizados](walkthrough-creating-custom-log-listeners.md)|  
|Filtre a saída dos logs `My.Application.Log`.|[Passo a passo: filtrar a saída de My.Application.Log](walkthrough-filtering-my-application-log-output.md)|  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [Trabalhar com logs do aplicativo](working-with-application-logs.md)
- [Solução de problemas: ouvintes de log](troubleshooting-log-listeners.md)
