---
description: 'Saiba mais sobre: N camadas e aplicativos remotos com LINQ to SQL'
title: Aplicativos de n camadas e remoto com LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 854a1cdd-53cb-45f5-83ca-63962a9b3598
ms.openlocfilehash: 6abaeed8d4953a9b810db32418a4ebd3e78683fc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695600"
---
# <a name="n-tier-and-remote-applications-with-linq-to-sql"></a>Aplicativos de n camadas e remoto com LINQ to SQL

Você pode criar aplicativos de n camadas ou multicamadas que usam [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Normalmente, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] contexto de dados, as classes de entidade e a lógica de construção de consulta estão localizados na camada intermediária como a Dal (camada de acesso a dados). A lógica comercial e todos os dados não persistentes podem ser completamente implementados em classes e métodos parciais nas entidades e de contexto de dados, ou pode ser implementado em classes separados.

 O cliente ou a camada de apresentação chamam métodos na interface remoto de camada intermediária, e o DAL na camada executará as consultas ou procedimentos armazenados que são mapeados para os métodos de <xref:System.Data.Linq.DataContext> . A camada intermediária retorna os dados para clientes geralmente como representações de XML de entidades ou objetos de proxy.

 Na camada intermediária, as entidades são criadas pelo contexto de dados, que acompanha seu estado, e gerencia a carga de exceção e o envio de alterações ao base de dados. Essas entidades são anexados” a “ `DataContext`. No entanto, depois que as entidades são enviadas a outra camada com a serialização, ficam destacadas, que significa que `DataContext` já não estiver controlando seu estado. As entidades que o cliente envia novamente para atualizações devem ser reatadas ao contexto de dados antes que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] pode enviar as alterações para o base de dados. O cliente é responsável por fornecer valores originais e/ou os carimbos de data/hora de volta a camada intermediária se esses são necessários para concorrência otimista verificações.

 Em aplicativos ASP.NET, <xref:System.Web.UI.WebControls.LinqDataSource> gerencia a maioria da complexidade. Para obter mais informações, consulte [LinqDataSource Web Server Control Overview](/previous-versions/aspnet/bb547113(v=vs.100)).

## <a name="additional-resources"></a>Recursos adicionais

 Para obter mais informações sobre como implementar aplicativos de n camadas que usam [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], consulte os seguintes tópicos:

- [LINQ to SQL de n camadas com o ASP.NET](linq-to-sql-n-tier-with-aspnet.md)

- [LINQ to SQL de n camadas com serviços da Web](linq-to-sql-n-tier-with-web-services.md)

- [Implementar lógica de negócios de N camadas](implementing-business-logic-linq-to-sql.md)

- [Recuperação de dados e operações de COMIDA RUMINADA em aplicativos de n camadas (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)

 Para obter mais informações sobre aplicativos de n camadas que usam conjuntos de dados ADO.NET, consulte [trabalhar com conjuntos de dados em aplicativos de n camadas](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications).

## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
