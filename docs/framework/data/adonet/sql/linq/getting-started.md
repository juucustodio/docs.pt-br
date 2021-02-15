---
title: Guia de Introdução
description: Com este código de exemplo, comece a usar o LINQ to SQL para utilizar a tecnologia LINQ para acessar bancos de dados SQL da mesma forma que você acessaria uma coleção na memória.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: db8a557a-fef8-4f4f-bb91-8cff7250ee25
ms.openlocfilehash: b886518d4cff687a18f363c3e3ba43b40631a22f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194369"
---
# <a name="getting-started"></a>Introdução

Usando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o, você pode usar a tecnologia LINQ para acessar bancos de dados SQL da mesma forma que acessaria uma coleção na memória.  
  
 Por exemplo, o objeto `nw` no código a seguir é criado para representar o banco de dados `Northwind`, a tabela `Customers` é destinada, as linhas são filtradas para `Customers` de `London` e uma cadeia de caracteres de `CompanyName` é selecionada para recuperação.  
  
 Quando o loop é executado, a coleção de valores de `CompanyName` é recuperada.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## <a name="next-steps"></a>Próximas etapas  

 Para obter alguns exemplos adicionais, incluindo inserção e atualização, consulte [o que você pode fazer com LINQ to SQL](what-you-can-do-with-linq-to-sql.md).  
  
 Em seguida, tente alguns tutoriais e explicações passo a passo para ter uma experiência prática de uso do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Consulte [aprendendo por passo a passos](learning-by-walkthroughs.md).  
  
 Por fim, saiba como começar a usar seu próprio [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projeto lendo [as etapas típicas para o uso de LINQ to SQL](typical-steps-for-using-linq-to-sql.md).  
  
## <a name="see-also"></a>Veja também

- [LINQ to SQL](index.md)
- [Introdução ao LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/index.md)
- [Introdução ao LINQ (Visual Basic)](../../../../../visual-basic/programming-guide/concepts/linq/introduction-to-linq.md)
- [Modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md)
