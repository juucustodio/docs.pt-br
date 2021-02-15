---
description: 'Saiba mais sobre: ServiceDescription e referência WSDL'
title: ServiceDescription and WSDL Reference
ms.date: 03/30/2017
ms.assetid: eedc025d-abd9-46b1-bf3b-61d2d5c95fd6
ms.openlocfilehash: 0ce3dc49d71eda1f9fe36940f153735b43be917b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793513"
---
# <a name="servicedescription-and-wsdl-reference"></a>ServiceDescription and WSDL Reference

Este tópico descreve como Windows Communication Foundation (WCF) mapeia documentos WSDL (linguagem de descrição de serviços Web) de e para <xref:System.ServiceModel.Description.ServiceDescription> instâncias do.  
  
## <a name="how-servicedescription-maps-to-wsdl-11"></a>Como o ServiceDescription é mapeado para o WSDL 1,1  

 Você pode usar o WCF para exportar documentos WSDL de uma <xref:System.ServiceModel.Description.ServiceDescription> instância do para seu serviço. Os documentos WSDL são gerados automaticamente para seu serviço quando você publica pontos de extremidade de metadados.  
  
 Você também pode importar <xref:System.ServiceModel.Description.ServiceEndpoint> instâncias, <xref:System.ServiceModel.Description.ContractDescription> instâncias e instâncias <xref:System.ServiceModel.Channels.Binding> de documentos WSDL usando o `WsdlImporter` tipo.  
  
 Os documentos WSDL, exportados pelo WCF, importam todas as definições de esquema XML usadas de documentos de esquema XML externos. Um documento de esquema XML separado é exportado para cada namespace de destino que os tipos de dados usam no serviço. Da mesma forma, um documento WSDL separado é exportado para cada namespace de destino usado pelos contratos de serviço.  
  
### <a name="servicedescription"></a>ServiceDescription  

 Uma <xref:System.ServiceModel.Description.ServiceDescription> instância é mapeada para um `wsdl:service` elemento. Uma <xref:System.ServiceModel.Description.ServiceDescription> instância contém uma coleção de <xref:System.ServiceModel.Description.ServiceEndpoint> instâncias que cada mapa para `wsdl:port` elementos individuais.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsdl:service` /@name valor do serviço.|  
|`Namespace`|O targetNamespace para a `wsdl:service` definição do serviço.|  
|`Endpoints`|As `wsdl:port` definições para o serviço.|  
  
### <a name="serviceendpoint"></a>ServiceEndpoint  

 Uma <xref:System.ServiceModel.Description.ServiceEndpoint> instância é mapeada para um `wsdl:port` elemento. Uma <xref:System.ServiceModel.Description.ServiceEndpoint> instância contém um endereço, uma associação e um contrato.  
  
 Os comportamentos de ponto de extremidade que implementam a <xref:System.ServiceModel.Description.IWsdlExportExtension> interface podem modificar o `wsdl:port` elemento para o ponto de extremidade ao qual estão anexados.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsdl:port` /@name valor do ponto de extremidade e o `wsdl:binding` /@name valor da Associação de ponto de extremidade.|  
|`Address`|O endereço para a `wsdl:port` definição do ponto de extremidade.<br /><br /> O transporte para o ponto de extremidade determina o formato do endereço. Por exemplo, para transportes com suporte do WCF, ele pode ser um endereço SOAP ou uma referência de ponto de extremidade.|  
|`Binding`|A `wsdl:binding` definição do ponto de extremidade.<br /><br /> Ao contrário das `wsdl:binding` definições, as associações no WCF não são ligadas a nenhum contrato.|  
|`Contract`|A `wsdl:portType` definição do ponto de extremidade.|  
|`Behaviors`|Os comportamentos de ponto de extremidade que implementam a <xref:System.ServiceModel.Description.IWsdlExportExtension> interface podem modificar o `wsdl:port` para o ponto de extremidade.|  
  
### <a name="bindings"></a>Associações  

 A instância de associação para uma `ServiceEndpoint` instância é mapeada para uma `wsdl:binding` definição. Ao contrário das `wsdl:binding` definições, que devem ser associadas a uma `wsdl:portType` definição específica, as associações do WCF são independentes de qualquer contrato.  
  
 Uma associação é composta de uma coleção de elementos de associação. Cada elemento descreve algum aspecto de como o ponto de extremidade se comunica com os clientes. Além disso, uma associação tem um <xref:System.ServiceModel.Channels.MessageVersion> que indica o <xref:System.ServiceModel.EnvelopeVersion> e o <xref:System.ServiceModel.Channels.AddressingVersion> para o ponto de extremidade.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|Usado no nome padrão de um ponto de extremidade, que é o nome de associação com o nome do contrato acrescentado, separado por um sublinhado.|  
