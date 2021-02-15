---
description: 'Saiba mais sobre: operações assíncronas'
title: Operações assíncronas
ms.date: 03/30/2017
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.openlocfilehash: 415da1c8a9891bcca13ad26cbbc4c09bfd8909f1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718558"
---
# <a name="asynchronous-operations"></a>Operações assíncronas

Algumas operações de banco de dados, como execuções de comando, podem demorar significativamente para serem concluídas. Nesses casos, os aplicativos de thread único devem bloquear outras operações e aguardar a conclusão do comando antes de poderem continuar suas próprias operações. Por outro lado, poder atribuir a operação demorada a um thread em segundo plano permite que o thread de primeiro plano permaneça ativo durante toda a operação. Em um aplicativo do Windows, por exemplo, delegar a operação demorada para um thread em segundo plano permite que o thread de interface do usuário permaneça responsivo enquanto a operação está em execução.  
  
 O .NET Framework fornece vários padrões de design assíncrono padrão que os desenvolvedores podem usar para aproveitar os threads em segundo plano e liberar a interface do usuário ou threads de alta prioridade para concluir outras operações. O ADO.NET dá suporte a esses mesmos padrões de design em sua <xref:System.Data.SqlClient.SqlCommand> classe. Especificamente, os métodos <xref:System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> e <xref:System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, emparelhados com os métodos <xref:System.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e <xref:System.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, fornecem o suporte assíncrono.  
  
> [!NOTE]
> A programação assíncrona é um recurso fundamental do .NET Framework, e o ADO.NET aproveita totalmente os padrões de design padrão. Para obter mais informações sobre as diferentes técnicas assíncronas disponíveis para os desenvolvedores, confira [Chamar métodos síncronos de forma assíncrona](../../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md).  
  
 Embora o uso de técnicas assíncronas com recursos ADO.NET não adicione nenhuma consideração especial, é provável que mais desenvolvedores usem recursos assíncronos no ADO.NET do que em outras áreas do .NET Framework. É importante estar ciente dos benefícios e das armadilhas da criação de aplicativos multissegmentados. Os exemplos a seguir nesta seção apontam vários problemas importantes que os desenvolvedores precisarão levar em consideração ao criar aplicativos que incorporam a funcionalidade multithread.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Aplicativos do Windows que usam retornos de chamada](windows-applications-using-callbacks.md)  
 Fornece um exemplo que demonstra como executar um comando assíncrono com segurança, manipulando corretamente a interação com um formulário e seu conteúdo de um thread separado.  
  
 [Aplicativos ASP.NET que usam identificadores de espera](aspnet-apps-using-wait-handles.md)  
 Fornece um exemplo que demonstra como executar vários comandos simultâneos de uma página do ASP.NET, usando os identificadores de espera para gerenciar a operação na conclusão de todos os comandos.  
  
 [Sondagem em aplicativos de console](polling-in-console-applications.md)  
 Fornece um exemplo que demonstra o uso de sondagem para aguardar a conclusão de uma execução de comando assíncrona de um aplicativo de console. Essa técnica também é válida em uma biblioteca de classes ou outro aplicativo sem uma interface do usuário.  
  
## <a name="see-also"></a>Consulte também

- [SQL Server e ADO.NET](index.md)
- [Chamando métodos síncronos de forma assíncrona](../../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
