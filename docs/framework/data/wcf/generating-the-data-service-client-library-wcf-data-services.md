---
description: 'Saiba mais sobre: gerando a biblioteca de cliente do serviço de dados (WCF Data Services)'
title: Gerando a biblioteca do cliente de serviço de dados (serviços de dados WCF)
ms.date: 03/30/2017
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- Add Service Reference dialog box
ms.assetid: 314077c1-ac10-47e1-bed4-940b5462359d
ms.openlocfilehash: 3bac2459044ff910c8085ff56e60d9da6e0ba877
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765926"
---
# <a name="generating-the-data-service-client-library-wcf-data-services"></a>Gerando a biblioteca do cliente de serviço de dados (serviços de dados WCF)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Um serviço de dados que implementa o Protocolo Open Data (OData) pode retornar um documento de metadados de serviço que descreve o modelo de dados exposto pelo feed OData. Para obter mais informações, consulte a seção documento de metadados de serviço no artigo [OData: Overview](https://www.odata.org/documentation/odata-version-2-0/overview/) . Você pode usar a caixa de diálogo **Adicionar referência de serviço** no Visual Studio para adicionar uma referência a um serviço baseado em OData. Quando você usa essa ferramenta para adicionar uma referência aos metadados retornados por um feed OData em um projeto cliente, ele executa as seguintes ações:  
  
- Solicita o documento de metadados de serviço do serviço de dados e interpreta os metadados retornados.  
  
    > [!NOTE]
    > Os metadados retornados são armazenados no projeto do cliente como um arquivo. edmx. Este arquivo .edmx não pode ser aberto usando o Designer de Modelo de Dados de Entidade porque não tem o mesmo formato que um arquivo .edmx usado pelo Entity Framework. Você pode exibir esse arquivo de metadados usando o Editor de XML ou qualquer outro editor de texto. Para obter mais informações, consulte [ \[ MC-EDMX \] : modelo de dados de entidade para o formato de empacotamento de serviços de dados](/openspecs/windows_protocols/mc-edmx/5dff5e25-56a1-408b-9d44-bff6634c7d16).
  
- Gera uma representação do serviço como uma classe do contêiner de entidade que herda de <xref:System.Data.Services.Client.DataServiceContext>. Essa classe do contêiner de entidade gerada parece o contêiner de entidade que as ferramentas de Modelo de Dados de Entidade geram. Para obter mais informações, consulte [Visão geral dos serviços de objeto (Entity Framework)](/previous-versions/bb386871(v=vs.100)).  
  
- Gera classes de dados para os tipos de modelo de dados que ela descobre nos metadados de serviço.  
  
- Adiciona uma referência ao assembly do `System.Data.Services.Client` ao projeto.  
  
 Para obter mais informações, consulte [como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md).  
  
 As classes de serviço de dados do cliente também podem ser geradas usando a ferramenta [DataSvcUtil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) no prompt de comando. Para obter mais informações, consulte [como: gerar manualmente classes de serviço de dados do cliente](how-to-manually-generate-client-data-service-classes-wcf-data-services.md).  
  
## <a name="client-data-type-mapping"></a>Mapeamento de tipo de dados de cliente  

 Quando você usa a caixa de diálogo **Adicionar referência de serviço** no Visual Studio ou a `DataSvcUtil.exe` ferramenta para gerar classes de dados de cliente baseadas em um feed OData, os tipos de dados .NET Framework são mapeados para os tipos primitivos do modelo de dados da seguinte maneira:  
  
|Tipo do modelo de dados|Tipo de dados do .NET Framework|  
|---------------------|------------------------------|  
|`Edm.Binary`|<xref:System.Byte> `[]`|  
|`Edm.Boolean`|<xref:System.Boolean>|  
|`Edm.Byte`|<xref:System.Byte>|  
|`Edm.DateTime`|<xref:System.DateTime>|  
|`Edm.Decimal`|<xref:System.Decimal>|  
|`Edm.Double`|<xref:System.Double>|  
|`Edm.Guid`|<xref:System.Guid>|  
|`Edm.Int16`|<xref:System.Int16>|  
|`Edm.Int32`|<xref:System.Int32>|  
|`Edm.Int64`|<xref:System.Int64>|  
|`Edm.SByte`|<xref:System.SByte>|  
|`Edm.Single`|<xref:System.Single>|  
|`Edm.String`|<xref:System.String>|  
  
 Para obter mais informações, consulte a seção tipos de dados primitivos no artigo [OData: Overview](https://www.odata.org/documentation/odata-version-2-0/overview/) .
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
- [Início rápido](quickstart-wcf-data-services.md)
