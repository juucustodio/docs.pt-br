---
description: 'Saiba mais sobre: provedores de serviços de dados (WCF Data Services)'
title: Provedores de serviços de dados (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: a0160b1b-3d9c-4cc8-8391-cb0986a60a41
ms.openlocfilehash: ee28604b7e3e9e1558a7d80838b072b236572893
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766108"
---
# <a name="data-services-providers-wcf-data-services"></a>Provedores de serviços de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

O WCF Data Services dá suporte a vários modelos de provedor para expor dados como um feed Protocolo Open Data (OData). Este tópico fornece informações para permitir que você selecione o melhor provedor de WCF Data Services para sua fonte de dados.  
  
## <a name="data-source-providers"></a>Provedores de fontes de dados  

 O WCF Data Services dá suporte aos provedores a seguir para definir o modelo de dados de um serviço de dados.  
  
|Provedor|Descrição|  
|--------------|-----------------|  
|Provedor de Entity Framework|Este provedor usa o ADO.NET Entity Framework para permitir que você use dados relacionais com um serviço de dados definindo um modelo de dados que é mapeado para dados relacionais. Sua fonte de dados pode ser o SQL Server ou qualquer outra fonte de dados com suporte a provedores de terceiros para o Entity Framework. Você deverá usar o provedor de Entity Framework quando tiver uma fonte de dados relacional, como um banco de dados do SQL Server. Para obter mais informações, consulte [provedor de Entity Framework](entity-framework-provider-wcf-data-services.md).|  
|Provedor de reflexão|Este provedor usa a reflexão para permitir que você defina um modelo de dados com base em classes de dados existentes que podem ser expostas como instâncias da interface <xref:System.Linq.IQueryable%601>. As atualizações são habilitadas com a implementação da interface <xref:System.Data.Services.IUpdatable>. Você deve usar esse provedor quando tem classes de dados estáticas que são definidas em runtime, como aquelas geradas pelo LINQ to SQL ou definidas por um DataSet tipado. Para obter mais informações, consulte [provedor de reflexão](reflection-provider-wcf-data-services.md).|  
|Provedores de serviços de dados personalizados|WCF Data Services inclui um conjunto de provedores que permitem que você defina dinamicamente um modelo de dados com base em tipos de dados de associação tardia. Você deve implementar essas interfaces quando os dados que estão sendo expostos não são conhecidos quando o aplicativo é criado ou quando os provedores de Entity Framework ou reflexão não são suficientes. Para obter mais informações, consulte [provedores de serviço de dados personalizados](custom-data-service-providers-wcf-data-services.md).|  
  
## <a name="other-data-service-providers"></a>Outros provedores de serviços de dados  

 O WCF Data Services tem o seguinte provedor de serviços de dados adicional que aprimora o desempenho de uma fonte de dados definida usando um dos outros provedores.  
  
|Provedor|Descrição|  
|--------------|-----------------|  
|Provedor de streaming|Esse provedor permite expor tipos de dados de objeto binário grande usando WCF Data Services. Um provedor de streaming é criado com a implementação da interface <xref:System.Data.Services.Providers.IDataServiceStreamProvider>. Este provedor pode ser implementado junto com qualquer provedor de fonte de dados. Para obter mais informações, consulte [streaming Provider](streaming-provider-wcf-data-services.md).|  
  
## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Configurar o serviço de dados](configuring-the-data-service-wcf-data-services.md)
- [Hospedar o serviço de dados](hosting-the-data-service-wcf-data-services.md)
