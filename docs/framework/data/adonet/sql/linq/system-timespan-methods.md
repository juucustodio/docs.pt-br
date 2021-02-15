---
description: 'Saiba mais sobre: métodos System. TimeSpan'
title: Métodos de System.TimeSpan
ms.date: 03/30/2017
ms.assetid: 9333fee8-1454-4374-855b-8c14c002f48f
ms.openlocfilehash: fa3192d18a59e589f2c7510776f8510b2c12cac4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681182"
---
# <a name="systemtimespan-methods"></a>Métodos de System.TimeSpan

Suporte de membro para <xref:System.TimeSpan?displayProperty=nameWithType> depende das versões do .NET Framework e do Microsoft SQL Server que você está usando.  
  
 Quando um método, um operador, ou uma propriedade são sem suporte; significa que LINQ to SQL não pode converter o membro para execução no SQL Server. Você pode ainda seja possível usar esses membros no seu código. No entanto, devem ser avaliado antes que a consulta seja convertida a Transact-SQL ou após os resultados foram recuperados de base de dados.  
  
## <a name="previous-limitations"></a>Limitações anteriores  

 Ao usar LINQ to SQL com versões do .NET Framework antes do .NET Framework 3.5 SP1, você não pode mapear campos de base de dados SQL Server a <xref:System.TimeSpan?displayProperty=nameWithType>. No entanto, as operações no <xref:System.TimeSpan> têm suporte porque os valores <xref:System.TimeSpan> podem ser retornados da subtração de <xref:System.DateTime> ou introduzidos em uma expressão como um literal ou uma variável associada.  
  
## <a name="supported-systemtimespan-member-support"></a>Suporte ao membro System. TimeSpan com suporte

 Seguinte LINQ para os métodos suportados SQL-, operadores, e propriedades estão disponíveis para que você as use nas consultas LINQ to SQL. Mapeado uma vez no modelo de objeto ou no arquivo de mapeamento externo, LINQ to SQL permite que você chame muitos dos membros de <xref:System.TimeSpan?displayProperty=nameWithType> em suas consultas LINQ to SQL.  
  
|Métodos suportados de <xref:System.TimeSpan>|Operadores de <xref:System.TimeSpan> suportados|Propriedades suportadas de <xref:System.TimeSpan>|  
|------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.TimeSpan.Compare%2A>|<xref:System.TimeSpan.op_Equality%2A>|<xref:System.TimeSpan.Days%2A>|  
|<xref:System.TimeSpan.CompareTo%28System.TimeSpan%29>|<xref:System.TimeSpan.op_GreaterThan%2A>|<xref:System.TimeSpan.Hours%2A>|  
|<xref:System.TimeSpan.Duration%2A>|<xref:System.TimeSpan.op_GreaterThanOrEqual%2A>|<xref:System.TimeSpan.MaxValue>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%2CSystem.TimeSpan%29>|<xref:System.TimeSpan.op_Inequality%2A>|<xref:System.TimeSpan.Milliseconds%2A>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%29>|<xref:System.TimeSpan.op_LessThan%2A>|<xref:System.TimeSpan.Minutes%2A>|  
||<xref:System.TimeSpan.op_LessThanOrEqual%2A>|<xref:System.TimeSpan.MinValue>|  
  
> [!NOTE]
> A capacidade de mapear <xref:System.TimeSpan?displayProperty=nameWithType> para uma coluna do SQL `TIME` com LINQ to SQL requer o .NET Framework 3.5 SP1 e além. O tipo de dados SQL `TIME` só está disponível no Microsoft SQL Server 2008 e além.  
  
### <a name="addition-and-subtraction"></a>Adição e subtração  

 Embora o tipo de CLR <xref:System.TimeSpan?displayProperty=nameWithType> suporte a adição e subtração, o tipo do SQL `TIME` não. Devido a isso, as consultas LINQ to SQL gerarão erros se tentam a adição e subtração quando eles são mapeadas para o tipo do SQL `TIME` . Você pode encontrar outras considerações para trabalhar com tipos de data e hora SQL no [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md).  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
- [Criando o modelo de objeto](creating-the-object-model.md)
- [Mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md)
- [Tipos de dados e funções](data-types-and-functions.md)
