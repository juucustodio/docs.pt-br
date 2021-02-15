---
title: 'Como: exibir o SQL gerado'
description: Saiba como exibir o código SQL gerado para consultas usando a propriedade log para ajudar a entender LINQ to SQL funcionalidade e para depuração.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 626492c0-5ee3-4675-88e8-8c40379510b6
ms.openlocfilehash: 81f6b9603cc7f8b7863f787272ce6a1af920fa75
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169473"
---
# <a name="how-to-display-generated-sql"></a>Como: exibir o SQL gerado

Você pode exibir o código SQL gerado para consultas e processamento de alteração usando a propriedade de <xref:System.Data.Linq.DataContext.Log%2A> . Essa abordagem pode ser útil para entender a funcionalidade de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] e depure questões específicas.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa a propriedade de <xref:System.Data.Linq.DataContext.Log%2A> para exibir o código SQL na janela do console antes que o código seja executado.  Você pode usar essa propriedade com consulta, inserir, atualizar, excluir e comandos.  
  
 As linhas da janela do console são as que você vê ao executar o código de Visual Basic ou C# a seguir.  
  
```console  
SELECT [t0].[CustomerID], [t0].[CompanyName], [t0].[ContactName], [t0].[ContactT  
itle], [t0].[Address], [t0].[City], [t0].[Region], [t0].[PostalCode], [t0].[Coun  
try], [t0].[Phone], [t0].[Fax]  
FROM [dbo].[Customers] AS [t0]  
WHERE [t0].[City] = @p0  
-- @p0: Input String (Size = 6; Prec = 0; Scale = 0) [London]  
-- Context: SqlProvider(Sql2005) Model: AttributedMetaModel Build: 3.5.20810.0  
```  
  
```console  
AROUT  
BSBEV  
CONSH  
EASTC  
NORTS  
SEVES  
```  
  
 [!code-csharp[DLinqDebuggingSupport#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDebuggingSupport/cs/Program.cs#1)]
 [!code-vb[DLinqDebuggingSupport#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDebuggingSupport/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>Confira também

- [Depuração de suporte](debugging-support.md)
