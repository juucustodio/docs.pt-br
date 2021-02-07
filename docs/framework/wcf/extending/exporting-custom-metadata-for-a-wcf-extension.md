---
description: 'Saiba mais sobre: exportando metadados personalizados para uma extensão WCF'
title: Exportando metadados personalizados para uma extensão do WCF
ms.date: 03/30/2017
ms.assetid: 53c93882-f8ba-4192-965b-787b5e3f09c0
ms.openlocfilehash: 5803dd7d2e03f9597ecac34bf38641656a9077b8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685784"
---
# <a name="exporting-custom-metadata-for-a-wcf-extension"></a>Exportando metadados personalizados para uma extensão do WCF

No Windows Communication Foundation (WCF), a exportação de metadados é o processo de descrever os pontos de extremidade de serviço e projetar-los em uma representação paralela e padronizada que os clientes podem usar para entender como usar o serviço. Metadados personalizados consistem em elementos XML que os exportadores de metadados fornecidos pelo sistema não podem exportar. Normalmente, isso inclui elementos WSDL personalizados para comportamentos definidos pelo usuário e elementos de ligação e declarações de política sobre os recursos e requisitos de associações e contratos.  
  
 Esta seção descreve como exportar declarações WSDL ou de política personalizadas e não se concentra no processo de exportação em si. Para obter mais informações sobre como usar os tipos que exportam e importam metadados independentemente de os metadados terem sido personalizados ou construídos pelo sistema, consulte [exportando e importando metadados](../feature-details/exporting-and-importing-metadata.md).  
  
## <a name="overview"></a>Visão geral  

 Quando os metadados são publicados usando o <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> , o <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> é examinado e XSD e o WSDL, incluindo as asserções de política, são gerados para todos os contratos e associações que o WCF pode dar suporte usando atributos e associações fornecidos pelo sistema. No entanto, os atributos de comportamento personalizado ou os elementos de ligação exigem suporte antes que possam ser exportados corretamente.  
  
 Esta seção descreve:  
  
1. Como implementar e usar a <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> interface, que expõe os dados de geração WSDL para você antes de publicar o WSDL.  
  
2. Como implementar e usar a <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> interface, que expõe os dados de política para você antes de exportar as declarações de política em dados WSDL.  
  
 Para obter mais informações sobre como importar declarações personalizadas de WSDL e de política, consulte [importando metadados personalizados para uma extensão WCF](importing-custom-metadata-for-a-wcf-extension.md).  
  
## <a name="exporting-custom-wsdl-elements"></a>Exportando elementos WSDL personalizados  

 Implemente o <xref:System.ServiceModel.Description.IWsdlExportExtension> em um comportamento de operação, comportamento de contrato, comportamento de ponto de extremidade ou elemento de associação ( <xref:System.ServiceModel.Description.IOperationBehavior> , <xref:System.ServiceModel.Description.IContractBehavior> , <xref:System.ServiceModel.Description.IEndpointBehavior> ou <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> respectivamente) e insira os comportamentos ou elementos de associação na descrição do serviço que você está tentando exportar. (Para obter mais informações sobre como inserir comportamentos, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md)). O <xref:System.ServiceModel.Description.IWsdlExportExtension> será chamado para cada ponto de extremidade e cada ponto de extremidade exportará o contrato primeiro se ele ainda não tiver sido exportado. Você pode participar de um processo de exportação, dependendo das suas necessidades:  
  
- Use o <xref:System.ServiceModel.Description.WsdlContractConversionContext> para modificar os metadados exportados no <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A> método.  
  
- Use o <xref:System.ServiceModel.Description.WsdlEndpointConversionContext> para modificar os metadados exportados para o ponto de extremidade no <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> método.  
  
 O <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A> método é chamado em todas as <xref:System.ServiceModel.Description.IWsdlExportExtension> implementações na <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType> instância que está sendo exportada.  O <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> método é chamado em todas as <xref:System.ServiceModel.Description.IWsdlExportExtension> implementações com a <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> instância que está sendo exportada.  
  
 Para obter mais informações, consulte [como: exportar WSDL personalizado](how-to-export-custom-wsdl.md) e a [publicação de WSDL personalizada](../samples/custom-wsdl-publication.md)de exemplo.  
  
## <a name="exporting-custom-policy-assertions"></a>Exportando declarações de política personalizada  

 Implemente o <xref:System.ServiceModel.Description.IPolicyExportExtension> em a <xref:System.ServiceModel.Channels.BindingElement> e adicione o elemento Binding à associação para escrever declarações de política personalizada sobre suporte de associação e recursos de contrato no WSDL. O <xref:System.ServiceModel.Description.IPolicyExportExtension> é chamado uma vez ao exportar o elemento de associação implementado em uma associação e passa o <xref:System.ServiceModel.Description.PolicyConversionContext> para o <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A> método. Você pode usar os métodos na <xref:System.ServiceModel.Description.PolicyConversionContext> instância para adicionar às declarações de política anexadas à associação WSDL na mensagem, na operação ou nos assuntos do ponto de extremidade.  
  
 Para obter mais informações, consulte [como: exportar declarações de política personalizada](how-to-export-custom-policy-assertions.md).  
  
## <a name="see-also"></a>Consulte também

- [Como: exportar o WSDL personalizado](how-to-export-custom-wsdl.md)
- [Como: exportar declarações de política personalizadas](how-to-export-custom-policy-assertions.md)
- [Importando metadados personalizados para uma extensão do WCF](importing-custom-metadata-for-a-wcf-extension.md)
