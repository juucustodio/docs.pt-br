---
description: 'Saiba mais sobre: expor seus dados como um serviço (WCF Data Services)'
title: Expondo seus dados como um serviço (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- getting started, WCF Data Services
- WCF Data Services, getting started
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
ms.openlocfilehash: 496cf18b264672814295916467e1bff93feebdde
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765965"
---
# <a name="expose-your-data-as-a-service-wcf-data-services"></a>Expor seus dados como um serviço (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

O WCF Data Services se integra ao Visual Studio para permitir que você defina mais facilmente os serviços para expor seus dados como feeds Protocolo Open Data (OData). A criação de um serviço de dados que expõe um feed OData envolve as seguintes etapas básicas:

1. **Defina o modelo de dados.** WCF Data Services nativamente dá suporte a modelos de dados baseados no [Entity Framework ADO.net](../adonet/ef/index.md). Para obter mais informações, consulte [como criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework](create-a-data-service-using-an-adonet-ef-data-wcf.md).

     O WCF Data Services também dá suporte a modelos de dados baseados em objetos Common Language Runtime (CLR) que retornam uma instância da <xref:System.Linq.IQueryable%601> interface. Isso permite que você implante serviços de dados baseados em listas, matrizes e coleções no .NET Framework. Para habilitar operações de criação, atualização e exclusão nessas estruturas de dados, você também deve implementar a <xref:System.Data.Services.IUpdatable> interface. Para obter mais informações, consulte [como: criar um serviço de dados usando o provedor de reflexão](create-a-data-service-using-rp-wcf-data-services.md).

     Para cenários mais avançados, WCF Data Services inclui um conjunto de provedores que permitem que você defina um modelo de dados com base em tipos de dados de associação tardia. Para obter mais informações, consulte [provedores de serviço de dados personalizados](custom-data-service-providers-wcf-data-services.md).

2. **Crie o serviço de dados.** O serviço de dados mais básico expõe uma classe herdada da classe <xref:System.Data.Services.DataService%601>, com um tipo `T` que é o nome qualificado para namespace do contêiner de entidade. Para obter mais informações, consulte [definindo WCF Data Services](defining-wcf-data-services.md).

3. **Configure o serviço de dados.** Por padrão, WCF Data Services desabilita o acesso a recursos que são expostos por um contêiner de entidade. A <xref:System.Data.Services.DataServiceConfiguration> interface permite que você configure o acesso a recursos e operações de serviço, especifique a versão com suporte do OData e defina outros comportamentos de todo o serviço, como comportamentos de envio em lote ou o número máximo de entidades que podem ser retornadas em uma única resposta. Para obter mais informações, consulte [Configurando o serviço de dados](configuring-the-data-service-wcf-data-services.md).

Para obter um exemplo de como criar um simple Data Service baseado no banco de dados de exemplo Northwind, consulte [início rápido](quickstart-wcf-data-services.md).

## <a name="see-also"></a>Consulte também

- [Introdução](getting-started-with-wcf-data-services.md)
- [Visão geral](wcf-data-services-overview.md)
