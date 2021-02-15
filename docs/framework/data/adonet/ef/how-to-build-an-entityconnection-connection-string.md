---
description: 'Saiba mais sobre: como criar uma cadeia de conexão de EntityConnection'
title: 'Como: criar uma cadeia de conexão EntityConnection'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5bd1a748-3df7-4d0a-a607-14f25e3175e9
ms.openlocfilehash: 760ed9d1f362e08135586a56a6b900afcd2b13bd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650827"
---
# <a name="how-to-build-an-entityconnection-connection-string"></a>Como: criar uma cadeia de conexão EntityConnection

Este tópico fornece um exemplo de como criar um <xref:System.Data.EntityClient.EntityConnection>.  
  
### <a name="to-run-the-code-in-this-example"></a>Para executar o código nesse exemplo  
  
1. Adicione o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) ao seu projeto e configure seu projeto para usar o Entity Framework. Para obter mais informações, consulte [como: usar o assistente de modelo de dados de entidade](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).  
  
2. Na página de código do seu aplicativo, adicione as seguintes instruções `using` (`Imports` no Visual Basic):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir inicializa o <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType> para o provedor subjacente e, em seguida, inicializa o objeto <xref:System.Data.EntityClient.EntityConnectionStringBuilder?displayProperty=nameWithType> e passa esse objeto para o construtor di <xref:System.Data.EntityClient.EntityConnection>.  
  
 [!code-csharp[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#buildingconnectionstringwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#buildingconnectionstringwithentitycommand)]  
  
## <a name="see-also"></a>Consulte também

- [Como: usar EntityConnection com um contexto de objeto](/previous-versions/dotnet/netframework-4.0/bb738461(v=vs.100))
- [Provedor EntityClient para Entity Framework](entityclient-provider-for-the-entity-framework.md)
