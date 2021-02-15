---
description: 'Saiba mais sobre: como: resultados de consulta do projeto (WCF Data Services)'
title: 'Como: resultados da consulta de projeto (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- projection [WCF Data Services]
- WCF Data Services, projection
- query projection [WCF Data Services]
- WCF Data Services, querying
ms.assetid: 474ac625-8770-43ba-8320-d3315ea9530f
ms.openlocfilehash: a851176e5f97e31d2e8d9ac62c720d04df4ddc37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765107"
---
# <a name="how-to-project-query-results-wcf-data-services"></a>Como: resultados da consulta de projeto (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

A projeção fornece um mecanismo para reduzir a quantidade de dados retornados por uma consulta, especificando que apenas determinadas propriedades de uma entidade são retornadas na resposta. Você pode executar projeções nos resultados de uma consulta de WCF Data Services usando a opção de `$select` consulta ou usando a cláusula [Select](../../../csharp/language-reference/keywords/select-clause.md) ([Select](../../../visual-basic/language-reference/queries/select-clause.md) in Visual Basic) em uma consulta LINQ. Para obter mais informações, consulte [consultando o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma consulta LINQ que projeta entidades de clientes em um novo tipo CustomerAddress, que contém apenas propriedades específicas de endereço e a propriedade Identity. Essa `CustomerAddress` classe é definida no cliente e é atribuída para que a biblioteca de cliente possa reconhecê-la como um tipo de entidade.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#selectcustomeraddress)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#selectcustomeraddress)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma consulta LINQ que os projetos retornavam entidades de clientes em um novo tipo CustomerAddressNonEntity, que contém apenas propriedades específicas de endereço e nenhuma propriedade Identity. Essa `CustomerAddressNonEntity` classe é definida no cliente e não é atribuída como um tipo de entidade.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#selectcustomeraddressnonentity)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#selectcustomeraddressnonentity)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra as definições dos `CustomerAddress` `CustomerAddressNonEntity` tipos e que são usados nos exemplos anteriores.  
  
 [!code-csharp[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customeraddress.cs#customeraddressdefinition)]
 [!code-vb[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customeraddress.vb#customeraddressdefinition)]
