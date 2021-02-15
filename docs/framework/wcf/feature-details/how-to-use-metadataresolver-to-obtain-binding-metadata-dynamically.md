---
description: 'Saiba mais sobre: como usar o MetadataResolver para obter metadados de associação dinamicamente'
title: 'Como: usar MetadataResolver para obter metadados de associação dinamicamente'
ms.date: 03/30/2017
ms.assetid: 56ffcb99-fff0-4479-aca0-e3909009f605
ms.openlocfilehash: 00f33b31504ede6868113040ba83b6f9462ee808
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734276"
---
# <a name="how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically"></a>Como: usar MetadataResolver para obter metadados de associação dinamicamente

Este tópico mostra como usar a <xref:System.ServiceModel.Description.MetadataResolver> classe para obter metadados de associação dinamicamente.  
  
### <a name="to-dynamically-obtain-binding-metadata"></a>Para obter metadados de associação dinamicamente  
  
1. Crie um <xref:System.ServiceModel.EndpointAddress> objeto com o endereço do ponto de extremidade de metadados.  
  
    ```csharp
    EndpointAddress metaAddress  
      = new EndpointAddress(new Uri("http://localhost:8080/SampleService/mex"));  
    ```  
  
2. Chamada <xref:System.ServiceModel.Description.MetadataResolver.Resolve%28System.Type%2CSystem.ServiceModel.EndpointAddress%29> , que passa o tipo de serviço e o endereço do ponto de extremidade de metadados. Isso retorna uma coleção de pontos de extremidade que implementam o contrato especificado. Somente informações de associação são importadas dos metadados; as informações de contrato não são importadas. O contrato fornecido é usado em seu lugar.  
  
    ```csharp  
    ServiceEndpointCollection endpoints = MetadataResolver.Resolve(typeof(SampleServiceClient),metaAddress);  
    ```  
  
3. Em seguida, você pode iterar pela coleção de pontos de extremidade de serviço para extrair as informações de associação necessárias. O código a seguir itera nos pontos de extremidade, cria um objeto de cliente de serviço que passa a associação e o endereço associado ao ponto de extremidade atual e, em seguida, chama um método no serviço.  
  
    ```csharp  
    foreach (ServiceEndpoint point in endpoints)  
    {  
       if (point != null)  
       {  
          // Create a new wcfClient using retrieved endpoints.  
          using (wcfClient = new SampleServiceClient(point.Binding, point.Address))  
          {  
             Console.WriteLine(  
               wcfClient.SampleMethod("Client used the "  
               + point.Address.ToString() + " address."));  
          }  
      }  
    }  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Metadados](metadata.md)
