---
description: 'Saiba mais sobre: como importar WSDL personalizado'
title: 'Como: importar o WSDL personalizado'
ms.date: 03/30/2017
ms.assetid: ddc3718d-ce60-44f6-92af-a5c67477dd99
ms.openlocfilehash: f21e5cace532bd6d20d409f297480f65bb23cbf4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780733"
---
# <a name="how-to-import-custom-wsdl"></a>Como: importar o WSDL personalizado

Este tópico descreve como importar o WSDL personalizado. Para lidar com o WSDL personalizado, você deve implementar a <xref:System.ServiceModel.Description.IWsdlImportExtension> interface.  
  
### <a name="to-import-custom-wsdl"></a>Para importar o WSDL personalizado  
  
1. Implementar <xref:System.ServiceModel.Description.IWsdlImportExtension>. Implemente o <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%28System.Web.Services.Description.ServiceDescriptionCollection%2CSystem.Xml.Schema.XmlSchemaSet%2CSystem.Collections.Generic.ICollection%7BSystem.Xml.XmlElement%7D%29> método para modificar os metadados antes que eles sejam importados. Implemente <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> os <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> métodos e para modificar os contratos e pontos de extremidade importados dos metadados. Para acessar o contrato ou ponto de extremidade importado, use o objeto de contexto correspondente ( <xref:System.ServiceModel.Description.WsdlContractConversionContext> ou <xref:System.ServiceModel.Description.WsdlEndpointConversionContext> ):  
  
    ```csharp
    public class WsdlDocumentationImporter : IWsdlImportExtension
    {
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
    }
    ```
  
2. Configure o aplicativo cliente para usar o importador WSDL personalizado. Observe que, se você estiver usando Svcutil.exe, deverá adicionar essa configuração ao arquivo de configuração para Svcutil.exe (Svcutil.exe.config):  
  
    ```xml  
    <system.serviceModel>  
          <client>  
            <endpoint
              address="http://localhost:8000/Fibonacci"
              binding="wsHttpBinding"  
              contract="IFibonacci"  
            />  
            <metadata>  
              <wsdlImporters>  
                <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
              </wsdlImporters>  
            </metadata>  
          </client>  
        </system.serviceModel>  
    ```  
  
3. Crie uma nova <xref:System.ServiceModel.Description.WsdlImporter> instância (passando a <xref:System.ServiceModel.Description.MetadataSet> instância que contém os documentos WSDL que você deseja importar) e chame <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A> :  
  
    ```csharp
    WsdlImporter importer = new WsdlImporter(metaDocs);
    System.Collections.ObjectModel.Collection<ContractDescription> contracts = importer.ImportAllContracts();  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Metadados](../feature-details/metadata.md)
- [Exportando e importando metadados](../feature-details/exporting-and-importing-metadata.md)
- [Publicação personalizada de WSDL](../samples/custom-wsdl-publication.md)
