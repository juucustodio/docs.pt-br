---
description: 'Saiba mais sobre: especificando o comportamento de Run-Time de serviço'
title: Especificando comportamento de tempo de execução de serviço
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
ms.openlocfilehash: a7336a64c32773b0fa960879021bb04cccfaa24f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703478"
---
# <a name="specifying-service-run-time-behavior"></a>Especificando comportamento de tempo de execução de serviço

Depois de criar um contrato de serviço ([Criando contratos de serviço](designing-service-contracts.md)) e implementar seu contrato de serviço ([implementando contratos de serviço](implementing-service-contracts.md)), você pode configurar o comportamento da operação do tempo de execução do serviço. Este tópico aborda os comportamentos de serviço e operação fornecidos pelo sistema e descreve onde encontrar mais informações para criar novos comportamentos. Embora alguns comportamentos sejam aplicados como atributos, muitos são aplicados usando um arquivo de configuração de aplicativo ou programaticamente. Para obter mais informações sobre como configurar seu aplicativo de serviço, consulte [Configurando serviços](configuring-services.md).  
  
## <a name="overview"></a>Visão geral  

 O contrato define as entradas, as saídas, os tipos de dados e os recursos de um serviço desse tipo. A implementação de um contrato de serviço cria uma classe que, quando configurada com uma associação em um endereço, atende ao contrato que ele implementa. Informações contratuais, de associação e de endereço são conhecidas pelo cliente; sem eles, o cliente não pode fazer uso do serviço.  
  
 No entanto, as especificações de operação, como problemas de threading ou gerenciamento de instância, são opacas para os clientes. Depois de implementar seu contrato de serviço, você pode configurar um grande número de características de operação usando *comportamentos*. Os comportamentos são objetos que modificam o tempo de execução do Windows Communication Foundation (WCF) definindo uma propriedade de tempo de execução ou inserindo um tipo de personalização no tempo de execução. Para obter mais informações sobre como modificar o tempo de execução criando comportamentos definidos pelo usuário, consulte [estendendo o ServiceHost e a camada do modelo de serviço](./extending/extending-servicehost-and-the-service-model-layer.md).  
  
 Os <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType> <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=nameWithType> atributos e são os comportamentos mais amplamente úteis e expõem os recursos de operação solicitados com mais frequência. Como eles são atributos, você os aplica à implementação do serviço ou da operação. Outros comportamentos, como o <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> ou <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=nameWithType> , normalmente são aplicados usando um arquivo de configuração de aplicativo, embora você possa usá-los programaticamente.  
  
 Este tópico fornece uma visão geral dos <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atributos e, descreve os vários escopos nos quais os comportamentos podem operar e fornece uma descrição rápida de muitos dos comportamentos fornecidos pelo sistema nos vários escopos que podem ser de interesse dos desenvolvedores do WCF.  
  
## <a name="servicebehaviorattribute-and-operationbehaviorattribute"></a>ServiceBehaviorAttribute e OperationBehaviorAttribute  

 Os comportamentos mais importantes são os <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atributos e, que você pode usar para controlar:  
  
- Tempos de vida da instância  
  
- Suporte a simultaneidade e sincronização  
  
- Comportamento da configuração  
  
- Comportamento da transação  
  
- Comportamento de serialização  
  
- Transformação de metadados  
  
- Tempo de vida da sessão  
  
- Filtragem de endereços e processamento de cabeçalho  
  
- Representação  
  
- Para usar esses atributos, marque a implementação do serviço ou da operação com o atributo apropriado para esse escopo e defina as propriedades. Por exemplo, o exemplo de código a seguir mostra uma implementação de operação que usa a <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=nameWithType> propriedade para exigir que os chamadores dessa operação ofereçam suporte à representação.  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 Muitas das propriedades exigem suporte adicional da associação. Por exemplo, uma operação que requer uma transação do cliente deve ser configurada para usar uma associação que dá suporte a transações fluidas.  
  
### <a name="well-known-singleton-services"></a>Well-Known serviços singleton  

 Você pode usar os <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atributos e para controlar determinados tempos de vida, os <xref:System.ServiceModel.InstanceContext> e dos objetos de serviço que implementam as operações.  
  
 Por exemplo, a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> propriedade controla com que frequência o <xref:System.ServiceModel.InstanceContext> é liberado e as <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=nameWithType> Propriedades e controlam quando o objeto de serviço é liberado.  
  
 No entanto, você também pode criar um objeto de serviço por conta própria e criar o host de serviço usando esse objeto. Para fazer isso, você também deve definir a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> propriedade como <xref:System.ServiceModel.InstanceContextMode.Single> ou uma exceção é lançada quando o host de serviço é aberto.  
  
 Use o <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29> construtor para criar um serviço desse tipo. Ele fornece uma alternativa à implementação de um personalizado <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=nameWithType> quando você deseja fornecer uma instância de objeto específica para uso por um serviço singleton. Você pode usar essa sobrecarga quando o tipo de implementação de serviço for difícil de construir (por exemplo, se ele não implementar um construtor público sem parâmetros).
  
 Observe que, quando um objeto é fornecido a esse construtor, alguns recursos relacionados ao comportamento de instanciação do Windows Communication Foundation (WCF) funcionam de maneira diferente. Por exemplo, <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=nameWithType> a chamada não tem efeito quando uma instância de objeto bem conhecida é fornecida. Da mesma forma, qualquer outro mecanismo de liberação de instância é ignorado. A <xref:System.ServiceModel.ServiceHost> classe sempre se comporta como se a <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> Propriedade fosse definida como <xref:System.ServiceModel.ReleaseInstanceMode.None?displayProperty=nameWithType> para todas as operações.  
  
