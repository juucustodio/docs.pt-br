---
description: 'Saiba mais sobre: Configurando o serviço de dados (WCF Data Services)'
title: Configurando o serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 59efd4c8-cc7a-4800-a0a4-d3f8abe6c55c
ms.openlocfilehash: 72bd0de5319cc4b19fd831f4ee302e073106c74b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766160"
---
# <a name="configuring-the-data-service-wcf-data-services"></a>Configurando o serviço de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode criar serviços de dados que expõem feeds Protocolo Open Data (OData). Os dados nesses feeds podem vir de uma variedade de fontes de dados. WCF Data Services usa provedores de dados para expor esses dados como um feed OData. Esses provedores incluem um provedor de Entity Framework, um provedor de reflexão e um conjunto de interfaces de provedor de serviços de dados personalizados. A implementação do provedor define o modelo de dados para o serviço. Para obter mais informações, consulte [provedores de serviços de dados](data-services-providers-wcf-data-services.md).  
  
 No WCF Data Services, um serviço de dados é uma classe que herda da <xref:System.Data.Services.DataService%601> classe, em que o tipo de serviço de dados é o contêiner de entidade do modelo de dados. Este contêiner de entidade tem uma ou mais propriedades que retornam um <xref:System.Linq.IQueryable%601>, que são usados para acessar conjuntos de entidades no modelo de dados.  
  
 Os comportamentos do serviço de dados são definidos pelos membros da classe <xref:System.Data.Services.DataServiceConfiguration> e por membros da classe <xref:System.Data.Services.DataServiceBehavior>, que é acessada da propriedade <xref:System.Data.Services.DataServiceConfiguration.DataServiceBehavior%2A> da classe <xref:System.Data.Services.DataServiceConfiguration>. A classe <xref:System.Data.Services.DataServiceConfiguration> é fornecida para o método `InitializeService` que é implementado pelo serviço de dados, como na seguinte implementação de um serviço de dados da Northwind:  
  
