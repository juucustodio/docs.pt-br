---
description: 'Saiba mais sobre: visão geral do modelo de fábrica'
title: Visão geral do modelo de fábrica
ms.date: 03/30/2017
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
ms.openlocfilehash: 175b05a298eb260dfe8c59b380ab3b8b9dcba943
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724200"
---
# <a name="factory-model-overview"></a>Visão geral do modelo de fábrica

O ADO.NET 2,0 introduziu novas classes base no <xref:System.Data.Common> namespace. As classes base são abstratas, o que significa que elas não podem ser instanciadas diretamente. Elas incluem <xref:System.Data.Common.DbConnection> , e <xref:System.Data.Common.DbCommand> <xref:System.Data.Common.DbDataAdapter> e são compartilhadas pelos provedores de dados .NET Framework, como <xref:System.Data.SqlClient> e <xref:System.Data.OleDb> . A adição de classes base simplifica a adição de funcionalidade aos provedores de dados de .NET Framework sem a necessidade de criar novas interfaces.  
  
 O ADO.NET 2,0 também introduziu classes base abstratas, que permitem que um desenvolvedor escreva código de acesso a dados genérico que não depende de um provedor de dados específico.  
  
## <a name="the-factory-design-pattern"></a>O padrão de design de fábrica  

 O modelo de programação para escrever código independente de provedor é baseado no uso do padrão de design "Factory", que usa uma única API para acessar bancos de dados entre vários provedores. Esse padrão é adequadamente nomeado, pois chama o uso de um objeto especializado exclusivamente para criar outros objetos, muito parecido com uma fábrica do mundo real. Para obter uma descrição mais detalhada do padrão de design de fábrica, consulte [escrevendo código de acesso a dados genérico em ASP.NET 2,0 e ADO.NET 2,0](/previous-versions/dotnet/articles/ms971499(v=msdn.10)).
  
 A partir do ADO.NET 2,0, a <xref:System.Data.Common.DbProviderFactories> classe fornece `static` (ou `Shared` em Visual Basic) métodos para criar uma <xref:System.Data.Common.DbProviderFactory> instância. Em seguida, a instância retorna um objeto com rigidez de tipos correto com base nas informações do provedor e na cadeia de conexão fornecida em tempo de execução.  
  
## <a name="see-also"></a>Consulte também

- [Obtendo um DbProviderFactory](obtaining-a-dbproviderfactory.md)
- [DbConnection, DbCommand e DbException](dbconnection-dbcommand-and-dbexception.md)
- [Modificar dados com um DbDataAdapter](modifying-data-with-a-dbdataadapter.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
