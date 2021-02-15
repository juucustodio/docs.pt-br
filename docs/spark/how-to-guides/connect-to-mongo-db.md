---
title: Conectar o .NET para Apache Spark ao MongoDB
description: Saiba como se conectar à sua instância do MongoDB de seu aplicativo .NET para Apache Spark.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 3889088ce32046f72a9a3392e28a5a36cda4745e
ms.sourcegitcommit: 7e42488c2f8f63f6d499b5f8fb1dec5bac9ad254
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98957839"
---
# <a name="connect-net-for-apache-spark-to-mongodb"></a>Conectar o .NET para Apache Spark ao MongoDB

Neste artigo, você aprenderá a se conectar a uma instância do MongoDB de seu aplicativo .NET para Apache Spark.

## <a name="prerequisites"></a>Prerequisites

- Ter um servidor MongoDB em funcionamento com um [banco de dados e alguma coleção](https://docs.mongodb.com/manual/core/databases-and-collections/) adicionada a ele (Baixe [este servidor da Comunidade](https://www.mongodb.com/try/download/community) para um servidor local ou experimente o [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) para um serviço MongoDB na nuvem).

## <a name="set-up-your-mongodb-instance"></a>Configurar sua instância do MongoDB

Para obter o .NET para Apache Spark se comunicar com sua instância do MongoDB, você precisa verificar se ele está configurado corretamente fazendo o seguinte:

1. Crie um nome de usuário e uma senha para o seu aplicativo se conectar e forneça ao usuário as permissões/funções necessárias usando o seguinte comando por meio do Shell Mongo:

    ```bash
    use database
    db.createUser(
      {
        user: "mySparkUser",
        pwd: "<password>",
        roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
      }
    )
    ```

2. Verifique se o endereço IP do computador no qual seu .NET para Apache Spark aplicativo está em execução é allowlisted para o servidor MongoDB ser capaz de se conectar. Você pode consultar [este guia](https://docs.atlas.mongodb.com/security/add-ip-address-to-list/) para saber como fazer isso.

## <a name="configure-your-net-for-apache-spark-application"></a>Configurar seu .NET para Apache Spark aplicativo

1. Tenha as seguintes variáveis definidas para configurar seu aplicativo para se comunicar com a instância do MongoDB e ler de uma coleção.
    1. **authURI**: "cadeia de conexão que autoriza seu aplicativo a se conectar à instância necessária do MongoDB". O formato para isso é o seguinte:

        ```
        "mongodb+srv://<username>:<password>@<cluster_address>/<database>.<collection>"
        ```

    2. **nome** de usuário: nome de usuário da conta que você criou na etapa 1 da seção anterior
    3. **senha**: senha da conta de usuário criada
    4. **cluster_address**: nome de host/endereço do seu cluster MongoDB
    5. **banco de dados**: o banco de dados MongoDB ao qual você deseja se conectar
    6. **coleção**: a coleção do MongoDB que você deseja ler. (Para este exemplo, usamos o [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) arquivo de exemplo padrão fornecido com cada instalação do Apache Spark.)

2. Use o `com.mongodb.spark.sql.DefaultSource` formato `spark.Read()` como mostrado abaixo em um trecho de código simples:

    ```csharp
    class Program
    {
        static void Main()
        {
            var authURI = "mongodb+srv://<username>:<password>@<cluster_address>/<database>.<collection>?retryWrites=true&w=majority";
            SparkSession spark = SparkSession
                .Builder()
                .AppName("Connect to Mongo DB example")
                .Config("spark.mongodb.input.uri", authURI)
                .GetOrCreate();

            DataFrame df = spark.Read().Format("com.mongodb.spark.sql.DefaultSource").Load();
            df.PrintSchema();
            df.Show();
            spark.Stop();
        }
    }
    ```

## <a name="run-your-application"></a>Execute seu aplicativo.

Para executar seu .NET para Apache Spark aplicativo, você deve definir o `mongo-spark-connector` módulo como parte da definição de compilação em seu projeto do Spark, usando o `libraryDependency` no `build.sbt` para projetos SBT. Para ambientes do Spark, como `spark-submit` (ou `spark-shell` ), use a `--packages` opção de linha de comando da seguinte forma:

```bash
spark-submit --master local --packages org.mongodb.spark:mongo-spark-connector_2.12:3.0.0 --class org.apache.spark.deploy.dotnet.DotnetRunner microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar yourApp.exe
```

> [!NOTE]
> Certifique-se de incluir a versão do pacote de acordo com a versão do Spark em execução.

O resultado, conforme exibido, é o dataframe ( `df` ) mostrado aqui:

```text
+--------------------+----+-------+
|                 _id| age|   name|
+--------------------+----+-------+
|[5f7c28438029a134...|null|Michael|
|[5f7c287f8029a134...|  30|   Andy|
|[5f7c289a8029a134...|  19| Justin|
+--------------------+----+-------+
```
