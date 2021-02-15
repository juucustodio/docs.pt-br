---
title: 'Como: usar funções definidas pelo usuário com valor de tabela'
description: Use estes exemplos para aprender a criar uma função com valor de tabela, que retorna um único conjunto de linhas. Use essa função com valor de tabela, assim como uma tabela.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5a4ae2b4-3290-4aa1-bc95-fc70c51b54cf
ms.openlocfilehash: 68a2b54c8fd541595d36bf9c864257b1be1f7856
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203573"
---
# <a name="how-to-use-table-valued-user-defined-functions"></a>Como: usar funções definidas pelo usuário com valor de tabela

Uma função de tabela valorizada retorna um único rowset (em vez de procedimentos armazenados, que podem retornar várias formas de resultado). Porque o tipo de retorno de uma função de tabela valorizada é `Table`, você pode usar uma função de tabela valorizada em qualquer lugar em SQL que você pode usar uma tabela. Você também pode tratar a função de tabela valorizada assim como você uma tabela.  
  
## <a name="example"></a>Exemplo  

 A função a seguir indica explicitamente SQL que retorna `TABLE`. Portanto, a estrutura de rowset retornado é definida implicitamente.  
  
```sql
CREATE FUNCTION ProductsCostingMoreThan(@cost money)  
RETURNS TABLE  
AS  
RETURN  
    SELECT ProductID, UnitPrice  
    FROM Products  
    WHERE UnitPrice > @cost  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mapeia a função como segue:  
  
 [!code-csharp[DLinqUDFS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#1)]
 [!code-vb[DLinqUDFS#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#1)]  
  
## <a name="example"></a>Exemplo  

 O código a seguir mostra SQL que você pode se juntar a tabela que a função e retorna a trata de outra maneira como você faria qualquer outra tabela:  
  
```sql
SELECT p2.ProductName, p1.UnitPrice  
FROM dbo.ProductsCostingMoreThan(80.50)  
AS p1 INNER JOIN Products AS p2 ON p1.ProductID = p2.ProductID  
```  
  
 Em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], a consulta será processada como segue:  
  
 [!code-csharp[DLinqUDFS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#2)]
 [!code-vb[DLinqUDFS#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Veja também

- [Funções definidas pelo usuário](user-defined-functions.md)
