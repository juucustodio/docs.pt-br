---
description: 'Saiba mais sobre: como gravar uma extensão para o ServiceContractGenerator'
title: 'Como: escrever uma extensão para o ServiceContractGenerator'
ms.date: 03/30/2017
ms.assetid: 876ca823-bd16-4bdf-9e0f-02092df90e51
ms.openlocfilehash: 29d6d65cc3f9d29009f72b9a0c81b6cb1f472ac9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644197"
---
# <a name="how-to-write-an-extension-for-the-servicecontractgenerator"></a>Como: escrever uma extensão para o ServiceContractGenerator

Este tópico descreve como gravar uma extensão para o <xref:System.ServiceModel.Description.ServiceContractGenerator> . Isso pode ser feito implementando a <xref:System.ServiceModel.Description.IOperationContractGenerationExtension> interface em um comportamento de operação ou implementando a <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> interface em um comportamento de contrato. Este tópico mostra como implementar a <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> interface em um comportamento de contrato.  
  
 O <xref:System.ServiceModel.Description.ServiceContractGenerator> gera contratos de serviço, tipos de cliente e configurações de cliente de <xref:System.ServiceModel.Description.ServiceEndpoint> <xref:System.ServiceModel.Description.ContractDescription> instâncias, e <xref:System.ServiceModel.Channels.Binding> . Normalmente, você importa <xref:System.ServiceModel.Description.ServiceEndpoint> , <xref:System.ServiceModel.Description.ContractDescription> e <xref:System.ServiceModel.Channels.Binding> instâncias de metadados de serviço e, em seguida, usa essas instâncias para gerar código para chamar o serviço. Neste exemplo, uma <xref:System.ServiceModel.Description.IWsdlImportExtension> implementação é usada para processar anotações WSDL e, em seguida, adicionar extensões de geração de código aos contratos importados para gerar comentários sobre o código gerado.  
  
### <a name="to-write-an-extension-for-the-servicecontractgenerator"></a>Para gravar uma extensão para o ServiceContractGenerator  
  
1. Implementar <xref:System.ServiceModel.Description.IServiceContractGenerationExtension>. Para modificar o contrato de serviço gerado, use a <xref:System.ServiceModel.Description.ServiceContractGenerationContext> instância passada para o <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> método.  
  
    ```csharp
    public void GenerateContract(ServiceContractGenerationContext context)  
    {  
        Console.WriteLine("In generate contract.");  
        context.ContractType.Comments.AddRange(Formatter.FormatComments(commentText));  
    }  
    ```  
  
2. Implemente <xref:System.ServiceModel.Description.IWsdlImportExtension> na mesma classe. O <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> método pode processar uma extensão WSDL específica (neste caso, anotações WSDL) adicionando uma extensão de geração de código à instância importada <xref:System.ServiceModel.Description.ContractDescription> .  
  
    ```csharp
    public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)
    {
        // Contract documentation
        if (context.WsdlPortType.Documentation != null)
        {
            context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));
        }
        // Operation documentation
        foreach (Operation operation in context.WsdlPortType.Operations)
        {
            if (operation.Documentation != null)
            {
                OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);
                if (operationDescription != null)
                {
                    operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));
                }
            }
        }
    }
    public void BeforeImport(ServiceDescriptionCollection wsdlDocuments, XmlSchemaSet xmlSchemas, ICollection<XmlElement> policy)
    {
        Console.WriteLine("BeforeImport called.");
    }

    public void ImportEndpoint(WsdlImporter importer, WsdlEndpointConversionContext context)
    {
        Console.WriteLine("ImportEndpoint called.");
    }
    ```  
  
3. Adicione o importador WSDL à sua configuração de cliente.  
  
    ```xml  
    <metadata>  
      <wsdlImporters>  
        <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
      </wsdlImporters>  
    </metadata>  
    ```  
  
4. No código do cliente, crie uma `MetadataExchangeClient` chamada e `GetMetadata` .  
  
    ```csharp
    var mexClient = new MetadataExchangeClient(metadataAddress);  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet metaDocs = mexClient.GetMetadata();  
    ```  
  
5. Crie uma `WsdlImporter` chamada e `ImportAllContracts` .  
  
    ```csharp
    var importer = new WsdlImporter(metaDocs);
    System.Collections.ObjectModel.Collection<ContractDescription> contracts = importer.ImportAllContracts();  
    ```  
  
6. Criar um `ServiceContractGenerator` e chamar `GenerateServiceContractType` para cada contrato.  
  
    ```csharp
    var generator = new ServiceContractGenerator();  
    foreach (ContractDescription contract in contracts)  
    {  
       generator.GenerateServiceContractType(contract);  
    }  
    if (generator.Errors.Count != 0)  
       throw new Exception("There were errors during code compilation.");  
    ```  
  
7. <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> é chamado automaticamente para cada comportamento de contrato em um determinado contrato que implementa <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> . Esse método pode, então, modificar o <xref:System.ServiceModel.Description.ServiceContractGenerationContext> passado. Neste exemplo, comentários são adicionados.  
  
## <a name="see-also"></a>Consulte também

- [Metadados](../feature-details/metadata.md)
- [Como: importar o WSDL personalizado](how-to-import-custom-wsdl.md)
