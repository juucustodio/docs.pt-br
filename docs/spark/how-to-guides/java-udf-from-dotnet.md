---
title: Invocar UDFs Java do .NET para Apache Spark aplicativo
description: Saiba como chamar um UDF Java de um aplicativo .NET para Apache Spark.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 17f0ff611e68a5dab2032f78ef75912f314d88a5
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688261"
---
# <a name="call-a-java-udf-from-your-net-for-apache-spark-application"></a>Chamar um UDF Java de seu aplicativo .NET para Apache Spark

Neste artigo, você aprenderá a chamar uma UDF (função de User-Defined Java) de seu aplicativo [.net para Apache Spark](https://github.com/dotnet/spark) .

1. Como definir seus UDFs Java e compilá-los em um jar – essa etapa não será necessária se você já tiver um UDF definido em um arquivo jar. Nesse caso, tudo o que você precisa é o nome completo da função UDF, incluindo o pacote.
2. Registre e chame seu UDF Java em seu aplicativo .NET para Apache Spark.

## <a name="define-and-compile-your-java-udfs"></a>Definir e compilar suas UDFs Java

1. Crie um projeto Maven ou SBT e adicione as seguintes dependências ao arquivo de configuração do projeto:
    1. `org.apache.spark.spark-core_2.11.<version>`
    2. `org.apache.spark.spark-sql_2.11.<version>`
2. Defina seu UDF Java implementando a [interface relevante](https://github.com/apache/spark/blob/master/sql/core/src/main/java/org/apache/spark/sql/api/java/UDF1.java) (de acordo com a assinatura de UDF) e importando o pacote relevante, conforme mostrado abaixo em um exemplo simples

    ```java
    package com.ScalaUdf.app; // Name of package where UDF is defined
    import org.apache.spark.sql.api.java.UDF1; // UDF interface to implement

    public class JavaUdf implements UDF1<Integer, Integer> { // Name of the Java UDF
        private static final int serialVersionUID = 1;
        @Override
        public Integer call(Integer num) throws Exception { // Define logic of UDF
            return (num + 5);
        }
    }
    ```

3. Compile e empacote seu projeto para criar e o JAR executável digamos `UdfApp-0.0.1.jar` .

## <a name="register-and-call-java-udfs-in-net-for-apache-spark"></a>Registrar e chamar UDFs Java no .NET para Apache Spark

1. Use a [`RegisterJava`](https://github.com/dotnet/spark/blob/8dcdcdc7c60d5f42cba5a90f1346d854ab5bf7bb/src/csharp/Microsoft.Spark/Sql/UDFRegistration.cs#L424) API para registrar seu UDF Java com o Spark SQL.
2. Registre o `DataFrame` no qual você deseja chamar o UDF como uma tabela SQL usando a [`CreateOrReplaceTempView`](https://github.com/dotnet/spark/blob/master/src/csharp/Microsoft.Spark/Sql/DataFrame.cs#L982) função.
3. Use `SparkSession.Sql` para chamar o UDF na exibição de tabela usando o Spark SQL.
Um exemplo básico para ilustrar as etapas acima:

    ```csharp
    class Program
    {
        static void Main()
        {
            SparkSession spark = SparkSession
                .Builder()
                .AppName("Scala/Java UDFs from .NET for Apache Spark")
                .GetOrCreate();
            spark.Udf().RegisterJava<int>("udfAdd5", "com.ScalaUdf.app.JavaUdf"); // Register your Java UDF as 'udfAdd5'
            DataFrame df = spark.CreateDataFrame(new int[] { 2, 5 });
            df.CreateOrReplaceTempView("numbersData"); // Create an SQL table from the DataFrame `df`
            DataFrame dfUdf = spark.Sql("SELECT udfAdd5(_1) As Result FROM numbersData"); // Call the registered UDF on the table
            dfUdf.Show();
            spark.Stop();
        }
    }
    ```

4. Envie este aplicativo usando `spark-submit` passando o jar Java UDF compilado anteriormente por meio da `--jars` opção:

    ```bash
    spark-submit --master local --jars UdfApp-0.0.1.jar --class org.apache.spark.deploy.dotnet.DotnetRunner microsoft-spark-2-4_2.11-1.0.0.jar InterRuntimeUDFs.exe
    ```

    O `dfUdf` dataframe resultante tinha o número 5 adicionado a cada linha da coluna de entrada, conforme definido por `JavaUdf` :

    ```text
    +-------+
    | Result|
    +-------+
    |      7|
    |     10|
    +-------+
    ```

## <a name="call-net-udf-from-scala-or-python-in-apache-spark"></a>Chamar UDF .NET de escala ou Python no Apache Spark

Você também pode registrar e invocar um UDF em C# de um aplicativo Apache Spark escrito em escala ou Python usando [a ferramenta de código aberto sparkdotnetudf](https://github.com/imback82/sparkdotnetudf).
