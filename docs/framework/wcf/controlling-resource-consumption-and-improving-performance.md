---
description: 'Saiba mais sobre: controlando o consumo de recursos e melhorando o desempenho'
title: Controlando o consumo de recursos e a melhoria de desempenho
ms.date: 03/30/2017
ms.assetid: 9a829669-5f76-4c88-80ec-92d0c62c0660
ms.openlocfilehash: df2a2ae8235acecd269644690546098f36bf73c8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794449"
---
# <a name="controlling-resource-consumption-and-improving-performance"></a>Controlando o consumo de recursos e a melhoria de desempenho

Este tópico descreve várias propriedades em áreas diferentes da arquitetura do Windows Communication Foundation (WCF) que funcionam para controlar o consumo de recursos e afetar as métricas de desempenho.

## <a name="properties-that-constrain-resource-consumption-in-wcf"></a>Propriedades que restringem o consumo de recursos no WCF

 O Windows Communication Foundation (WCF) aplica restrições a certos tipos de processos para fins de segurança ou desempenho. Essas restrições são fornecidas em dois formulários principais, cotas e restrições. As *cotas* são limites que, quando atingido ou excedido, disparam uma exceção imediata em algum momento no sistema. Restrições *são limites* que não fazem com que uma exceção seja gerada imediatamente. Em vez disso, quando um limite de aceleração é atingido, o processamento continua, mas dentro dos limites definidos por esse valor de limitação. Esse processamento limitado pode disparar uma exceção em outro lugar, mas isso depende do aplicativo.

 Além da distinção entre cotas e restrições, algumas propriedades de restrição estão localizadas no nível de serialização, algumas no nível de transporte e algumas no nível do aplicativo. Por exemplo, a cota <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=nameWithType> , que é implementada por todos os elementos de associação de transporte fornecidos pelo sistema, é definida como 65.536 bytes por padrão para impedir que clientes mal-intencionados entrem em ataques de negação de serviço contra um serviço, causando o consumo excessivo de memória. (Normalmente, você pode aumentar o desempenho reduzindo esse valor.)

 Um exemplo de uma cota de serialização é a <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> propriedade, que especifica o número máximo de objetos que o serializador serializa ou desserializa em uma única <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A> chamada de método. Um exemplo de um acelerador de nível de aplicativo é a <xref:System.ServiceModel.Dispatcher.ServiceThrottle.MaxConcurrentSessions%2A?displayProperty=nameWithType> propriedade, que por padrão restringe o número de conexões de canal de sessão simultâneas para 10. (Ao contrário das cotas, se esse valor de limitação for atingido, o aplicativo continuará processando, mas não aceitará nenhum novo canal de sessão, o que significa que novos clientes não poderão se conectar até que um dos outros canais de sessão seja encerrado.)

 Esses controles são projetados para fornecer uma mitigação pronta para uso em determinados tipos de ataques ou para melhorar as métricas de desempenho, como o volume de memória, o tempo de inicialização e assim por diante. No entanto, dependendo do aplicativo, esses controles podem impedir o desempenho do aplicativo de serviço ou impedir que o aplicativo funcione. Por exemplo, um aplicativo projetado para transmitir vídeo pode facilmente exceder a <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=nameWithType> propriedade padrão. Este tópico fornece uma visão geral dos vários controles aplicados aos aplicativos em todos os níveis do WCF, descreve várias maneiras de obter mais informações sobre se uma configuração está prejudicando seu aplicativo e descreve maneiras de corrigir vários problemas. A maioria das limitações e algumas cotas estão disponíveis no nível do aplicativo, mesmo quando a propriedade base é uma restrição de serialização ou transporte. Por exemplo, você pode definir a <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> propriedade usando a <xref:System.ServiceModel.ServiceBehaviorAttribute.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> Propriedade na classe de serviço.

> [!NOTE]
> Se você tiver um problema específico, primeiro leia o guia de [início rápido de solução de problemas do WCF](wcf-troubleshooting-quickstart.md) para ver se o problema (e uma solução) está listado lá.

 As propriedades que restringem os processos de serialização são listadas em [considerações de segurança para dados](./feature-details/security-considerations-for-data.md). As propriedades que restringem o consumo de recursos relacionados aos transportes são listadas em [cotas de transporte](./feature-details/transport-quotas.md). As propriedades que restringem o consumo de recursos na camada de aplicativo são os membros da <xref:System.ServiceModel.Dispatcher.ServiceThrottle> classe.

