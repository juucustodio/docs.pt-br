---
description: 'Saiba mais sobre: como retornar conjuntos de linhas'
title: 'Como: retornar conjuntos de linhas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 725718f5-da29-4841-9f53-aafef64ba977
ms.openlocfilehash: b799ce82542e6929f42485508b3a2c36cc42ee60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723381"
---
# <a name="how-to-return-rowsets"></a>Como: retornar conjuntos de linhas

Este exemplo retorna um conjunto de linhas do banco de dados e inclui um parâmetro de entrada para filtrar o resultado.  
  
 Ao executar um procedimento armazenado que retorna um conjunto de linhas, você usa uma classe *Result* que armazena os retornos do procedimento armazenado. Para obter mais informações, consulte [analisando LINQ to SQL código-fonte](analyzing-linq-to-sql-source-code.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir representa um procedimento armazenado que retorna linhas de clientes e usa um parâmetro de entrada para retornar somente as linhas que listam "London" como a cidade do cliente. O exemplo supõe uma classe `CustomersByCityResult` enumerável.  
  
```sql  
CREATE PROCEDURE [dbo].[Customers By City]  
    (@param1 NVARCHAR(20))  
AS  
BEGIN  
    -- SET NOCOUNT ON added to prevent extra result sets from  
    -- interfering with SELECT statements.  
    SET NOCOUNT ON;  
    SELECT CustomerID, ContactName, CompanyName, City from Customers  
        as c where c.City=@param1  
END  
```  
  
 [!code-csharp[DLinqSprox#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#1)]
 [!code-vb[DLinqSprox#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Procedimentos armazenados](stored-procedures.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
