---
description: 'Saiba mais sobre: log de eventos no WCF'
title: Registro de eventos em log no WCF
ms.date: 03/30/2017
helpviewer_keywords:
- event logging [WCF]
ms.assetid: aac0530d-f44c-45a1-bada-e30e0677b41f
ms.openlocfilehash: 741e6efce9f5fffec607d511f04a400e1292b682
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99744208"
---
# <a name="event-logging-in-wcf"></a>Registro de eventos em log no WCF

Windows Communication Foundation (WCF) rastreia eventos internos no log de eventos do Windows.  
  
## <a name="viewing-event-logs"></a>Exibindo logs de eventos  

 O log de eventos é habilitado automaticamente por padrão e não há nenhum mecanismo para desabilitá-lo. Os eventos registrados pelo WCF podem ser exibidos usando o Visualizador de Eventos. Para iniciar essa ferramenta, clique em **Iniciar**, **painel de controle**, clique duas vezes em **Ferramentas administrativas** e, em seguida, clique duas vezes em **Visualizador de eventos**.  
  
### <a name="application-event-log"></a>Log de Eventos do Aplicativo  

 O **log de eventos do aplicativo** contém a maioria dos eventos gerados pelo WCF. A maioria das entradas indica que um recurso específico falhou ao ser inicializado para um aplicativo. Os exemplos incluem:  
  
- Rastreamento/log de mensagens: o WCF grava um evento no log de eventos quando o log de mensagens e o rastreamento falham. No entanto, nem toda falha de rastreamento dispara um evento. Para impedir que o log de eventos seja completamente preenchido com falhas de rastreamentos, o WCF implementa um período de blecaute de 10 minutos para tal evento. Isso significa que, se o WCF gravar uma falha de rastreamento no log de eventos, ele não fará isso novamente por pelo menos 10 minutos.  
  
- Ouvinte compartilhado: o serviço de compartilhamento de porta TCP do WCF registra um evento quando ele não é iniciado.  
  
- CardSpace: registra eventos quando o serviço não é iniciado.  
  
- Eventos críticos e de erro, como falhas de inicialização ou falhas  
  
- Log de mensagens ativado: registra eventos quando o log de mensagens está ativado. Isso é notificar o administrador de que as informações confidenciais específicas do aplicativo podem ser registradas em cabeçalhos e corpos de mensagens.  
  
- Um evento é registrado quando o `enableLoggingKnownPII` atributo no `machineSettings` elemento do `machine.config` arquivo é definido. Esse atributo especifica se qualquer aplicativo em execução no computador tem permissão para registrar informações de identificação pessoal conhecidas (PII).  
  
- Se o `logKnownPii` atributo no `app.config` `web.config` arquivo ou estiver definido como `true` para um aplicativo específico ativar o log de PII, mas o `enableLoggingKnownPII` atributo no `machineSettings` elemento do `machine.config` arquivo for definido como `false` , um evento será registrado. Além disso, se ambos `logKnownPii` e `enableLoggingKnownPII` estiverem definidos como `true` , e o evento for registrado. Para obter mais informações sobre essas definições de configuração, consulte a seção segurança do tópico [Configurando o log de mensagens](../configuring-message-logging.md) .  
  
### <a name="security-event-log"></a>Log de eventos de segurança  

 O **log de eventos de segurança** contém eventos de auditoria de segurança que são registrados pelo WCF.  
  
### <a name="system-event-log"></a>Log de Eventos do Sistema  

 O WCF não registra em log nada no **log de eventos do sistema**.  
  
### <a name="event-log-entries"></a>Entradas do log de eventos  

 A **origem** de um evento é o nome do assembly que gera a entrada de log.  
  
 O tipo de uma entrada de log de eventos é usado para indicar a severidade de um evento. Cada evento deve ser de um único tipo, que o aplicativo indica quando relata o evento. O Visualizador de Eventos usa esse tipo para determinar qual ícone deve ser exibido na exibição de lista do log. Para o tipo de evento diferente de uma entrada de log de eventos, consulte <xref:System.Diagnostics.EventLogEntryType> .  
  
 Quando você clica em "mais informações" ao exibir um evento na Visualizador de Eventos, o Visualizador de Eventos pode enviar informações pela Internet. Para obter mais informações, consulte a ajuda do Visualizador de Eventos.  
  
## <a name="see-also"></a>Consulte também

- [Administração e diagnósticos](../index.md)
- [Referência geral de eventos](events-general-reference.md)
