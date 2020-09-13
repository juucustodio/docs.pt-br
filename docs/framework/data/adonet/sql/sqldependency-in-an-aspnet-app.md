---
title: SqlDependency em um aplicativo ASP.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.openlocfilehash: 2ec9415f63151443d5008fbce471fabeb89cdb91
ms.sourcegitcommit: 1e8382d0ce8b5515864f8fbb178b9fd692a7503f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89656165"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency em um aplicativo ASP.NET
O exemplo nesta seção mostra como usar <xref:System.Data.SqlClient.SqlDependency> indiretamente, utilizando o objeto ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. O objeto <xref:System.Web.Caching.SqlCacheDependency> usa um <xref:System.Data.SqlClient.SqlDependency> para escutar notificações e atualizar corretamente o cache.  
  
> [!NOTE]
> O código de exemplo pressupõe que você habilitou notificações de consulta executando os scripts em [habilitando notificações de consulta](enabling-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Sobre o aplicativo de exemplo  
 O aplicativo de exemplo usa uma página da Web ASP.NET para exibir informações sobre o produto no banco de dados do SQL Server **AdventureWorks** em um controle <xref:System.Web.UI.WebControls.GridView>. Quando a página é carregada, o código grava a hora atual em um controle <xref:System.Web.UI.WebControls.Label>. Ele define um objeto <xref:System.Web.Caching.SqlCacheDependency> e as propriedades no objeto <xref:System.Web.Caching.Cache> para armazenar os dados do cache por até três minutos. O código se conecta ao banco de dados e recupera os dados. Quando a página é carregada e o aplicativo está em execução, o ASP.NET recuperará os dados do cache, que você pode verificar observando que a hora na página não é alterada. Se os dados que estão sendo monitorados forem alterados, o ASP.NET invalidará o cache e preencherá novamente o controle `GridView` com os dados atualizados, atualizando a hora exibida no controle `Label`.  
  
## <a name="creating-the-sample-application"></a>Criando o aplicativo de exemplo  
 Siga estas etapas para criar e executar o aplicativo de exemplo:  
  
1. Criar um site do ASP.NET.  
  
2. Adicione um <xref:System.Web.UI.WebControls.Label> e um controle <xref:System.Web.UI.WebControls.GridView> à página Default.aspx.  
  
3. Abra o módulo de classe da página e adicione as seguintes diretivas:  
  
    ```vb  
    Option Strict On  
    Option Explicit On  
  
    Imports System.Data.SqlClient  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Adicione o seguinte código no evento `Page_Load` da página:  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#1)]
     [!code-vb[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#1)]  
  
5. Adicione dois métodos auxiliares, `GetConnectionString` e `GetSQL`. A cadeia de conexão definida usa segurança integrada. Você precisará verificar se a conta que está usando tem as permissões de banco de dados necessárias e se o banco de dados de exemplo, **AdventureWorks**, tem notificações habilitadas.
  
     [!code-csharp[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#2)]
     [!code-vb[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#2)]  
  
### <a name="testing-the-application"></a>Testando o aplicativo  
 O aplicativo armazenará em cache os dados exibidos no formulário da Web e os atualizará a cada três minutos se não houver atividade. Se ocorrer uma alteração no banco de dados, o cache será atualizado imediatamente. Execute o aplicativo no Visual Studio, que carrega a página para o navegador. O tempo de atualização do cache exibido indica quando o cache foi atualizado pela última vez. Aguarde três minutos e atualize a página, fazendo ocorrer um evento de postback. Observe que a hora exibida na página foi alterada. Se você atualizar a página em menos de três minutos, a hora exibida na página permanecerá a mesma.  
  
 Agora atualize os dados no banco de dados, usando um comando UPDATE Transact-SQL e atualize a página. A hora exibida agora indica que o cache foi atualizado com os novos dados do banco de dados. Observe que, embora o cache seja atualizado, a hora exibida na página não é alterada até que ocorra um evento de postback.  

## <a name="distributed-cache-synchronization-using-sql-dependency"></a>Sincronização de cache distribuído usando dependência SQL

Alguns dos caches distribuídos de terceiros, como o [NCache](https://www.alachisoft.com/ncache) , oferecem suporte para sincronizar o banco de dados SQL e o cache usando a [dependência SQL](https://www.alachisoft.com/resources/docs/ncache/prog-guide/sql-dependency.html). Para obter mais informações e uma implementação de código-fonte de exemplo, consulte [exemplo de dependência de SQL de cache distribuído](https://github.com/Alachisoft/NCache-Samples/tree/master/dotnet/Dependencies/SQLDependency).

## <a name="see-also"></a>Confira também

- [Notificações de consulta no SQL Server](query-notifications-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
