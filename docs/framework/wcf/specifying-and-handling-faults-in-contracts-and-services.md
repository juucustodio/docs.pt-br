---
description: 'Saiba mais sobre: especificando e manipulando falhas em contratos e serviços'
title: Especificando e lidando com falhas em contratos e serviços
ms.date: 03/30/2017
helpviewer_keywords:
- handling faults [WCF]
ms.assetid: a9696563-d404-4905-942d-1e0834c26dea
ms.openlocfilehash: 32a1c795d2be964ff5da259b70a5695ddedfadb2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676385"
---
# <a name="specifying-and-handling-faults-in-contracts-and-services"></a>Especificando e lidando com falhas em contratos e serviços

Os aplicativos Windows Communication Foundation (WCF) manipulam situações de erro mapeando objetos de exceção gerenciados para objetos de falha SOAP e objetos de falha SOAP para objetos de exceção gerenciados. Os tópicos nesta seção discutem como criar contratos para expor condições de erro como falhas de SOAP personalizadas, como retornar essas falhas como parte da implementação do serviço e como os clientes interceptam essas falhas.

## <a name="error-handling-overview"></a>Visão geral do tratamento de erros

Em todos os aplicativos gerenciados, os erros de processamento são representados por <xref:System.Exception> objetos. Em aplicativos baseados em SOAP, como aplicativos WCF, os métodos de serviço comunicam informações de erro de processamento usando mensagens de falha de SOAP. Falhas de SOAP são tipos de mensagem que são incluídos nos metadados de uma operação de serviço e, portanto, criam um contrato de falha que os clientes podem usar para tornar suas operações mais robustas ou interativas. Além disso, como as falhas de SOAP são expressas para clientes em formato XML, é um sistema de tipo altamente interoperável que os clientes em qualquer plataforma SOAP podem usar, aumentando o alcance de seu aplicativo WCF.

Como os aplicativos WCF são executados em ambos os tipos de sistemas de erro, todas as informações de exceção gerenciadas enviadas ao cliente devem ser convertidas de exceções em falhas de SOAP no serviço, enviadas e convertidas de falhas de SOAP para exceções de falha em clientes WCF. No caso de clientes duplex, os contratos de cliente também podem enviar falhas SOAP de volta para um serviço. Em ambos os casos, você pode usar os comportamentos de exceção de serviço padrão ou pode controlar explicitamente se — e como — as exceções são mapeadas para as mensagens de falha.

Dois tipos de falhas SOAP podem ser enviados: *declarados* e não *declarados*. As falhas de SOAP declaradas são aquelas em que uma operação tem um <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> atributo que especifica um tipo de falha SOAP personalizado. Não *declarado* Falhas de SOAP não são especificadas no contrato para uma operação.

É altamente recomendável que as operações de serviço declarem suas falhas usando o <xref:System.ServiceModel.FaultContractAttribute> atributo para especificar formalmente todas as falhas SOAP que um cliente pode esperar receber no curso normal de uma operação. Também é recomendável que você retorne em uma falha SOAP apenas as informações que um cliente deve saber para minimizar a divulgação de informações.

Normalmente, os serviços (e clientes duplex) realizam as seguintes etapas para integrar com êxito o tratamento de erros em seus aplicativos:

- Mapeie condições de exceção para falhas de SOAP personalizadas.

- Os clientes e serviços enviam e recebem falhas de SOAP como exceções.

Além disso, os clientes e serviços WCF podem usar falhas SOAP não declaradas para fins de depuração e podem estender o comportamento de erro padrão. As seções a seguir discutem essas tarefas e conceitos.

## <a name="map-exceptions-to-soap-faults"></a>Mapear exceções para falhas de SOAP

A primeira etapa na criação de uma operação que manipula as condições de erro é decidir em quais condições um aplicativo cliente deve ser informado sobre erros. Algumas operações têm condições de erro específicas para sua funcionalidade. Por exemplo, uma `PurchaseOrder` operação pode retornar informações específicas aos clientes que não têm mais permissão para iniciar uma ordem de compra. Em outros casos, como um `Calculator` serviço, uma falha de SOAP mais geral `MathFault` pode ser capaz de descrever todas as condições de erro em um serviço inteiro. Depois que as condições de erro dos clientes do serviço são identificadas, uma falha de SOAP personalizada pode ser construída e a operação pode ser marcada como retornando essa falha de SOAP quando ocorre a condição de erro correspondente.

Para obter mais informações sobre esta etapa do desenvolvimento de seu serviço ou cliente, consulte [definindo e especificando falhas](defining-and-specifying-faults.md).

