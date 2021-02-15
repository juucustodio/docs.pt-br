---
description: 'Saiba mais sobre: Enumerando instâncias de SQL Server (ADO.NET)'
title: Enumerando instâncias de SQL Server
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.openlocfilehash: dd52142a06d5c7203eb8a2a14d0e6fc48f1e2a27
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672303"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>Enumerando instâncias do SQL Server (ADO.NET)

O SQL Server permite que aplicativos localizem instâncias do SQL Server na rede atual. A classe <xref:System.Data.Sql.SqlDataSourceEnumerator> expõe essas informações ao desenvolvedor de aplicativos, fornecendo um <xref:System.Data.DataTable> que contém informações sobre todos os servidores visíveis. Esta tabela retornada contém uma lista de instâncias de servidor disponíveis na rede que corresponde à lista fornecida quando um usuário tenta criar uma nova conexão, e expande a lista suspensa que contém todos os servidores disponíveis na caixa de diálogo **Propriedades da Conexão**. Os resultados exibidos nem sempre estão completos.  
  
> [!NOTE]
> Assim como na maioria dos serviços Windows, é melhor executar o serviço do SQL Browser com o mínimo possível de privilégios. Confira os Manuais Online do SQL Server para obter mais informações sobre o serviço do navegador do SQL e sobre como gerenciar seu comportamento.  
  
## <a name="retrieving-an-enumerator-instance"></a>Recuperando uma instância de enumerador  

 Para recuperar a tabela que contém informações sobre as instâncias disponíveis do SQL Server, primeiro recupere um enumerador, usando a propriedade compartilhada/estática <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A>:  
  
```vb  
Dim instance As System.Data.Sql.SqlDataSourceEnumerator = _  
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
 Depois de recuperar a instância estática, você pode chamar o método <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>, que retorna um <xref:System.Data.DataTable> que contém informações sobre os servidores disponíveis:  
  
```vb  
Dim dataTable As System.Data.DataTable = instance.GetDataSources()  
```  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
 A tabela retornada da chamada de método contém as seguintes colunas e todas elas contêm valores `string`:  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**ServerName**|O nome do servidor.|  
|**InstanceName**|Nome da instância do servidor. Em branco se o servidor estiver sendo executado como a instância padrão.|  
|**IsClustered**|Indica se o servidor faz parte de um cluster.|  
|**Versão**|Versão do servidor. Por exemplo:<br /><br /> -   9.00.x (SQL Server 2005)<br />– 10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />– 11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>Limitações de enumeração  

 Todos os servidores disponíveis podem ou não estar listados. A lista pode variar dependendo de fatores como tempos limite e tráfego de rede. Isso pode fazer com que a lista seja diferente em duas chamadas consecutivas. Somente os servidores na mesma rede serão listados. Os pacotes de difusão normalmente não percorrerão roteadores, motivo pelo qual você não verá um servidor listado, mas ele será estável em chamadas.  
  
 Os servidores listados podem ou não ter informações adicionais, como `IsClustered` e versão. Isso depende de como a lista foi obtida. Servidores listados através do serviço do navegador do SQL Server terão mais detalhes do que os encontrados pela infraestrutura do Windows, que listarão somente o nome.  
  
> [!NOTE]
> A enumeração de servidor só está disponível quando executada em confiança total. Os assemblies em execução em um ambiente parcialmente confiável não poderão usá-lo, mesmo que tenham a permissão de CAS (segurança de acesso ao código) do <xref:System.Data.SqlClient.SqlClientPermission>.  
  
 O SQL Server fornece informações para <xref:System.Data.Sql.SqlDataSourceEnumerator> usando um serviço Windows externo chamado SQL Browser. Esse serviço é habilitado por padrão, mas os administradores podem desativá-lo ou desabilitá-lo, tornando a instância do servidor invisível para essa classe.  
  
## <a name="example"></a>Exemplo  

 O aplicativo de console a seguir recupera informações sobre todas as instâncias visíveis do SQL Server e exibe as informações na janela do console.  
  
```vb  
Imports System.Data.Sql  
  
Module Module1  
  Sub Main()  
    ' Retrieve the enumerator instance and then the data.  
    Dim instance As SqlDataSourceEnumerator = _  
     SqlDataSourceEnumerator.Instance  
    Dim table As System.Data.DataTable = instance.GetDataSources()  
  
    ' Display the contents of the table.  
    DisplayData(table)  
  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Sub  
  
  Private Sub DisplayData(ByVal table As DataTable)  
    For Each row As DataRow In table.Rows  
      For Each col As DataColumn In table.Columns  
        Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
      Next  
      Console.WriteLine("============================")  
    Next  
  End Sub  
End Module  
```  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [SQL Server e ADO.NET](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
