---
description: 'Saiba mais sobre: administração e diagnóstico'
title: Administração e diagnósticos
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, diagnostics
- Windows Communication Foundation, administration
- diagnostics [WCF]
- WCF, diagnostics
- administration [WCF]
- WCF, administration
ms.assetid: 34c81c08-0e0f-4fbc-9ae8-91948640ee43
ms.openlocfilehash: aa2efe31431f80dda6c98b0ac13162e32390b12c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99771256"
---
# <a name="administration-and-diagnostics"></a>Administração e diagnósticos

O Windows Communication Foundation (WCF) fornece um conjunto avançado de funcionalidades que podem ajudá-lo a monitorar os diferentes estágios da vida útil de um aplicativo. Por exemplo, você pode usar a configuração para configurar serviços e clientes na implantação. O WCF inclui um grande conjunto de contadores de desempenho para ajudá-lo a medir o desempenho do seu aplicativo. O WCF também expõe dados de inspeção de um serviço em tempo de execução por meio de um provedor de Instrumentação de Gerenciamento do Windows WCF (WMI). Quando o aplicativo passa por uma falha ou começa a agir de forma inadequada, você pode usar o log de eventos para ver se algo significativo ocorreu. Você também pode usar o rastreamento e o log de mensagens para ver quais eventos estão ocorrendo de ponta a ponta em seu aplicativo. Esses recursos ajudam os desenvolvedores e profissionais de ti a solucionarem problemas de um aplicativo WCF quando ele não estiver se comportando corretamente.  
  
> [!NOTE]
> Se você estiver recebendo falhas sem informações detalhadas específicas, habilite o `includeExceptionDetailInFaults` atributo do [\<serviceDebug>](../../configure-apps/file-schema/wcf/servicedebug.md) elemento de configuração. Isso instrui o WCF a enviar detalhes de exceção aos clientes, o que permite detectar muitos problemas comuns sem a necessidade de diagnóstico mais avançado. Para obter mais informações, consulte [enviando e recebendo falhas](../sending-and-receiving-faults.md).  
  
## <a name="diagnostics-features-provided-by-wcf"></a>Recursos de diagnóstico fornecidos pelo WCF  

 O WCF fornece as seguintes funcionalidades de diagnóstico:  
  
- O rastreamento de ponta a ponta fornece dados de instrumentação para solução de problemas de um aplicativo sem usar um depurador. O WCF gera rastreamentos para etapas do processo, bem como mensagens de erro. Isso pode incluir a abertura de uma fábrica de canais ou o envio e recebimento de mensagens por um host de serviço. O rastreamento pode ser habilitado para que um aplicativo em execução monitore seu progresso. Para obter mais informações, consulte o tópico de [rastreamento](./tracing/index.md) . Para entender como você pode usar o rastreamento para depurar seu aplicativo, consulte o tópico [usando o rastreamento para solucionar problemas do seu aplicativo](./tracing/using-tracing-to-troubleshoot-your-application.md) .  
  
- O log de mensagens permite que você veja como as mensagens parecem antes e depois da transmissão. Para obter mais informações, consulte o tópico [log de mensagens](message-logging.md) .  
  
- O rastreamento de eventos grava eventos no log de eventos em busca de quaisquer problemas importantes. Em seguida, você pode usar o Visualizador de Eventos para examinar as anormalidades. Para obter mais informações, consulte o tópico [log de eventos](./event-logging/index.md) .  
  
- Os contadores de desempenho expostos por meio do monitor de desempenho permitem que você monitore a integridade do seu aplicativo e do sistema. Para obter mais informações, consulte o tópico [contadores de desempenho](./performance-counters/index.md) .  
  
- O <xref:System.ServiceModel.Configuration> namespace permite que você carregue arquivos de configuração e configure um ponto de extremidade de serviço ou cliente. Você pode usar o modelo de objeto para gerar scripts de alterações em muitos aplicativos quando as atualizações devem ser implantadas em vários computadores. Como alternativa, você pode usar a [ferramenta do editor de configuração (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md) para editar as definições de configuração usando um assistente de GUI. Para obter mais informações, consulte o tópico [configurando seu aplicativo](configuring-your-application.md) .  
  
- O WMI permite que você descubra quais serviços estão escutando em um computador e as associações que estão em uso. Para obter mais informações, consulte o tópico [usando instrumentação de gerenciamento do Windows para diagnóstico](./wmi/index.md) .  
  
 O WCF também fornece várias ferramentas de GUI e de linha de comando para facilitar a criação, a implantação e o gerenciamento de aplicativos WCF. Para obter mais informações, consulte [ferramentas de Windows Communication Foundation](../tools.md). Por exemplo, você pode usar a [ferramenta do editor de configuração (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md) para criar e Editar definições de configuração do WCF usando um assistente, em vez de editar XML diretamente. Você também pode usar a [ferramenta Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) para exibir, agrupar e filtrar mensagens de rastreamento para que você possa diagnosticar, reparar e verificar problemas com os serviços WCF.  
  
## <a name="see-also"></a>Consulte também

- [Configurando seu aplicativo](configuring-your-application.md)
- [Implantando serviços](deploying-services.md)
- [Referência de exceções](./exceptions-reference/index.md)
- [Log de eventos](./event-logging/index.md)
- [Registro em log de mensagens](message-logging.md)
- [Ferramenta Configuration Editor (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md)
- [Ferramenta Visualizador de Rastreamento de Serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md)
- [Ferramenta de registro de ServiceModel](servicemodel-registration-tool.md)
- [Rastreamento](./tracing/index.md)
- [Usando Windows Management Instrumentation para diagnóstico](./wmi/index.md)
- [Contadores de desempenho](./performance-counters/index.md)
- [Ferramentas do Windows Communication Foundation](../tools.md)
