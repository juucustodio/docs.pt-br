---
description: 'Saiba mais sobre: métodos System. DateTimeOffset'
title: Métodos de System.DateTimeOffset
ms.date: 03/30/2017
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
ms.openlocfilehash: 050c710d4a3f3db8112d0d108338c010345afdda
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681323"
---
# <a name="systemdatetimeoffset-methods"></a>Métodos de System.DateTimeOffset

Mapeado uma vez no modelo de objeto ou no arquivo de mapeamento externo, LINQ to SQL permite que você chame a maioria dos métodos de <xref:System.DateTimeOffset?displayProperty=nameWithType> , operadores, e as propriedades do seu consulte LINQ to SQL.  
  
 Somente os métodos suportados não são aqueles herdados de <xref:System.Object?displayProperty=nameWithType> que não fazem sentido no contexto de consultas LINQ to SQL, como: `Finalize`, `GetHashCode`, `GetType`, e `MemberwiseClone`. Esses métodos não são suportados porque LINQ to SQL não pode converter os para execução no SQL Server.  
  
> [!NOTE]
> A estrutura do Common Language Runtime (CLR) <xref:System.DateTimeOffset?displayProperty=nameWithType> , e a capacidade mapear-lo para uma coluna do SQL `DATETIMEOFFSET` com LINQ to SQL, requerem o .NET Framework 3.5 SP1 ou além. A coluna SQL `DATETIMEOFFSET` só está disponível no Microsoft SQL Server 2008 e além.  
  
## <a name="sqlmethods-date-and-time-methods"></a>Métodos de data e hora de SQLMethods  

 Além dos métodos oferecidos pela estrutura de <xref:System.DateTimeOffset> , LINQ to SQL oferece métodos listados na tabela de classes de <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=nameWithType> para trabalhar com data e hora.  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
- [Criando o modelo de objeto](creating-the-object-model.md)
- [Mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md)
