---
description: 'Saiba mais sobre: tipos de dados do SQL Server e ADO.NET'
title: Tipos de dados do SQL Server e ADO.NET
titleSuffix: ''
ms.date: 03/30/2017
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.openlocfilehash: 841fa5864bf54b5e4fc4dc24dab64e6ac1435c7e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767291"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipos de dados do SQL Server e ADO.NET

O SQL Server e o .NET Framework são baseados em diferentes tipos de sistema, o que pode resultar em potencial perda de dados. Para preservar a integridade dos dados, o provedor de dados .NET Framework para SQL Server (<xref:System.Data.SqlClient>) fornece métodos tipados acessadores para trabalhar com dados do SQL Server. Você pode usar as enumerações nas classes de <xref:System.Data.SqlDbType> para especificar tipos de dados <xref:System.Data.SqlClient.SqlParameter>.  
  
 Para obter mais informações e uma tabela que descreve os mapeamentos de tipo de dados entre SQL Server e .NET Framework tipos de dados, consulte [SQL Server mapeamentos de tipo de dados](../sql-server-data-type-mappings.md).  
  
 O SQL Server 2008 apresenta novos tipos de dados criados para atender às necessidades empresariais para trabalhar usando dados de data e hora, estruturados, semiestruturados e não estruturados. Eles são documentados nos Manuais Online do SQL Server 2008.  
  
 Os tipos de dados do SQL Server disponíveis para uso em seu aplicativo dependem da versão do SQL Server que você está usando. Para obter mais informações, consulte a versão relevante de Manuais Online do SQL Server na tabela a seguir.  
  
 **Documentação do SQL Server**  
  
1. [Tipos de dados (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)  
  
## <a name="in-this-section"></a>Nesta seção  

 [SqlTypes e DataSet](sqltypes-and-the-dataset.md)  
 Descreve o suporte de tipo para `SqlTypes` no `DataSet`.  
  
 [Manipulando valores nulos](handling-null-values.md)  
 Demonstra como trabalhar com valores nulos e lógica de três valores.  
  
 [Comparando valores de GUID e uniqueidentifier](comparing-guid-and-uniqueidentifier-values.md)  
 Demonstra como trabalhar com GUID e com valores uniqueidentifier no SQL Server e no .NET Framework.  
  
 [Dados de data e hora](date-and-time-data.md)  
 Descreve como usar os novos tipos de dados de data e hora introduzidos no SQL Server 2008.  
  
 [UDTs grandes](large-udts.md)  
 Demonstra como recuperar dados de UDTs de valor grande introduzidos no SQL Server 2008.  
  
 [Dados XML no SQL Server](xml-data-in-sql-server.md)  
 Descreve como trabalhar com os dados XML recuperados do SQL Server.  
  
## <a name="reference"></a>Referência  

 <xref:System.Data.DataSet>  
 Descreve a classe `DataSet` e todos os membros dela.  
  
 <xref:System.Data.SqlTypes>  
 Descreve o namespace `SqlTypes` e todos os membros dele.  
  
 <xref:System.Data.SqlDbType>  
 Descreve a enumeração `SqlDbType` e todos os membros dela.  
  
 <xref:System.Data.DbType>  
 Descreve a enumeração `DbType` e todos os membros dela.  
  
## <a name="see-also"></a>Consulte também

- [Mapeamentos de tipos de dados do SQL Server](../sql-server-data-type-mappings.md)
- [Configurar parâmetros e tipos de dados de parâmetro](../configuring-parameters-and-parameter-data-types.md)
- [Parâmetros com valor de tabela](table-valued-parameters.md)
- [Dados binários e de valor grande do SQL Server](sql-server-binary-and-large-value-data.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
