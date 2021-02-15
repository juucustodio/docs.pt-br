---
description: 'Saiba mais sobre: LINQ to SQL consultas'
title: Consultas LINQ to SQL
ms.date: 03/30/2017
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
ms.openlocfilehash: 5b5df2095043b01eb426de86e4add91941bb74c6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712474"
---
# <a name="linq-to-sql-queries"></a>Consultas LINQ to SQL

Você define [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] consultas usando a mesma sintaxe que faria no LINQ. A única diferença é que os objetos referenciados nas consultas são mapeados para os elementos em uma base de dados. Para obter mais informações, consulte [Introdução a Consultas de LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte as consultas que você escreve em consultas SQL equivalentes e as envia para o servidor para processamento. Mais especificamente, seu aplicativo usa a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] API para solicitar a execução da consulta. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Em seguida, o provedor transforma a consulta em texto SQL e delega a execução para o provedor ADO. O provedor ADO retorna os resultados da consulta como um `DataReader` . O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] provedor converte os resultados do ADO em uma <xref:System.Linq.IQueryable> coleção de objetos de usuário.  
  
> [!NOTE]
> A maioria dos métodos e operadores em .NET Framework tipos internos têm traduções diretas para o SQL. Aqueles que o LINQ não pode converter geram exceções de tempo de execução. Para obter mais informações, consulte [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md).  
  
 A tabela a seguir mostra as semelhanças e diferenças entre o LINQ e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] os itens de consulta.  
  
|Item|Consulta LINQ|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Consulta|  
|----------|----------------|----------------------------------------------------------------------|  
|Tipo de retorno da variável local que contém a consulta (para consultas que as sequências de retorno)|`IEnumerable`genérico|`IQueryable`genérico|  
|Especificando a fonte de dados|Usa a `From` cláusula (Visual Basic) ou `from` (C#)|Idêntico|  
|Filtragem|Usa a `Where` / `where` cláusula|Idêntico|  
|Agrupamento|Usa a `Group…By` / `groupby` cláusula|Idêntico|  
|Selecione (se projetar)|Usa a `Select` / `select` cláusula|Idêntico|  
|Execução adiada versus imediata|Consulte [introdução às consultas LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)|Idêntico|  
|Implementar join|Usa a `Join` / `join` cláusula|Pode usar a `Join` / `join` cláusula, mas usa com mais eficiência o <xref:System.Data.Linq.Mapping.AssociationAttribute> atributo. Para obter mais informações, consulte [consultando entre relações](querying-across-relationships.md).|  
|Editando contra a execução local||Para obter mais informações, consulte [execução remota versus local](remote-vs-local-execution.md).|  
|Passar contra consulte armazenado em cachê|Não aplicável em um cenário de memória local||  
  
## <a name="see-also"></a>Consulte também

- [Introdução a consultas LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)
- [Operações de consulta LINQ básicas](../../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)
- [Relacionamentos de tipo em operações de consulta LINQ](../../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)
- [Consulte conceitos](query-concepts.md)
