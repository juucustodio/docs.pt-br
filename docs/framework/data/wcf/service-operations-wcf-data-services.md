---
description: 'Saiba mais sobre: operações de serviço (WCF Data Services)'
title: Operações de serviço (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service operations [WCF Data Services]
- WCF Data Services, service operations
ms.assetid: 583a690a-e60f-4990-8991-d6efce069d76
ms.openlocfilehash: 3c811da86b1654f33675b46575d45884a6ba9b1f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773089"
---
# <a name="service-operations-wcf-data-services"></a>Operações de serviço (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services permite que você defina as operações de serviço em um serviço de dados para expor métodos no servidor. Como outros recursos do serviço de dados, as operações de serviço são endereçadas por URIs. As operações de serviço permitem que você exponha a lógica de negócio em um serviço de dados, como implementar a lógica de validação, aplicar a segurança baseada em função, ou expor recursos de consulta especializada. As operações de serviço são métodos adicionados à classe de serviço de dados derivada de <xref:System.Data.Services.DataService%601> . Assim como todos os outros recursos de serviço de dados, você pode fornecer parâmetros para o método de operação de serviço. Por exemplo, o seguinte URI de operação de serviço (com base no serviço de dados de [início rápido](quickstart-wcf-data-services.md) ) passa o valor `London` para o `city` parâmetro:

```http
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'
```

A definição para esta operação de serviço é a seguinte:

[!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationdef)]
[!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationdef)]

Você pode usar o <xref:System.Data.Services.DataService%601.CurrentDataSource%2A> do <xref:System.Data.Services.DataService%601> para acessar diretamente a fonte de dados que o serviço de dados está usando. Para obter mais informações, consulte [como: definir uma operação de serviço](how-to-define-a-service-operation-wcf-data-services.md).

Para obter informações sobre como chamar uma operação de serviço de um aplicativo cliente .NET Framework, consulte [chamando operações de serviço](calling-service-operations-wcf-data-services.md).

## <a name="service-operation-requirements"></a>Requisitos da operação de serviço

Os seguintes requisitos aplicam-se ao definir operações de serviço no serviço de dados. Se um método não atender a esses requisitos, ele não será exposto como uma operação de serviço para o serviço de dados.

- A operação deve ser um método público de instância que é um membro da classe do serviço de dados.

- O método da operação só pode aceitar parâmetros de entrada. Os dados enviados no corpo da mensagem não podem ser acessados pelo serviço de dados.

- Se os parâmetros forem definidos, o tipo de cada parâmetro deverá ser um tipo primitivo. Todos os dados de um tipo não primitivo devem ser serializados e passados em um parâmetro de cadeia de caracteres.

- O método deve retornar um destes procedimentos:

  - `void` (`Nothing` no Visual Basic)

  - <xref:System.Collections.Generic.IEnumerable%601>

  - <xref:System.Linq.IQueryable%601>

  - Um tipo de entidade no modelo de dados que o serviço de dados expõe.

  - Uma classe primitiva como inteiro ou cadeia de caracteres.

- Para dar suporte a opções de consulta como classificação, paginação e filtragem, os métodos da operação de serviço deverão retornar <xref:System.Linq.IQueryable%601>. As solicitações a operações de serviço que incluem opções de consulta são rejeitadas para as operações que somente retornam <xref:System.Collections.Generic.IEnumerable%601>.

- Para dar suporte ao acesso a entidades relacionadas usando propriedades de navegação, a operação de serviço deverá retornar <xref:System.Linq.IQueryable%601>.

- O método deve ser anotado com o atributo `[WebGet]` ou `[WebInvoke]`.

  - `[WebGet]` permite que o método seja chamado usando uma solicitação GET.

  - `[WebInvoke(Method = "POST")]` permite que o método seja chamado usando uma solicitação POST. Outros métodos <xref:System.ServiceModel.Web.WebInvokeAttribute> não têm suporte.

- Uma operação de serviço pode ser anotada com o <xref:System.Data.Services.SingleResultAttribute> que especifica que o valor de retorno do método é uma única entidade em vez de uma coleção de entidades. Essa distinção determina a serialização resultante da resposta e a maneira na qual as passagens de propriedades de navegação adicionais são representadas no URI. Por exemplo, ao usar a serialização AtomPub, uma única instância do tipo de recurso é representada como um elemento de entrada e um conjunto de instâncias como um elemento de feed.

