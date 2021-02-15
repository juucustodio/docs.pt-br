---
description: 'Saiba mais sobre: como importar declarações de política personalizada'
title: 'Como: importar declarações de política personalizadas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f41d787-accb-4a10-bfc6-a807671d1581
ms.openlocfilehash: e9190a97ed7d2d369b8f9ddc3d7fec71daf1e54f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644327"
---
# <a name="how-to-import-custom-policy-assertions"></a>Como: importar declarações de política personalizadas

As declarações de política descrevem os recursos e os requisitos de um ponto de extremidade de serviço.  Os aplicativos cliente podem usar declarações de política em metadados de serviço para configurar a associação de cliente ou para personalizar o contrato de serviço para um ponto de extremidade de serviço.  
  
 As declarações de política personalizada são importadas implementando a <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> interface e passando esse objeto para o sistema de metadados ou registrando o tipo de implementação em seu arquivo de configuração de aplicativo.  As implementações da <xref:System.ServiceModel.Description.IPolicyImportExtension> interface devem fornecer um construtor sem parâmetros.  
  
### <a name="to-import-custom-policy-assertions"></a>Para importar declarações de política personalizada  
  
1. Implemente a <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> interface em uma classe. Consulte os procedimentos a seguir.  
  
2. Insira o importador de política personalizada por:  
  
3. Usando um arquivo de configuração. Consulte os procedimentos a seguir.  
  
4. Usando um arquivo de configuração com a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md). Consulte os procedimentos a seguir.  
  
5. Inserindo programaticamente o importador de política. Consulte os procedimentos a seguir.  
  
### <a name="to-implement-the-systemservicemodeldescriptionipolicyimportextension-interface-on-any-class"></a>Para implementar a interface System. ServiceModel. Description. IPolicyImportExtension em qualquer classe  
  
1. No <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType> método, para cada assunto da política sobre a qual você está interessado, localize as declarações de política que deseja importar chamando o método apropriado (dependendo do escopo da declaração que você deseja) no <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType> objeto passado para o método. O exemplo de código a seguir mostra como usar o <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType> método para localizar a declaração de política personalizada e removê-la da coleção em uma única etapa. Se você usar o método remove para localizar e remover a asserção, não será necessário executar a etapa 4.  
  
     [!code-csharp[CustomPolicySample#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyimporter.cs#9)]
     [!code-vb[CustomPolicySample#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyimporter.vb#9)]  
  
2. Processar as declarações de política. Observe que o sistema de política não normaliza políticas aninhadas e `wsp:optional` . Você deve processar essas construções em sua implementação de extensão de importação de política.  
  
3. Execute a personalização para a associação ou contrato que dá suporte à capacidade ou ao requisito especificado pela declaração de política. Normalmente, as declarações indicam que uma associação requer uma configuração específica ou um elemento de ligação específico. Faça essas modificações acessando a <xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A?displayProperty=nameWithType> propriedade. Outras asserções exigem que você modifique o contrato.  Você pode acessar e modificar o contrato usando a <xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A?displayProperty=nameWithType> propriedade.  Observe que o importador de política pode ser chamado várias vezes para a mesma associação e contrato, mas alternativas de política diferentes se a importação de uma alternativa de política falhar. Seu código deve ser resiliente a esse comportamento.  
  
4. Remova a declaração de política personalizada da coleção de asserção. Se você não remover o Windows Communication Foundation de asserção (WCF) supõe que a importação de política não foi bem-sucedida e não importará a associação associada. Se você usou o <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType> método para localizar a declaração de política personalizada e removê-la da coleção em uma única etapa, não será necessário executar essa etapa.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-a-configuration-file"></a>Para inserir o importador de política personalizada no sistema de metadados usando um arquivo de configuração  
  
1. Adicione o tipo de importador ao `<extensions>` elemento dentro do [\<policyImporters>](../../configure-apps/file-schema/wcf/policyimporters.md) elemento no arquivo de configuração do cliente.  
  
     [!code-xml[CustomPolicySample#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.exe.config#7)]
  
2. No aplicativo cliente, use o <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType> ou o <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> para resolver os metadados e o importador é invocado automaticamente.  
  
     [!code-csharp[CustomPolicySample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.cs#10)]
     [!code-vb[CustomPolicySample#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.vb#10)]  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-svcutilexe"></a>Para inserir o importador de política personalizada no sistema de metadados usando Svcutil.exe  
  
1. Adicione o tipo de importador ao `<extensions>` elemento dentro do [\<policyImporters>](../../configure-apps/file-schema/wcf/policyimporters.md) elemento no arquivo de configuração Svcutil.exe.config. Você também pode apontar Svcutil.exe para carregar os tipos de importador de política registrados em um arquivo de configuração diferente usando a `/svcutilConfig` opção.  
  
2. Use a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) para importar os metadados e o importador é invocado automaticamente.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-programmatically"></a>Para inserir o importador de política personalizada no sistema de metadados de forma programática  
  
1. Adicione o importador à <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A?displayProperty=nameWithType> Propriedade (por exemplo, se você estiver usando o <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> ) antes de importar os metadados.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>
- [Estendendo o sistema de metadados](extending-the-metadata-system.md)