[!code-csharp[Astoria Northwind Service#DataServiceConfigComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigcomplete)]  
[!code-vb[Astoria Northwind Service#DataServiceConfigComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigcomplete)]  
  
## <a name="data-service-configuration-settings"></a>Parâmetros de configuração do serviço de dados  

 A classe <xref:System.Data.Services.DataServiceConfiguration> permite que você especifique os seguintes comportamentos de serviço de dados:  
  
|Membro|Comportamento|  
|------------|--------------|  
|<xref:System.Data.Services.DataServiceBehavior.AcceptCountRequests%2A>|Permite que você desative as solicitações de contagem que são enviadas para o serviço de dados usando o segmento do caminho `$count` e a opção de consulta `$inlinecount`. Para obter mais informações, consulte [OData: convenções de URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).|  
|<xref:System.Data.Services.DataServiceBehavior.AcceptProjectionRequests%2A>|Permite que você desative o suporte para projeção de dados nas solicitações que são enviadas para o serviço de dados usando a opção de consulta `$select`. Para obter mais informações, consulte [OData: convenções de URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).|  
|<xref:System.Data.Services.DataServiceConfiguration.EnableTypeAccess%2A>|Permite que um tipo de dados seja exposto nos metadados para um provedor dinâmico de metadados definidos usando a interface <xref:System.Data.Services.Providers.IDataServiceMetadataProvider>.|  
|<xref:System.Data.Services.DataServiceConfiguration.EnableTypeConversion%2A>|Permite que você especifique se o runtime do serviço de dados deve converter o tipo que está contido na carga para o tipo da propriedade real que é especificado na solicitação.|  
|<xref:System.Data.Services.DataServiceBehavior.InvokeInterceptorsOnLinkDelete%2A>|Permite que você especifique se os interceptores de alteração registrados são chamados ou não nas entidades relacionadas quando um link de relação entre as duas entidades é excluído.|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxBatchCount%2A>|Permite que você limite o número de conjuntos de alterações e operações de consulta que são permitidos em um único lote. Para obter mais informações, consulte [OData: operações em](https://www.odata.org/documentation/odata-version-2-0/batch-processing/) lote e [em lote](batching-operations-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxChangesetCount%2A>|Permite que você limite o número de alterações que podem ser incluídas em um único conjunto de alteração. Para obter mais informações, consulte [como habilitar a paginação de resultados do serviço de dados](how-to-enable-paging-of-data-service-results-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxExpandCount%2A>|Permite que você limite o tamanho de uma resposta limitando o número de entidades relacionadas que podem ser incluídas em uma única solicitação usando o operador de consulta `$expand`. Para obter mais informações, consulte [OData: convenções de URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/) e [carregamento de conteúdo adiado](loading-deferred-content-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxExpandDepth%2A>|Permite que você limite o tamanho de uma resposta limitando a profundidade do grafo de entidades relacionadas que podem ser incluídas em uma única solicitação usando o operador de consulta `$expand`. Para obter mais informações, consulte [OData: convenções de URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/) e [carregamento de conteúdo adiado](loading-deferred-content-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxObjectCountOnInsert%2A>|Permite que você limite o número de entidades a serem inseridas que podem ser contidas em uma única solicitação POST.|  
|<xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A>|Define a versão do protocolo Atom que é usado pelo serviço de dados. Quando o valor de <xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A> é definido como um valor menor que o valor máximo de <xref:System.Data.Services.Common.DataServiceProtocolVersion> , a funcionalidade mais recente do WCF Data Services não está disponível para clientes que acessam o serviço de dados. Para obter mais informações, consulte [controle de versão do serviço de dados](data-service-versioning-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxResultsPerCollection%2A>|Permite que você limite o tamanho de uma resposta limitando o número de entidades em cada conjunto de entidades que é retornado como um feed de dados.|  
|<xref:System.Data.Services.DataServiceConfiguration.RegisterKnownType%2A>|Adiciona um tipo de dados à lista de tipos que são reconhecidos pelo serviço de dados.|  
|<xref:System.Data.Services.DataServiceConfiguration.SetEntitySetAccessRule%2A>|Define os direitos de acesso para os recursos do conjunto de entidades que estão disponíveis no serviço de dados. Um valor de asterisco (`*`) pode ser fornecido para o parâmetro de nome para definir o acesso para todos os conjuntos de entidades restantes para o mesmo nível. Recomendamos que você defina o acesso para conjuntos de entidades para fornecer acesso de privilégios mínimos para os recursos de serviço de dados que são exigidos por aplicativos cliente. Para obter mais informações, consulte [securing WCF Data Services](securing-wcf-data-services.md). Para obter exemplos dos direitos mínimos de acesso necessários para um determinado URI e uma ação HTTP, consulte a tabela na seção [requisitos mínimos de acesso a recursos](configuring-the-data-service-wcf-data-services.md#accessRequirements) .|  
|<xref:System.Data.Services.DataServiceConfiguration.SetEntitySetPageSize%2A>|Define o tamanho máximo da página para um recurso do conjunto de entidades. Para obter mais informações, consulte [como habilitar a paginação de resultados do serviço de dados](how-to-enable-paging-of-data-service-results-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.SetServiceOperationAccessRule%2A>|Define os direitos de acesso para as operações de serviço que são definidas no serviço de dados. Para obter mais informações, consulte [operações de serviço](service-operations-wcf-data-services.md). Um valor de asterisco (`*`) pode ser fornecido para o parâmetro de nome para definir o acesso para todas as operações de serviços para o mesmo nível. Recomendamos que você defina o acesso para operações de serviço para fornecer acesso de privilégios mínimos para os recursos de serviço de dados que são exigidos por aplicativos cliente. Para obter mais informações, consulte [securing WCF Data Services](securing-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A>|Esta propriedade de configuração permite que você solucione problemas de um serviço de dados mais facilmente retornando mais informações na mensagem de resposta de erro. Esta opção não é destinada a ser usada em um ambiente de produção. Para obter mais informações, consulte [desenvolvendo e Implantando WCF Data Services](developing-and-deploying-wcf-data-services.md).|  
  
<a name="accessRequirements"></a>

## <a name="minimum-resource-access-requirements"></a>Requisitos mínimos de acesso a recursos  

 A tabela a seguir detalha os direitos mínimos do conjunto de entidades que devem ser concedidos para executar uma operação específica. Os exemplos de caminho são baseados no serviço de dados Northwind que é criado quando você conclui o [início rápido](quickstart-wcf-data-services.md). Como as enumerações <xref:System.Data.Services.EntitySetRights> e <xref:System.Data.Services.ServiceOperationRights> são definidas usando o <xref:System.FlagsAttribute>, você pode usar um operador OR lógico para especificar várias permissões para um único conjunto de entidades ou operação. Para obter mais informações, consulte [como habilitar o acesso ao serviço de dados](how-to-enable-access-to-the-data-service-wcf-data-services.md).  
  
|Caminho/ação|`GET`|`DELETE`|`MERGE`|`POST`|`PUT`|  
|------------------|-----------|--------------|-------------|------------|-----------|  
|`/Customers`|<xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|<xref:System.Data.Services.EntitySetRights.WriteAppend>|Sem suporte|  
|`/Customers('ALFKI')`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteDelete>|<xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge>|n/a|<xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge> ou <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> -e-<br /><br /> `Orders``:`e<xref:System.Data.Services.EntitySetRights.WriteAppend>|Sem suporte|  
|`/Customers('ALFKI')/Orders(10643)`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteDelete>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge>|Sem suporte|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Orders(10643)/Customer`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteDelete><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge>;<br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.WriteAppend><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.WriteAppend> e <xref:System.Data.Services.EntitySetRights.ReadSingle>|Sem suporte|  
|`/Customers('ALFKI')/$links/Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge> ou <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|Sem suporte|  
|`/Customers('ALFKI')/$links/Orders(10643)`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge> ou <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|Sem suporte|Sem suporte|Sem suporte|  
|`/Orders(10643)/$links/Customer`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge> ou <xref:System.Data.Services.EntitySetRights.WriteReplace>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteMerge>|Sem suporte|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle>;<br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers/$count`|<xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|Sem suporte|Sem suporte|  
|`/Customers('ALFKI')/ContactName`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|Sem suporte|<xref:System.Data.Services.EntitySetRights.WriteMerge>|Sem suporte|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/Address/StreetAddress/$value` <sup>1</sup>|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.WriteDelete>|Sem suporte|Sem suporte|Sem suporte|  
|`/Customers('ALFKI')/ContactName/$value`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.ReadSingle> e <xref:System.Data.Services.EntitySetRights.WriteDelete>|<xref:System.Data.Services.EntitySetRights.WriteMerge>|Sem suporte|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/$value` <sup>2</sup>|<xref:System.Data.Services.EntitySetRights.ReadSingle>|Sem suporte|Sem suporte|Sem suporte|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers?$select=Orders/*&$expand=Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|`Customers`: <xref:System.Data.Services.EntitySetRights.WriteAppend>|Sem suporte|  
|`/Customers('ALFKI')?$select=Orders/*&$expand=Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> -e-<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Sem suporte|Sem suporte|Sem suporte|Sem suporte|  
  
 <sup>1</sup> neste exemplo, `Address` representa uma propriedade de tipo complexo da `Customers` entidade que tem uma propriedade chamada `StreetAddress` . O modelo usado pelos serviços de dados da Northwind não define explicitamente este tipo complexo. Quando o modelo de dados é definido usando o provedor de Entity Framework, você pode usar as ferramentas de Modelo de Dados de Entidade para definir um tipo complexo. Para obter mais informações, consulte [como: criar e modificar tipos complexos](/previous-versions/dotnet/netframework-4.0/dd456820(v=vs.100)).  
  
 <sup>2</sup> esse URI tem suporte quando uma propriedade que retorna um blob (objeto binário grande) é definida como o recurso de mídia que pertence a uma entidade que é uma entrada de link de mídia, que nesse caso é `Customers` . Para obter mais informações, consulte [streaming Provider](streaming-provider-wcf-data-services.md).  
  
<a name="versioning"></a>

## <a name="versioning-requirements"></a>Requisitos de controle de versão  

 Os seguintes comportamentos de configuração de serviço de dados exigem a versão 2 do protocolo OData ou versões posteriores:  
  
- Suporte para solicitações de contagem.  
  
- Suporte a opção de consulta de $select para a projeção.  
  
 Para obter mais informações, consulte [controle de versão do serviço de dados](data-service-versioning-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Hospedar o serviço de dados](hosting-the-data-service-wcf-data-services.md)