|`Namespace`|O `targetNamespace` para a `wsdl:binding` definição.<br /><br /> Na importação, se uma política for anexada à porta WSDL, o namespace de associação importado será mapeado para o `targetNamespace` para a `wsdl:port` definição.|  
|`BindingElementCollection`, conforme retornado pelo `CreateBindingElements` método ()|Várias extensões específicas de domínio para a `wsdl:binding` definição, normalmente as declarações de política.|  
|`MessageVersion`|O `EnvelopeVersion` e `AddressingVersion` para o ponto de extremidade.<br /><br /> Quando `MessageVersion.None` é especificado, a associação WSDL não contém uma ligação SOAP e a porta WSDL não contém WS-Addressing conteúdo. Essa configuração normalmente é usada para pontos de extremidade de POX (XML antigo).|  
  
#### <a name="bindingelements"></a>BindingElements  

 Os elementos de associação para uma associação de ponto de extremidade são mapeados para várias extensões WSDL no `wsdl:binding` , como declarações de política.  
  
 O <xref:System.ServiceModel.Channels.TransportBindingElement> para a associação determina o Uniform Resource Identifier de transporte (URI) para uma associação SOAP.  
  
#### <a name="addressingversion"></a>AddressingVersion  

 O `AddressingVersion` em uma associação é mapeado para a versão de endereçamento usada no `wsd:port` . O WCF dá suporte a endereços SOAP 1,1 e SOAP 1,2 e WS-Addressing referências de ponto de extremidade 08/2004 e WS-Addressing 1,0.  
  
#### <a name="envelopeversion"></a>EnvelopeVersion  

 O `EnvelopeVersion` em uma associação é mapeado para a versão do SOAP usada no `wsdl:binding` . O WCF dá suporte a associações SOAP 1,1 e SOAP 1,2.  
  
### <a name="contracts"></a>Contratos  

 A <xref:System.ServiceModel.Description.ContractDescription> instância de uma `ServiceEndpoint` instância é mapeada para um `wsdl:portType` . Uma `ContractDescription` instância descreve todas as operações de um determinado contrato.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsdl:portType` /@name valor do contrato.|  
|`Namespace`|O targetNamespace para a `wsdl:portType` definição.|  
|`SessionMode`|O `wsdl:portType` /@msc:usingSession valor do contrato. Este atributo é uma extensão WCF para o WSDL 1,1.|  
|`Operations`|As `wsdl:operation` definições do contrato.|  
  
### <a name="operations"></a>Operações  

 Uma <xref:System.ServiceModel.Description.OperationDescription> instância é mapeada para um `wsdl:portType` / `wsdl:operation` . Um `OperationDescription` contém uma coleção de `MessageDescription` instâncias que descrevem as mensagens para a operação.  
  
 Dois comportamentos de operação participam muito de como um `OperationDescription` é mapeado para um documento WSDL: `DataContractSerializerOperationBehavior` e `XmlSerializerOperationBehavior` .  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsdl:portType` / `wsdl:operation` /@name valor da operação.|  
|`ProtectionLevel`|Declarações de proteção na política de segurança anexadas às `wsdl:binding/wsdl:operation` mensagens para esta operação.|  
|`IsInitiating`|O `wsdl:portType` / `wsdl:operation` /@msc:isInitiating valor da operação. Este atributo é uma extensão WCF para o WSDL 1,1.|  
|`IsTerminating`|O `wsdl:portType` / `wsdl:operation` /@msc:isTerminating valor da operação. Este atributo é uma extensão WCF para o WSDL 1,1.|  
|`Messages`|As `wsdl:portType` / `wsdl:operation` / `wsdl:input` `wsdl:portType` / `wsdl:operation` / `wsdl:output` mensagens e para a operação.|  
|`Faults`|As `wsdl:portType` / `wsdl:operation` / `wsdl:fault` definições para a operação.|  
|`Behaviors`|O `DataContractSerializerOperationBehavior` e `XmlSerializerOperationBehavior` lidar com a associação de operação e as mensagens de operação.|  
  
#### <a name="the-datacontractserializeroperationbehavior"></a>O DataContractSerializerOperationBehavior  

 O `DataContractSerializerOperationBehavior` para uma operação é uma `IWsdlExportExtension` implementação que exporta as mensagens WSDL e a associação para essa operação. Os tipos de esquema XML são exportados usando o `XsdDataContractExporter` . O `DataContractSerializerOperationBehavior` também determina o uso, o estilo e o exportador de esquema e o importador a ser usado para essa operação.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`DataContractFormatAttribute`|A `Style` propriedade desse atributo é mapeada para o `wsdl:binding` / `wsdl:operation` / `soap:operation` /@style valor da operação.<br /><br /> O `DataContractSerializerOperationBehavior` oferece suporte apenas ao uso literal dos tipos de esquema no WSDL.|  
  
