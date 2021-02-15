---
title: Conectar .NET para Apache Spark a SQL Server
description: Saiba como se conectar a uma instância de SQL Server de seu aplicativo .NET para Apache Spark.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 1fecd796aeefd6c5681c4c2ea623e89f3a5a3c1d
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94439528"
---
# <a name="connect-net-for-apache-spark-to-sql-server"></a>Conectar .NET para Apache Spark a SQL Server

Neste artigo, você aprenderá a se conectar a uma instância do SQL Server de seu aplicativo [.net para Apache Spark](https://github.com/dotnet/spark) .

## <a name="configure-sql-server-to-grant-your-application-access"></a>Configurar SQL Server para conceder acesso ao aplicativo

1. Adicione um usuário e senha de logon escolhendo SQL Server autenticação para sua instância do SQL Server.
2. Conceda permissões necessárias ao usuário de logon no nível de banco de dados relevante, conforme mostrado abaixo:

    ![Permissões do SQL Server](./media/connect-external-sources/SqlServerAuth.png)

3. Verifique se a porta padrão para SQL Server `1433` é permitida por meio do firewall.
4. Abra o SQL configure Manager para habilitar o TCP/IP por meio da configuração de rede, conforme mostrado abaixo:

    ![Habilitar SQL Server TCP/IP](./media/connect-external-sources/SqlServerTCPIP.png)

    Observe também o valor de **escutar tudo** na guia acima, em **protocolo**.

5. Configure a porta TCP/IP para 1433 para todos os endereços IP necessários se o `Listen All` for definido como `No` . Caso contrário, defina a porta TCP em IPAll.

    ![SQL Server porta TCP/IP](./media/connect-external-sources/SQLServerTCPIIPPort.png)

## <a name="connect-to-sql-server-from-your-application"></a>Conectar-se a SQL Server do seu aplicativo

1. Use o Microsoft JDBC Driver para SQL Server para fornecer conectividade de banco de dados por meio de seu aplicativo (Baixe deste [site oficial](/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)).
2. Defina as seguintes configurações para se conectar à instância do SQL Server e ao banco de dados do seu aplicativo:
    1. **connection_url** : essa é a URL usada para se conectar à instância/banco de dados do SQL Server e tem o seguinte formato:

        ```
        jdbc:sqlserver://<SQL_server_IP_address>:1433;instanceName=<instance_name>;databaseName=<database_name>;
        ```

    2. **DBTABLE** : nome da tabela que está sendo acessada.
    3. **usuário** : logon de usuário configurado na etapa 1 de configuração do SQL Server.
    4. **senha** : senha do usuário configurada na etapa 1 de configuração do SQL Server.
3. Use a configuração acima no código do aplicativo para ler os dados de uma tabela, conforme mostrado abaixo:

    ```csharp
    static void Main()
    {
        SparkSession spark = SparkSession
            .Builder()
            .AppName("Connect to SQL Server")
            .GetOrCreate();

        string connection_url = "<URL to connect to SQL server instance>";
        string dbtable = "<database table to access>";
        string user = "<Login user name>";
        string password = "<Login user password>";

        DataFrame jdbcDF = spark.Read()
            .Format("jdbc")
            .Option("driver", "com.microsoft.sqlserver.jdbc.SQLServerDriver")
            .Option("url", connection_url)
            .Option("dbtable", dbtable)
            .Option("user", user)
            .Option("password", password).Load();
        jdbcDF.Show(); // Displays the content of the SQL table as a DataFrame
    }
    ```
