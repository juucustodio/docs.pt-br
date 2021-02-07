---
description: 'Saiba mais sobre: SQL Server Express instâncias de usuário'
title: Instâncias de usuário do SQL Server Express
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.openlocfilehash: 8579dee5c31a2b63156db72df6cc109beb843f08
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767265"
---
# <a name="sql-server-express-user-instances"></a>Instâncias de usuário do SQL Server Express

O Microsoft SQL Server Express Edition (SQL Server Express) dá suporte ao recurso de instância de usuário, que somente está disponível quando é usado o Provedor de Dados .NET Framework para SQL Server (`SqlClient`). Uma instância de usuário é uma instância separada do Mecanismo de Banco de Dados do SQL Server Express gerada por uma instância pai. As instâncias de usuário permitem que os usuários que não são administradores nos computadores locais deles anexem bancos de dados do SQL Server Express e se conectem a eles. Cada instância é executada no contexto de segurança do usuário individual, uma instância por usuário.  
  
## <a name="user-instance-capabilities"></a>Recursos de instância de usuário  

 As instâncias de usuário são úteis para usuários que executam o Windows sob uma conta de usuário com privilégios mínimos (LUA). Cada usuário tem SQL Server `sysadmin` privilégios de administrador do sistema sobre a instância em execução em seu computador sem precisar executar como administrador do Windows também. O software em execução em uma instância de usuário com permissões limitadas não pode realizar alterações em todo o sistema porque a instância do SQL Server Express está em execução na conta do Windows que não é de administrador do usuário, não como um serviço. Cada instância de usuário é isolada de sua instância pai e de qualquer outra instância de usuário que estiver em execução no mesmo computador. Os bancos de dados em execução em uma instância de usuário são abertos somente no modo de usuário único. Não é possível a conexão de vários usuários a bancos de dados em execução em uma instância de usuário. A replicação e as consultas distribuídas também são desabilitadas para instâncias de usuário.
  
> [!NOTE]
> As instâncias de usuário não são necessárias para usuários que já são administradores nos próprios computadores ou para cenários que envolvam vários usuários de banco de dados.  
  
## <a name="enabling-user-instances"></a>Habilitando instâncias de usuário  

 Para gerar instâncias de usuário, uma instância pai do SQL Server Express deve estar em execução. As instâncias de usuário são habilitadas por padrão quando o SQL Server Express é instalado, e podem ser habilitadas ou desabilitadas explicitamente por um administrador do sistema que esteja executando o procedimento armazenado do sistema **sp_configure** na instância pai.  
  
```sql  
-- Enable user instances.  
sp_configure 'user instances enabled','1'
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
 O protocolo de rede das instâncias de usuário só podem ser Pipes Nomeados. Uma instância de usuário não pode ser iniciada em uma instância remota do SQL Server e não são permitidos logons do SQL Server.  
  
## <a name="connecting-to-a-user-instance"></a>Conectando-se a uma instância de usuário  

 As palavras-chave `User Instance` e `AttachDBFilename`<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> permitem que <xref:System.Data.SqlClient.SqlConnection> se conecte a uma instância de usuário. Também há suporte para instâncias de usuário nas propriedades <xref:System.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` e `AttachDBFilename`.  
  
 Observe o seguinte sobre as cadeias de conexão de exemplo mostradas abaixo:  
  
- A palavra-chave `Data Source` se refere à instância pai do SQL Server Express que está gerando a instância de usuário. A instância padrão é .\sqlexpress.  
  
- `Integrated Security` está definido como `true`. Para se conectar a uma instância de usuário, é preciso autenticar-se no Windows; não há suporte para logons do SQL Server.  
  
- O `User Instance` é definido como `true`, que invoca uma instância de usuário. (O padrão é `false`.)  
  
- A palavra-chave da cadeia de conexão `AttachDbFileName` é usada para anexar o arquivo de banco de dados primário (.mdf), que deve incluir o nome do caminho completo. `AttachDbFileName` também corresponde às chaves "propriedades estendidas" e "nome do arquivo inicial" em uma cadeia de conexão <xref:System.Data.SqlClient.SqlConnection>.  
  