## <a name="other-service-endpoint-contract-and-operation-behaviors"></a>Outros comportamentos de serviço, ponto de extremidade, contrato e operação  

 Comportamentos de serviço, como o <xref:System.ServiceModel.ServiceBehaviorAttribute> atributo, operam em um serviço inteiro. Por exemplo, se você definir a <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> propriedade como <xref:System.ServiceModel.ConcurrencyMode.Multiple?displayProperty=nameWithType> você deve tratar problemas de sincronização de threads dentro de cada operação nesse serviço por conta própria. Os comportamentos de ponto de extremidade operam em um ponto de extremidade; muitos dos comportamentos de ponto de extremidade fornecidos pelo sistema são para a funcionalidade do cliente. Os comportamentos de contrato operam no nível do contrato e os comportamentos de operação modificam a entrega da operação.  
  
 Muitos desses comportamentos são implementados em atributos e você faz uso deles como faz os <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atributos e — aplicando-os à implementação de operação ou da classe de serviço apropriada. Outros comportamentos, como os <xref:System.ServiceModel.Description.ServiceMetadataBehavior> objetos ou <xref:System.ServiceModel.Description.ServiceDebugBehavior> , normalmente são aplicados usando um arquivo de configuração de aplicativo, embora eles também possam ser usados programaticamente.  
  
 Por exemplo, a publicação de metadados é configurada usando o <xref:System.ServiceModel.Description.ServiceMetadataBehavior> objeto. O arquivo de configuração de aplicativo a seguir mostra o uso mais comum.  
  
 [!code-xml[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.exe.config#1)]  
  
 As seções a seguir descrevem muitos dos comportamentos mais úteis fornecidos pelo sistema que você pode usar para modificar a entrega de tempo de execução do seu serviço ou cliente. Consulte o tópico de referência para determinar como usar cada um.  
  
### <a name="service-behaviors"></a>Comportamentos de serviço  

 Os comportamentos a seguir operam em serviços.  
  
- <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>. Aplicado a um serviço WCF para indicar se esse serviço pode ser executado no modo de compatibilidade do ASP.NET.  
  
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. Controla como o serviço autoriza as declarações do cliente.  
  
- <xref:System.ServiceModel.Description.ServiceCredentials>. Configura uma credencial de serviço. Use essa classe para especificar a credencial para o serviço, como um certificado X. 509.  
  
- <xref:System.ServiceModel.Description.ServiceDebugBehavior>. Habilita a depuração e recursos de informações de ajuda para um serviço WCF.  
  
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>. Controla a publicação de metadados de serviço e informações associadas.  
  
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>. Especifica o comportamento de auditoria de eventos de segurança.  
  
- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>. Define as configurações de taxa de transferência de tempo de execução que permitem ajustar o desempenho do serviço.  
  
### <a name="endpoint-behaviors"></a>Comportamentos de ponto de extremidade  

 Os comportamentos a seguir operam em pontos de extremidade. Muitos desses comportamentos são usados em aplicativos cliente.  
  
- <xref:System.ServiceModel.CallbackBehaviorAttribute>. Configura uma implementação de serviço de retorno de chamada em um aplicativo cliente duplex.  
  
- <xref:System.ServiceModel.Description.CallbackDebugBehavior>. Habilita a depuração de serviço para um objeto de retorno de chamada WCF.  
  
- <xref:System.ServiceModel.Description.ClientCredentials>. Permite que o usuário configure credenciais de cliente e serviço, bem como configurações de autenticação de credenciais de serviço para uso no cliente.  
  
- <xref:System.ServiceModel.Description.ClientViaBehavior>. Usado pelos clientes para especificar o Uniform Resource Identifier (URI) para o qual o canal de transporte deve ser criado.  
  
- <xref:System.ServiceModel.Description.MustUnderstandBehavior>. Instrui o WCF a desabilitar o `MustUnderstand` processamento.  
  
- <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>. Instrui o tempo de execução para usar um processo de recebimento síncrono para canais.  
  
- <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. Otimiza as operações de recebimento para transportes que dão suporte a recebimentos transacionais.  
  
### <a name="contract-behaviors"></a>Comportamentos de contrato  

 <xref:System.ServiceModel.DeliveryRequirementsAttribute>. Especifica os requisitos de recurso que as associações devem fornecer para a implementação do serviço ou cliente.  
  
### <a name="operation-behaviors"></a>Comportamentos de operação  

 Os comportamentos de operação a seguir especificam os controles de serialização e de transação para operações.  
  
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>. Representa o comportamento de tempo de execução de <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.  
  
- <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>. Controla o comportamento de tempo de execução do `XmlSerializer` e o associa a uma operação.  
  
- <xref:System.ServiceModel.TransactionFlowAttribute>. Especifica o nível no qual uma operação de serviço aceita um cabeçalho de transação.  
  
## <a name="see-also"></a>Consulte também

- [Configurando serviços](configuring-services.md)
- [Como: controlar instanciação de serviço](./feature-details/how-to-control-service-instancing.md)
