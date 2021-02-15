---
title: Compilar um aplicativo .NET para Apache Spark no Ubuntu
description: Saiba como criar seu .NET para Apache Spark aplicativo no Ubuntu
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 77daad7298c41d21054db9174f30a8d1ed12648d
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94687786"
---
# <a name="learn-how-to-build-your-net-for-apache-spark-application-on-ubuntu"></a>Saiba como criar seu .NET para Apache Spark aplicativo no Ubuntu

Este artigo ensina como criar seu .NET para aplicativos Apache Spark no Ubuntu.

## <a name="prerequisites"></a>Pré-requisitos

Se você já tiver todos os pré-requisitos a seguir, pule para as etapas de [compilação](#build) .

1. Baixar e instalar o **[SDK do .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)** -a instalação do SDK adiciona o `dotnet` ferramentas ao seu caminho.  Há suporte para o .NET Core 2,1, 2,2 e 3,1.

2. Instale o **[OpenJDK 8](https://openjdk.java.net/install/)**.

   - Você pode usar o seguinte comando:

   ```bash
   sudo apt install openjdk-8-jdk
   ```

   * Verifique se você pode executar a `java` partir de sua linha de comando.

      Saída de exemplo de versão Java:

      ```bash
      openjdk version "1.8.0_191"
      OpenJDK Runtime Environment (build 1.8.0_191-8u191-b12-2ubuntu0.18.04.1-b12)
      OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)
      ```

   * Se você já tiver várias versões do OpenJDK instaladas e quiser selecionar o OpenJDK 8, use o seguinte comando:

      ```bash
      sudo update-alternatives --config java
      ```

3. Instale o **[Apache Maven 3.6.0 +](https://maven.apache.org/download.cgi)**.

   * Execute o seguinte comando:

      ```bash
      mkdir -p ~/bin/maven
      cd ~/bin/maven
      wget https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
      tar -xvzf apache-maven-3.6.0-bin.tar.gz
      ln -s apache-maven-3.6.0 current
      export M2_HOME=~/bin/maven/current
      export PATH=${M2_HOME}/bin:${PATH}
      source ~/.bashrc
      ```

       Observe que essas variáveis de ambiente serão perdidas quando você fechar o terminal. Se você quiser que as alterações sejam permanentes, adicione as `export` linhas ao `~/.bashrc` arquivo.

   * Verifique se você pode executar a `mvn` partir de sua linha de comando

       Exemplo de saída MVN-Version:

       ```output
       Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T18:41:47Z)
       Maven home: ~/bin/apache-maven-3.6.0
       Java version: 1.8.0_191, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
       Default locale: en, platform encoding: UTF-8
       OS name: "linux", version: "4.4.0-17763-microsoft", arch: "amd64", family: "unix"
       ```

4. Instale o **[Apache Spark 2.3 +](https://spark.apache.org/downloads.html)**.
Baixe [Apache Spark 2.3 +](https://spark.apache.org/downloads.html) e extraia-o em uma pasta local (por exemplo, `~/bin/spark-3.0.1-bin-hadoop2.7` ). (As versões do Spark com suporte são 2,3. *, 2.4.0, 2.4.1, 2.4.3, 2.4.4, 2.4.5, 2.4.6, 2.4.7, 3.0.0 e 3.0.1)

   ```bash
   tar -xvzf /path/to/spark-3.0.1-bin-hadoop2.7.tgz -C ~/bin/spark-3.0.1-bin-hadoop2.7
   ```

   * Adicionar as [variáveis de ambiente](https://www.java.com/en/download/help/path.xml) necessárias `SPARK_HOME` (por exemplo, `~/bin/spark-3.0.1-bin-hadoop2.7/` ) e `PATH` (por exemplo, `$SPARK_HOME/bin:$PATH` )

      ```bash
      export SPARK_HOME=~/bin/spark-3.0.1-hadoop2.7
      export PATH="$SPARK_HOME/bin:$PATH"
      source ~/.bashrc
      ```

      Observe que essas variáveis de ambiente serão perdidas quando você fechar o terminal. Se você quiser que as alterações sejam permanentes, adicione as `export` linhas ao `~/.bashrc` arquivo.

   * Verifique se você pode executar a `spark-shell` partir de sua linha de comando.

      Exemplo de saída do console:

      ```
      Welcome to
            ____              __
           / __/__  ___ _____/ /__
          _\ \/ _ \/ _ `/ __/  '_/
         /___/ .__/\_,_/_/ /_/\_\   version 3.0.1
            /_/

      Using Scala version 2.12.10 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_201)
      Type in expressions to have them evaluated.
      Type :help for more information.

      scala> sc
      res0: org.apache.spark.SparkContext = org.apache.spark.SparkContext@6eaa6b0c
      ```

Verifique se você pode executar `dotnet` o,, `java` `mvn` , `spark-shell` de sua linha de comando antes de passar para a próxima seção. Existe uma maneira melhor? [Abra um problema](https://github.com/dotnet/spark/issues) e sinta-se à vontade para contribuir.

## <a name="build"></a>Build

Para o restante deste guia, você precisará ter clonado o .NET para o repositório Apache Spark em seu computador, por exemplo, `~/dotnet.spark/` .

```bash
git clone https://github.com/dotnet/spark.git ~/dotnet.spark
```

### <a name="build-net-for-spark-scala-extensions-layer"></a>Compilar .NET para camada de extensões do Spark escalares

Quando você envia um aplicativo .NET, o .NET for Apache Spark tem a lógica necessária escrita em escalares que informa Apache Spark como lidar com suas solicitações (por exemplo, solicitação para criar uma nova sessão do Spark, solicitação para transferir dados do lado do .NET para o lado da JVM, etc.). Essa lógica pode ser encontrada no [código-fonte escalar do .net para Apache Spark](https://github.com/dotnet/spark/tree/master/src/scala).

A próxima etapa é criar o .NET para Apache Spark camada de extensão escalabilidade:

```bash
cd src/scala
mvn clean package
```

Você deve ver os JARs criados para as versões do Spark com suporte:

* `microsoft-spark-2-3\target\microsoft-spark-2-3_2.11-<spark-dotnet-version>.jar`
* `microsoft-spark-2-4\target\microsoft-spark-2-4_2.11-<spark-dotnet-version>.jar`
* `microsoft-spark-3-0\target\microsoft-spark-3-0_2.12-<spark-dotnet-version>.jar`

### <a name="build-net-sample-applications-using-net-core-cli"></a>Crie aplicativos de exemplo .NET usando o CLI do .NET Core

Esta seção explica como criar os [aplicativos de exemplo](https://github.com/dotnet/spark/tree/master/examples) para .net para Apache Spark. Essas etapas ajudarão a compreender o processo de criação geral de qualquer aplicativo .NET para Spark.

1. Crie o trabalho:

   ```dotnetcli
   cd ~/dotnet.spark/src/csharp/Microsoft.Spark.Worker/
   dotnet publish -f netcoreapp3.1 -r ubuntu.18.04-x64
   ```

   Exemplo de saída do console:

   ```bash
   user@machine:/home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker$ dotnet publish -f netcoreapp3.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.6.0+5ff7b0c9e for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 36.03 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker/Microsoft.Spark.Worker.csproj.
      Restore completed in 35.94 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.1/Microsoft.Spark.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish/Microsoft.Spark.Worker.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish/
   ```

2. Compile os exemplos:

   ```dotnetcli
   cd ~/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/
   dotnet publish -f netcoreapp3.1 -r ubuntu.18.04-x64
   ```

   Exemplo de saída do console:

   ```bash
   user@machine:/home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples$ dotnet publish -f netcoreapp3.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.6.0+5ff7b0c9e for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 37.11 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Restore completed in 281.63 ms for /home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/Microsoft.Spark.CSharp.Examples.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.1/Microsoft.Spark.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish/Microsoft.Spark.CSharp.Examples.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish/
   ```  

## <a name="run-the-net-for-spark-sample-applications"></a>Executar o .NET para aplicativos de exemplo do Spark

Depois de criar os exemplos, você pode usar o `spark-submit` para enviar seus aplicativos .NET Core. Verifique se você seguiu a seção de [pré-requisitos](#prerequisites) e instalou o Apache Spark.

1. Defina a `DOTNET_WORKER_DIR` `PATH` variável de ambiente ou para incluir o caminho em que o `Microsoft.Spark.Worker` binário foi gerado (por exemplo, `~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish` ).

   ```bash
   export DOTNET_WORKER_DIR=~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish
   ```

2. Abra um terminal e vá para o diretório em que o binário do aplicativo foi gerado (por exemplo, `~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish` ).

   ```bash
   cd ~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp3.1/ubuntu.18.04-x64/publish
   ```

3. A execução do aplicativo segue a estrutura básica:

   ```bash
   spark-submit \
     [--jars <any-jars-your-app-is-dependent-on>] \
     --class org.apache.spark.deploy.dotnet.DotnetRunner \
     --master local \
     <path-to-microsoft-spark-jar> \
     <path-to-your-app-binary> <argument(s)-to-your-app>
   ```

   Aqui estão alguns exemplos que você pode executar:

   * **[Microsoft.Spark.Examples.Sql.Batch. Basic](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Batch/Basic.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Batch.Basic $SPARK_HOME/examples/src/main/resources/people.json
      ```

   * **[Microsoft. Spark. examples. Sql. streaming. StructuredNetworkWordCount](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredNetworkWordCount.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredNetworkWordCount localhost 9999
      ```

   * **[Microsoft. Spark. examples. Sql. streaming. StructuredKafkaWordCount (com acesso ao Maven)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.2 \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
      ```

   * **[Microsoft. Spark. examples. Sql. streaming. StructuredKafkaWordCount (jars fornecidos)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --jars path/to/net.jpountz.lz4/lz4-1.3.0.jar,path/to/org.apache.kafka/kafka-clients-0.10.0.1.jar,path/to/org.apache.spark/spark-sql-kafka-0-10_2.11-2.3.2.jar,`path/to/org.slf4j/slf4j-api-1.7.6.jar,path/to/org.spark-project.spark/unused-1.0.0.jar,path/to/org.xerial.snappy/snappy-java-1.1.2.6.jar \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
       ```