- A cadeia de caracteres de substituição `|DataDirectory|` incluída nos símbolos de pipe refere-se ao diretório de dados do aplicativo que abre a conexão e fornece um caminho relativo que indica a localização dos arquivos de banco de dados .mdf e .ldf e de log. Se desejar localizar esses arquivos em outro lugar, você deverá fornecer o caminho completo para os arquivos.  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
> Você também pode usar as propriedades <xref:System.Data.SqlClient.SqlConnectionStringBuilder><xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> e <xref:System.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> para criar uma cadeia de conexão em tempo de execução.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>Usando a cadeia de caracteres de substituição do &#124;DataDirectory&#124;  

 `AttachDbFileName` foi ampliado no ADO.NET 2.0 com a introdução da cadeia de caracteres de substituição `|DataDirectory|` (entre barras verticais). `DataDirectory` é usado em conjunto com `AttachDbFileName` para indicar um caminho relativo para um arquivo de dados, permitindo que os desenvolvedores criem cadeias de conexão baseadas em um caminho relativo para a fonte de dados em vez precisarem especificar um caminho completo.  
  
 A localização física para a qual `DataDirectory` aponta depende do tipo de aplicativo. Neste exemplo, o arquivo Northwind.mdf a ser anexado está localizado na pasta \app_data do aplicativo.  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
 Quando `DataDirectory` é usado, o caminho do arquivo resultante não pode ser maior na estrutura de diretório do que o diretório apontado pela cadeia de caracteres de substituição. Por exemplo, se o `DataDirectory` totalmente expandido for C:\AppDirectory\app_data, a cadeia de conexão de exemplo mostrada acima funcionará porque está embaixo de c:\AppDirectory. No entanto, tentar especificar `DataDirectory` como `|DataDirectory|\..\data` resultará em um erro porque \data não é um subdiretório de \AppDirectory.  
  
 Se a cadeia de conexão tiver uma cadeia de caracteres de substituição formatada incorretamente, uma <xref:System.ArgumentException> será gerada.  
  
> [!NOTE]
> <xref:System.Data.SqlClient> resolve as cadeias de caracteres de substituição em caminhos completos com relação ao sistema de arquivos do computador local. Portanto, não há suporte para servidor remoto, HTTP e nomes de caminho UNC. Uma exceção será gerada quando a conexão for aberta se o servidor não estiver localizado no computador local.  
  
 Quando <xref:System.Data.SqlClient.SqlConnection> é aberto, é redirecionado da instância do SQL Server Express padrão para uma instância iniciada em tempo de execução que está sendo executada na conta do chamador.  
  
> [!NOTE]
> Pode ser necessário aumentar o valor <xref:System.Data.SqlClient.SqlConnection.ConnectionTimeout%2A>, pois as instâncias de usuário podem levar mais tempo para serem carregadas do que instâncias regulares.  
  
 O fragmento de código a seguir abre uma nova `SqlConnection`, exibe a cadeia de conexão na janela do console e fecha a conexão ao sair do bloco de código de `using`.  
  
```vb  
Private Sub OpenSqlConnection()  
    ' Retrieve the connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    Using connection As New SqlConnection(connectionString)  
        connection.Open()  
        Console.WriteLine("ConnectionString: {0}", _  
           connection.ConnectionString)  
    End Using  
End Sub  
```  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
> Não há suporte para instâncias de usuário em código CLR (Common Language Runtime) que está em execução dentro do SQL Server. Uma <xref:System.InvalidOperationException> será gerada se `Open` for chamado em um <xref:System.Data.SqlClient.SqlConnection> que tenha `User Instance=true` na cadeia de conexão.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>Tempo de vida de uma conexão de instância de usuário  

 Diferentemente das versões de SQL Server executadas como um serviço, as instâncias do SQL Server Express não precisam ser iniciadas nem interrompidas manualmente. Sempre que um usuário fizer logon e se conectar a uma instância de usuário, ela será iniciada se ainda não estiver em execução. Os bancos de dados da instância de usuário têm a opção `AutoClose` definida para que o banco de dados seja desligado automaticamente após um período de inatividade. O processo sqlservr.exe iniciado será mantido em execução durante um período de tempo limite limitado depois que a última conexão com a instância for fechada; portanto, não será necessário reiniciá-la se outra conexão for aberta antes que o tempo limite tenha expirado. A instância de usuário será desligada automaticamente se nenhuma nova conexão for aberta antes que esse período de tempo limite tenha expirado. Um administrador do sistema na instância pai pode definir a duração do período de tempo limite para uma instância do usuário usando **sp_configure** para alterar a opção **tempo limite da instância de usuário**. O padrão é de 60 minutos.  
  
> [!NOTE]
> Se `Min Pool Size` for usado na cadeia de conexão com um valor maior que zero, o pooler de conexão sempre manterá algumas conexões abertas e a instância do usuário não será desligada automaticamente.  
  