## <a name="detecting-application-and-performance-issues-related-to-quota-settings"></a>Detectando problemas de desempenho e aplicativo relacionados às configurações de cota

 Os padrões dos valores anteriores foram escolhidos para habilitar a funcionalidade básica do aplicativo em uma ampla variedade de tipos de aplicativos, fornecendo proteção básica contra problemas comuns de segurança. No entanto, diferentes designs de aplicativo podem exceder uma ou mais configurações de limitação, embora o aplicativo de outra forma seja seguro e funcione como projetado. Nesses casos, você deve identificar quais valores de limitação estão sendo excedidos e em qual nível e decidir o curso de ação apropriado para aumentar a taxa de transferência do aplicativo.

 Normalmente, ao gravar o aplicativo e depurá-lo, você define a <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> propriedade como `true` no arquivo de configuração ou programaticamente. Isso instrui o WCF a retornar rastreamentos de pilha de exceção de serviço para o aplicativo cliente para exibição. Esse recurso relata a maioria das exceções de nível de aplicativo de forma a exibir quais configurações de cota podem estar envolvidas, se esse for o problema.

 Algumas exceções acontecem em tempo de execução abaixo da visibilidade da camada de aplicativo e não são retornadas usando esse mecanismo, e elas podem não ser tratadas por uma <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=nameWithType> implementação personalizada. Se você estiver em um ambiente de desenvolvimento como Microsoft Visual Studio, a maioria dessas exceções será exibida automaticamente. No entanto, algumas exceções podem ser mascaradas por configurações de ambiente de desenvolvimento, como [apenas meu código](/visualstudio/debugger/just-my-code) Visual Studio.

 Independentemente dos recursos do seu ambiente de desenvolvimento, você pode usar recursos de rastreamento do WCF e log de mensagens para depurar todas as exceções e ajustar o desempenho de seus aplicativos. Para obter mais informações, consulte [usando o rastreamento para solucionar problemas de seu aplicativo](./diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md).

## <a name="performance-issues-and-xmlserializer"></a>Problemas de desempenho e XmlSerializer

 Serviços e aplicativos cliente que usam tipos de dados que são serializáveis usando o <xref:System.Xml.Serialization.XmlSerializer> código de serialização Generate e compile para esses tipos de dados em tempo de execução, o que pode resultar em um desempenho de inicialização lento.

> [!NOTE]
> O código de serialização gerado previamente pode ser usado somente em aplicativos cliente e não em serviços.

 A [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) pode melhorar o desempenho de inicialização para esses aplicativos, gerando o código de serialização necessário dos assemblies compilados para o aplicativo. Para obter mais informações, consulte [como: melhorar o tempo de inicialização de aplicativos cliente WCF usando o XmlSerializer](./feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md).

## <a name="performance-issues-when-hosting-wcf-services-under-aspnet"></a>Problemas de desempenho ao hospedar serviços WCF em ASP.NET

Quando um serviço WCF é hospedado em IIS e ASP.NET, as definições de configuração do IIS e do ASP.NET podem afetar a taxa de transferência e a superfície de memória do serviço WCF.  Para obter mais informações sobre o desempenho do ASP.NET, consulte [melhorando o desempenho do ASP.net](/previous-versions/msp-n-p/ff647787(v=pandp.10)). Uma configuração que pode ter consequências indesejadas é <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A> , que é uma propriedade do <xref:System.Web.Configuration.ProcessModelSection> . Se seu aplicativo tiver um número fixo ou pequeno de clientes, <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A> a configuração para 2 pode fornecer um aumento de taxa de transferência em um computador com multiprocessador que tenha uma utilização de CPU perto de 100%. Esse aumento no desempenho vem com um custo: ele também causará um aumento no uso da memória, o que pode reduzir a escalabilidade.

## <a name="see-also"></a>Consulte também

- [Administração e diagnósticos](./diagnostics/index.md)
- [Dados grandes e streaming](./feature-details/large-data-and-streaming.md)
