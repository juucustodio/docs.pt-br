---
description: 'Saiba mais sobre: carregamento de conteúdo adiado (WCF Data Services)'
title: Carregando conteúdo adiado (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: 32f9b588-c832-44c4-a7e0-fcce635df59a
ms.openlocfilehash: e14796ba003cbad721160ed4a0e2be3e8d148660
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764912"
---
# <a name="loading-deferred-content-wcf-data-services"></a>Carregando conteúdo adiado (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Por padrão, WCF Data Services limita a quantidade de dados retornada por uma consulta. No entanto, você pode carregar dados adicionais explicitamente, incluindo entidades relacionadas, dados de resposta paginados e fluxos de dados binários, do serviço de dados quando necessário. Este tópico descreve como carregar esse conteúdo adiado em seu aplicativo.  
  
## <a name="related-entities"></a>Entidades relacionadas  

 Quando você executa uma consulta, somente as entidades no conjunto de entidades endereçadas são retornadas. Por exemplo, quando uma consulta no serviço de dados Northwind retorna `Customers` entidades, por padrão as `Orders` entidades relacionadas não são retornadas, mesmo que haja uma relação entre `Customers` e `Orders` . Além disso, quando a paginação está habilitada no serviço de dados, você deve carregar explicitamente as páginas de dados subsequentes do serviço. Há duas maneiras de carregar entidades relacionadas:  
  
- **Carregamento adiantado**: você pode usar a `$expand` opção de consulta para solicitar que a consulta retorne entidades relacionadas por uma associação ao conjunto de entidades que a consulta solicitou. Use o <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> método no <xref:System.Data.Services.Client.DataServiceQuery%601> para adicionar a `$expand` opção à consulta que é enviada para o serviço de dados. Você pode solicitar vários conjuntos de entidades relacionadas separando-os por uma vírgula, como no exemplo a seguir. Todas as entidades solicitadas pela consulta são retornadas em uma única resposta. O exemplo a seguir retorna `Order_Details` e `Customers` junto com o `Orders` conjunto de entidades:  
  
     [!code-csharp[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#expandorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#expandorderdetailsspecific)]  
  
     WCF Data Services limita-se a 12 o número de conjuntos de entidades que podem ser incluídos em uma única consulta usando a `$expand` opção de consulta.  
  
- **Carregamento explícito**: você pode chamar o <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> método na <xref:System.Data.Services.Client.DataServiceContext> instância para carregar explicitamente entidades relacionadas. Cada chamada para o <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> método cria uma solicitação separada para o serviço de dados. O exemplo a seguir é carregado explicitamente `Order_Details` para uma `Orders` entidade:  
  
     [!code-csharp[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadrelatedorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadrelatedorderdetailsspecific)]  
  
 Quando você considera qual opção usar, perceba que há uma compensação entre o número de solicitações para o serviço de dados e a quantidade de dados retornados em uma única resposta. Use o carregamento adiantado quando seu aplicativo exigir objetos associados e você quiser evitar a latência adicional de solicitações adicionais para recuperá-las explicitamente. No entanto, se houver casos em que o aplicativo precisa apenas dos dados para instâncias de entidade relacionadas específicas, você deverá considerar carregar explicitamente essas entidades chamando o <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> método. Para obter mais informações, consulte [como carregar entidades relacionadas](how-to-load-related-entities-wcf-data-services.md).  
  
## <a name="paged-content"></a>Conteúdo paginado  

 Quando a paginação está habilitada no serviço de dados, o número de entradas no feed que o serviço de dados retorna é limitado pela configuração do serviço de dados. Os limites de página podem ser definidos separadamente para cada conjunto de entidades. Para obter mais informações, consulte [Configurando o serviço de dados](configuring-the-data-service-wcf-data-services.md). Quando a paginação está habilitada, a entrada final no feed contém um link para a próxima página de dados. Esse link está contido em um <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> objeto. Você Obtém o URI para a próxima página de dados chamando o <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> método no <xref:System.Data.Services.Client.QueryOperationResponse%601> retornado quando o <xref:System.Data.Services.Client.DataServiceQuery%601> é executado. O <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> objeto retornado é usado para carregar a próxima página de resultados. Você deve enumerar o resultado da consulta antes de chamar o <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> método. Considere usar um `do…while` loop para primeiro enumerar o resultado da consulta e, em seguida, verificar um `non-null` valor de próximo link. Quando o <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> método retorna `null` ( `Nothing` em Visual Basic), não há nenhuma página de resultado adicional para a consulta original. O exemplo a seguir mostra um `do…while` loop que carrega dados de cliente paginados do serviço de dados de exemplo Northwind.  
  
 [!code-csharp[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadnextlink)]
 [!code-vb[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadnextlink)]  
  
 Quando uma consulta solicita que as entidades relacionadas sejam retornadas em uma única resposta junto com o conjunto de entidades solicitado, os limites de paginação podem afetar os feeds aninhados que são incluídos embutidos com a resposta. Por exemplo, quando um limite de paginação é definido no serviço de dados de exemplo Northwind para o `Customers` conjunto de entidades, um limite de paginação independente também pode ser definido para o `Orders` conjunto de entidades relacionadas, como no exemplo a seguir do arquivo Northwind.svc.cs que define o serviço de dados de exemplo Northwind.  
  
 [!code-csharp[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigpaging)]
 [!code-vb[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigpaging)]  
  
 Nesse caso, você deve implementar a paginação para os feeds de entidade de nível superior `Customers` e aninhado `Orders` . O exemplo a seguir mostra o `while` loop usado para carregar páginas de `Orders` entidades relacionadas a uma `Customers` entidade selecionada.  
  
 [!code-csharp[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadnextorderslink)]
 [!code-vb[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadnextorderslink)]  
  
 Para obter mais informações, consulte [como carregar resultados paginados](how-to-load-paged-results-wcf-data-services.md).  
  
## <a name="binary-data-streams"></a>Fluxos de dados binários  

 WCF Data Services permite que você acesse dados BLOB (objeto binário grande) como um fluxo de dados. O streaming adia o carregamento de dados binários até que seja necessário, e o cliente pode processar esses dados com mais eficiência. Para aproveitar essa funcionalidade, o serviço de dados deve implementar o <xref:System.Data.Services.Providers.IDataServiceStreamProvider> provedor. Para obter mais informações, consulte [streaming Provider](streaming-provider-wcf-data-services.md). Quando o streaming está habilitado, os tipos de entidade são retornados sem os dados binários relacionados. Nesse caso, você deve usar o <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> método da <xref:System.Data.Services.Client.DataServiceContext> classe para acessar o fluxo de dados para os dados binários do serviço. Da mesma forma, use o <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> método para adicionar ou alterar dados binários de uma entidade como um fluxo. Para obter mais informações, consulte [trabalhando com dados binários](working-with-binary-data-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
- [Consultar o serviço de dados](querying-the-data-service-wcf-data-services.md)