## <a name="addressing-service-operations"></a>Resolvendo operações de serviço

Você pode resolver operações de serviço colocando o nome do método no primeiro segmento de caminho de um URI. Como exemplo, o seguinte URI acessa uma operação `GetOrdersByState` que retorna uma coleção <xref:System.Linq.IQueryable%601> de objetos `Orders`.

```http
http://localhost:12345/Northwind.svc/GetOrdersByState?state='CA'&includeItems=true
```

Ao chamar uma operação de serviço, os parâmetros serão fornecidos como opções de consulta. A operação de serviço anterior aceita um parâmetro `state` de cadeia de caracteres e um parâmetro booliano `includeItems` que indica se deve incluir os objetos `Order_Detail` relacionados na resposta.

Os seguintes tipos de retorno são válidos para uma operação de serviço:

|Tipos de retorno válidos|Regras de URI|
|------------------------|---------------|
|`void` (`Nothing` no Visual Basic)<br /><br /> -ou-<br /><br /> Tipos de entidade<br /><br /> -ou-<br /><br /> Tipos primitivos|O URI deve ser um único segmento de caminho que é o nome da operação de serviço. As opções de consulta não são permitidas.|
|<xref:System.Collections.Generic.IEnumerable%601>|O URI deve ser um único segmento de caminho que é o nome da operação de serviço. Como o tipo do resultado não é um tipo <xref:System.Linq.IQueryable%601>, as opções de consulta não são permitidas.|
|<xref:System.Linq.IQueryable%601>|Os segmentos do caminho de consulta além do caminho que é o nome da operação de serviço são permitidos. As opções de consulta também são permitidas.|

Os segmentos de caminho ou as opções de consulta adicionais podem ser adicionados ao URI dependendo do tipo de retorno da operação de serviço. Por exemplo, o seguinte URI acessa uma operação `GetOrdersByCity` que retorna uma coleção <xref:System.Linq.IQueryable%601> de objetos `Orders`, ordenada por `RequiredDate` em ordem decrescente, juntamente com os objetos `Order_Details` relacionados:

```http
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc
```

## <a name="service-operations-access-control"></a>Controle de acesso a operações de serviço

A visibilidade do serviço de operações de serviço é controlada pelo método <xref:System.Data.Services.IDataServiceConfiguration.SetServiceOperationAccessRule%2A> na classe <xref:System.Data.Services.IDataServiceConfiguration> da mesma forma que a visibilidade do conjunto de entidades é controlada usando o método <xref:System.Data.Services.IDataServiceConfiguration.SetEntitySetAccessRule%2A>. Por exemplo, a seguinte linha de código na definição do serviço de dados permite o acesso à operação de serviço `CustomersByCity`.

[!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationconfig)]
[!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationconfig)]

> [!NOTE]
> Se uma operação de serviço tiver um tipo de retorno que foi oculto pelo acesso de restrição nos conjuntos de entidades subjacentes, a operação de serviço não estará disponível para aplicativos cliente.

Para obter mais informações, consulte [como: definir uma operação de serviço](how-to-define-a-service-operation-wcf-data-services.md).

## <a name="raising-exceptions"></a>Gerando exceções

Recomendamos que você use a classe <xref:System.Data.Services.DataServiceException> sempre que gerar uma exceção na execução do serviço de dados. Isso ocorre porque o runtime do serviço de dados sabe como mapear corretamente as propriedades desse objeto de exceção para a mensagem de resposta HTTP. Quando você gera um <xref:System.Data.Services.DataServiceException> em uma operação de serviço, a exceção retornada é empacotada em um <xref:System.Reflection.TargetInvocationException>. Para retornar o <xref:System.Data.Services.DataServiceException> base sem o <xref:System.Reflection.TargetInvocationException> incluído, você deverá substituir o método <xref:System.Data.Services.DataService%601.HandleException%2A> no <xref:System.Data.Services.DataService%601>, extrair o <xref:System.Data.Services.DataServiceException> de <xref:System.Reflection.TargetInvocationException> e retorná-lo como o erro de nível superior, como no exemplo a seguir:

[!code-csharp[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#handleexceptions)]
[!code-vb[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#handleexceptions)]

## <a name="see-also"></a>Consulte também

- [Interceptadores](interceptors-wcf-data-services.md)