#### <a name="the-xmlserializeroperationbehavior"></a>O XmlSerializerOperationBehavior  

 O `XmlSerializerOperationBehavior` para uma operação é uma `IWsdlExportExtension` implementação que exporta as mensagens WSDL e a associação para essa operação. Os tipos de esquema XML são exportados usando o `XmlSchemaExporter` . O `XmlSerializerOperationBehavior` também determina o uso, o estilo e o exportador de esquema e o importador a ser usado para essa operação.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`XmlSerializerFormatAttribute`|A `Style` propriedade desse atributo é mapeada para o `wsdl:binding` / `wsdl:operation` / `soap:operation` /@style valor da operação.<br /><br /> A `Use` propriedade desse atributo é mapeada para os `wsdl:binding` / `wsdl:operation` / `soap:operation` valores/* /@use para todas as mensagens na operação.|  
  
### <a name="messages"></a>Mensagens  

 Uma `MessageDescription` instância é mapeada para um `wsdl:message` que é referenciado por uma `wsdl:portType` / `wsdl:operation` / `wsdl:input` ou uma `wsdl:portType` / `wsdl:operation` / `wsdl:output` mensagem em uma operação. Um `MessageDescription` tem um corpo e cabeçalhos.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Action`|A ação SOAP ou WS-Addressing para a mensagem.<br /><br /> Observe que as operações que usam a cadeia de caracteres de ação "*" não são representadas em WSDL.|  
|`Direction`|`MessageDirection.Input` mapeia para `wsdl:input` .<br /><br /> `MessageDirection.Output` mapeia para `wsdl:output` .|  
|`ProtectionLevel`|Declarações de proteção na política de segurança anexada à `wsdl:message` definição desta mensagem.|  
|`Body`|O corpo da mensagem para a mensagem.|  
|`Headers`|Os cabeçalhos da mensagem.|  
|`ContractDescription.Name`, `OperationContract.Name`|Na exportação, usado para derivar o `wsdl:message` /@name valor.|  
  
#### <a name="message-body"></a>Corpo da mensagem  

 Uma `MessageBodyDescription` instância é mapeada para as `wsdl:message` / `wsdl:part` definições do corpo de uma mensagem. O corpo da mensagem pode ser encapsulado ou vazio.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`WrapperName`|Se o estilo não for RPC, o será `WrapperName` mapeado para o nome do elemento referenciado pelo `wsdl:message` / `wsdl:part` com @name definido como "Parameters".|  
|`WrapperNamespace`|Se o estilo não for RPC, o será `WrapperNamespace` mapeado para o namespace do elemento para o `wsdl:message` / `wsdl:part` com @name definido como "Parameters".|  
|`Parts`|As partes da mensagem para este corpo da mensagem.|  
|`ReturnValue`|O elemento filho do elemento wrapper se existir um elemento wrapper (estilo empacotado do documento ou estilo RPC), caso contrário, o primeiro `wsdl:message` / `wsdl:part` na mensagem.|  
  
#### <a name="message-parts"></a>Partes da mensagem  

 Uma `MessagePartDescription` instância é mapeada para um `wsdl:message` / `wsdl:part` e o tipo ou elemento de esquema XML para o qual a parte da mensagem aponta.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsd:message` / `wsdl:part` /@name valor da parte da mensagem e o nome do elemento para o qual a parte da mensagem aponta.|  
|`Namespace`|O namespace do elemento ao qual a parte da mensagem aponta.|  
|`Index`|O índice do `wsdl:message` / `wsdl:part` para a mensagem.|  
|`ProtectionLevel`|Declarações de proteção na política de segurança anexada à `wsdl:message` definição desta parte de mensagem. A política é parametrizada para apontar para a parte de mensagem específica.|  
|`MessageType`|O tipo de esquema XML do elemento ao qual a parte da mensagem aponta.|  
  
#### <a name="message-headers"></a>Cabeçalhos da mensagem  

 Uma `MessageHeaderDescription` instância é uma parte de mensagem que também é mapeada para uma `soap:header` Associação para a parte da mensagem.  
  
### <a name="faults"></a>Falhas  

 Uma `FaultDescription` instância é mapeada para uma `wsdl:portType` / `wsdl:operation` / `wsdl:fault` definição e sua `wsdl:message` definição associada. O `wsdl:message` é adicionado ao mesmo namespace de destino que seu tipo de porta WSDL associado. O `wsdl:message` tem uma única parte de mensagem denominada "Detail" que aponta para o elemento de esquema XML que corresponde ao `DefaultType` valor da propriedade da `FaultDescription` instância.  
  
|Propriedades|Mapeamento de WSDL|  
|----------------|------------------|  
|`Name`|O `wsdl:portType` / `wsdl:operation` / `wsdl:fault` /@name valor da falha.|  
|`Namespace`|O namespace do elemento de esquema XML para o qual a parte da mensagem de detalhes de falha aponta.|  
|`Action`|A ação SOAP ou WS-Addressing para a falha.|  
|`ProtectionLevel`|Declarações de proteção na política de segurança anexada à `wsdl:message` definição para essa falha.|  
|`DetailType`|O tipo de esquema XML do elemento para o qual a parte de mensagem de detalhe aponta.|  
|`Name, ContractDescription.Name, OperationDescription.Name,`|Usado para derivar o `wsdl:message` /@name valor da mensagem de falha.|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description>