## <a name="clients-and-services-handle-soap-faults-as-exceptions"></a>Clientes e serviços lidam com falhas de SOAP como exceções

Identificar as condições de erro da operação, definir falhas de SOAP personalizadas e marcar essas operações como retornando essas falhas são as primeiras etapas do tratamento de erros bem-sucedido em aplicativos WCF. A próxima etapa é implementar corretamente o envio e o recebimento dessas falhas. Normalmente, os serviços enviam falhas para informar os aplicativos cliente sobre as condições de erro, mas os clientes duplex também podem enviar falhas de SOAP aos serviços.

Para obter mais informações, consulte [enviando e recebendo falhas](sending-and-receiving-faults.md).

## <a name="undeclared-soap-faults-and-debugging"></a>Falhas e depuração de SOAP não declaradas

As falhas de SOAP declaradas são extremamente úteis para a criação de aplicativos robustos, interoperáveis e distribuídos. No entanto, em alguns casos, é útil para um serviço (ou cliente duplex) enviar uma falha de SOAP não declarada, uma que não é mencionada no WSDL (Web Services Description Language) para essa operação. Por exemplo, ao desenvolver um serviço, podem ocorrer situações inesperadas em que é útil para fins de depuração para enviar informações de volta ao cliente. Além disso, você pode definir a <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> propriedade ou a <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> propriedade como `true` para permitir que os clientes WCF obtenham informações sobre exceções de operação de serviço interno. Tanto o envio de falhas individuais quanto a definição das propriedades de comportamento de depuração são descritos no [envio e recebimento de falhas](sending-and-receiving-faults.md).

> [!IMPORTANT]
> Como as exceções gerenciadas podem expor informações internas do aplicativo, <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> a configuração ou o <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> `true` pode permitir que os clientes WCF obtenham informações sobre exceções de operação de serviço interno, incluindo identificação pessoal ou outras informações confidenciais.
>
> Portanto, <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> a configuração ou <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> para `true` é recomendada apenas como uma maneira de depurar temporariamente um aplicativo de serviço. Além disso, o WSDL para um método que retorna exceções gerenciadas sem tratamento dessa maneira não contém o contrato para o <xref:System.ServiceModel.FaultException%601> do tipo <xref:System.ServiceModel.ExceptionDetail> . Os clientes devem esperar a possibilidade de uma falha SOAP desconhecida (retornada aos clientes WCF como <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> objetos) para obter as informações de depuração corretamente.

## <a name="customizing-error-handling-with-ierrorhandler"></a>Personalizando o tratamento de erros com o IErrorHandler

Se você tiver requisitos especiais para personalizar a mensagem de resposta para o cliente quando ocorrer uma exceção no nível do aplicativo ou executar algum processamento personalizado depois que a mensagem de resposta for retornada, implemente a <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=nameWithType> interface.

## <a name="fault-serialization-issues"></a>Problemas de serialização de falha

Ao desserializar um contrato de falha, o WCF tenta primeiro fazer a correspondência do nome do contrato de falha na mensagem SOAP com o tipo de contrato de falha. Se não for possível encontrar uma correspondência exata, ele pesquisará a lista de contratos de falha disponíveis em ordem alfabética para um tipo compatível. Se dois contratos de falha forem tipos compatíveis (um é uma subclasse de outro, por exemplo), o tipo incorreto poderá ser usado para desserializar a falha. Isso só ocorrerá se o contrato de falha não especificar um nome, um namespace e uma ação. Para evitar que esse problema ocorra, sempre qualifique totalmente os contratos de falha especificando o nome, o namespace e os atributos de ação. Além disso, se você tiver definido um número de contratos de falha relacionados derivados de uma classe base compartilhada, certifique-se de marcar todos os novos membros com `[DataMember(IsRequired=true)]` . Para obter mais informações sobre esse `IsRequired` atributo, consulte <xref:System.Runtime.Serialization.DataMemberAttribute> . Isso impedirá que uma classe base seja um tipo compatível e force a falha a ser desserializada no tipo derivado correto.

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.FaultException>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.FaultException>
- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.CommunicationException>
- <xref:System.ServiceModel.FaultContractAttribute.Action%2A>
- <xref:System.ServiceModel.FaultException.Code%2A>
- <xref:System.ServiceModel.FaultException.Reason%2A>
- <xref:System.ServiceModel.FaultCode.SubCode%2A>
- <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>
- [Definindo e especificando falhas](defining-and-specifying-faults.md)