## <a name="how-user-instances-work"></a>Como as instâncias de usuário funcionam  

 A primeira vez que uma instância de usuário é gerada para cada usuário, os bancos de dados do sistema **master** e **msdb** são copiados da pasta Dados de Modelo para um caminho no diretório local do repositório de dados do aplicativo do usuário para uso exclusivo pela instância de usuário. O caminho geralmente é `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`. Quando uma instância de usuário é iniciada, o **tempdb**, o log e os arquivos de rastreamento também são gravados neste diretório. Um nome é gerado para a instância, que tem a garantia de ser única para cada usuário.  
  
 Por padrão, todos os membros do grupo Builtin\Users do Windows recebem permissões para conectar-se na instância local, assim como permissões de leitura e execução nos binários do SQL Server. Depois que as credenciais do usuário chamador que hospeda a instância de usuário tiverem sido verificadas, o usuário se tornará o `sysadmin` nessa instância. Somente a memória compartilhada está habilitada para instâncias de usuário, o que significa que são possíveis apenas operações no computador local.  
  
 Os usuários devem receber permissões de leitura e gravação nos arquivos .mdf e .ldf especificados na cadeia de conexão.  
  
> [!NOTE]
> Os arquivos .mdf e .ldf representam o banco de dados e os arquivos de log, respectivamente. Esses dois arquivos são um conjunto correspondente; portanto, tome cuidado durante operações de backup e restauração. O arquivo de banco de dados contém informações sobre a versão exata do arquivo de log. O banco de dados não será aberto se for acoplado com o arquivo de log errado.  
  
 Para evitar dados corrompidos, um banco de dados na instância de usuário é aberto com acesso exclusivo. Se duas instâncias de usuário diferentes compartilharem o mesmo banco de dados no mesmo computador, o usuário na primeira instância deverá fechar o banco de dados antes que ele possa ser aberto em uma segunda instância.  
  
## <a name="user-instance-scenarios"></a>Cenários de instância de usuário  

 As instâncias de usuário fornecem aos desenvolvedores de aplicativos de banco de dados um armazenamento de dados do SQL Server que não depende de os desenvolvedores terem contas administrativas nos computadores de desenvolvimento deles. As instâncias de usuário são baseadas no modelo Access/Jet, em que o aplicativo de banco de dados simplesmente se conecta a um arquivo e o usuário tem automaticamente permissões completas sobre todos os objetos de banco de dados sem precisar de intervenção de um administrador do sistema para conceder permissões. Ele se destina a funcionar em situações nas quais o usuário está em execução em uma LUA (conta de usuário com privilégios mínimos) e não tem privilégios administrativos no servidor ou no computador local, mas que precisa criar aplicativos e objetos de banco de dados. As instâncias de usuário permitem que os usuários criem instâncias em tempo de execução executadas no próprio contexto de segurança do usuário, e não no contexto de segurança de um serviço de sistema com mais privilégios.  
  
> [!IMPORTANT]
> As instâncias de usuário só devem ser usadas em cenários nos quais todos os aplicativos que as usam são totalmente confiáveis.  
  
 Os cenários de instância de usuário incluem:  
  
- Qualquer aplicativo de usuário único em que não é necessário compartilhar dados.  
  
- Implantação do ClickOnce. Se .NET Framework 2,0 (ou posterior) e SQL Server Express já estiverem instalados no computador de destino, o pacote de instalação baixado como resultado de uma ação do ClickOnce pode ser instalado e usado por usuários que não são administradores. Observe que um administrador deverá instalar o SQL Server Express se ele fizer parte da instalação. Para obter mais informações, confira [Implantação do ClickOnce para Windows Forms](/dotnet/desktop/winforms/clickonce-deployment-for-windows-forms).
  
- Hospedagem ASP.NET dedicada usando a Autenticação do Windows. Uma só instância do SQL Server Express pode ser hospedada em uma intranet. O aplicativo se conecta usando a conta do Windows do ASPNET, não usando a representação. As instâncias de usuário não devem ser usadas para cenários de hospedagem compartilhada ou de terceiros em que todos os aplicativos compartilhariam a mesma instância de usuário e não permaneceriam mais isolados uns dos outros.  
  
## <a name="see-also"></a>Consulte também

- [SQL Server e ADO.NET](index.md)
- [Cadeias de conexão](../connection-strings.md)
- [Conectando a uma Fonte de Dados](../connecting-to-a-data-source.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
