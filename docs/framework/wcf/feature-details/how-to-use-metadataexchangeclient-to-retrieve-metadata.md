---
description: 'Saiba mais sobre: como usar o MetadataExchangeClient para recuperar metadados'
title: 'Como: usar MetadataExchangeClient para recuperar metadados'
ms.date: 03/30/2017
ms.assetid: 0754e9dc-13c5-45c2-81b5-f3da466e5a87
ms.openlocfilehash: 17206bbba2ccde5961326a431b019fb7718f6cd4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734328"
---
# <a name="how-to-use-metadataexchangeclient-to-retrieve-metadata"></a>Como: usar MetadataExchangeClient para recuperar metadados

Use a <xref:System.ServiceModel.Description.MetadataExchangeClient> classe para baixar metadados usando o protocolo de WS-MetadataExchange (MEX). Os arquivos de metadados recuperados são retornados como um <xref:System.ServiceModel.Description.MetadataSet> objeto. O <xref:System.ServiceModel.Description.MetadataSet> objeto retornado contém uma coleção de <xref:System.ServiceModel.Description.MetadataSection> objetos, cada um contendo um dialeto de metadados específico e um identificador. Você pode gravar os metadados retornados em arquivos ou, se os metadados retornados contiverem documentos WSDL (Web Services Description Language), você poderá importar os metadados usando o <xref:System.ServiceModel.Description.WsdlImporter> .  
  
 Os <xref:System.ServiceModel.Description.MetadataExchangeClient> construtores que assumem um endereço usam a associação na <xref:System.ServiceModel.Description.MetadataExchangeBindings> classe estática que corresponde ao esquema de Uniform Resource Identifier (URI) do endereço. Como alternativa, você pode usar o <xref:System.ServiceModel.Description.MetadataExchangeClient> Construtor que permite especificar explicitamente a associação a ser usada. A associação especificada é usada para resolver todas as referências de metadados.  
  
 Assim como qualquer outro cliente do Windows Communication Foundation (WCF), o <xref:System.ServiceModel.Description.MetadataExchangeClient> tipo fornece um construtor para carregar as configurações de ponto de extremidade do cliente usando o nome de configuração do ponto de extremidade. A configuração do ponto de extremidade especificado deve especificar o <xref:System.ServiceModel.Description.IMetadataExchange> contrato. O endereço na configuração do ponto de extremidade não é carregado, portanto, você deve usar uma das <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> sobrecargas que usam um endereço. Quando você especifica o endereço de metadados usando uma <xref:System.ServiceModel.EndpointAddress> instância, o <xref:System.ServiceModel.Description.MetadataExchangeClient> pressupõe que o endereço aponta para um ponto de extremidade MEX. Se você especificar o endereço de metadados como uma URL, também precisará especificar qual deles <xref:System.ServiceModel.Description.MetadataExchangeClientMode> usar, Mex ou http Get.  
  
> [!IMPORTANT]
> Por padrão, o <xref:System.ServiceModel.Description.MetadataExchangeClient> resolve todas as referências para você, incluindo WSDL e importações de esquema XML e inclui o. Você pode desabilitar essa funcionalidade definindo a <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> propriedade como `false` . Você pode controlar o número máximo de referências a serem resolvidas usando a <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> propriedade. Você pode usar essa propriedade em conjunto com a `MaxReceivedMessageSize` Propriedade na associação para controlar a quantidade de metadados recuperados.  
  
### <a name="to-use-metadataexchangeclient-to-obtain-metadata"></a>Para usar o MetadataExchangeClient para obter metadados  
  
1. Crie um novo <xref:System.ServiceModel.Description.MetadataExchangeClient> objeto especificando explicitamente uma associação, um nome de configuração de ponto de extremidade ou o endereço dos metadados.  
  
2. Configure o <xref:System.ServiceModel.Description.MetadataExchangeClient> para atender às suas necessidades. Por exemplo, você pode especificar as credenciais a serem usadas ao solicitar metadados, controlar como as referências de metadados são resolvidas e definir a <xref:System.ServiceModel.Description.MetadataExchangeClient.OperationTimeout%2A> propriedade para controlar quanto tempo a solicitação de metadados deve retornar antes de expirar.  
  
3. Obtenha o <xref:System.ServiceModel.Description.MetadataSet> objeto que contém os metadados recuperados chamando um dos <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> métodos. Observe que você só poderá usar a <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> sobrecarga que não utilize nenhum argumento se você especificou explicitamente um endereço ao construir o <xref:System.ServiceModel.Description.MetadataExchangeClient> .  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir mostra como usar o <xref:System.ServiceModel.Description.MetadataExchangeClient> para baixar e enumerar arquivos de metadados.  

 [!code-csharp[MetadataResolver#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/metadataresolver/cs/client.cs#3)]  

## <a name="compiling-the-code"></a>Compilando o código  

 Para compilar este exemplo de código, você deve referenciar o assembly System.ServiceModel.dll e importar o <xref:System.ServiceModel.Description> namespace.  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.MetadataResolver>
- <xref:System.ServiceModel.Description.MetadataExchangeClient>
- <xref:System.ServiceModel.Description.WsdlImporter>
