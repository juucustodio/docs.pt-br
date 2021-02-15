---
title: Implantar um aplicativo .NET para Apache Spark no Amazon EMR Spark
description: Descubra como implantar um aplicativo do .NET para Apache Spark no Amazon EMR Spark.
ms.date: 10/09/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: dd1cfdf12266b55d9dbc0210479b89ba68c59a38
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688066"
---
# <a name="deploy-a-net-for-apache-spark-application-to-amazon-emr-spark"></a>Implantar um aplicativo .NET para Apache Spark no Amazon EMR Spark

Este tutorial ensina a implantar um aplicativo do .NET para Apache Spark no Amazon EMR Spark. O [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html) é uma plataforma de cluster gerenciada que simplifica a execução de estruturas de Big Data na AWS.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
>
> * Preparar o Microsoft.Spark.Worker
> * Publicar seu aplicativo Spark .NET
> * Implantar seu aplicativo no Amazon EMR Spark
> * Executar o aplicativo

> [!Note]
> O AWS EMR Spark é baseado em Linux. Portanto, se você estiver interessado em implantar seu aplicativo no AWS EMR Spark, verifique se seu aplicativo é .NET Standard compatível e se você usa o compilador .NET Core para compilar seu aplicativo.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, faça o seguinte:

* Baixe a [CLI da AWS](https://aws.amazon.com/cli/).
* Baixe o [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh) para seu computador local. Esse é um script auxiliar que você usa posteriormente para copiar arquivos dependentes do .NET para Apache Spark para os nós de trabalho do cluster do Spark.

## <a name="prepare-worker-dependencies"></a>Preparar dependências de trabalho

O **Microsoft.Spark.Worker** é um componente de back-end que reside nos nós de trabalho individuais do seu cluster do Spark. Quando você deseja executar uma UDF em C# (função definida pelo usuário), o Spark precisa entender como iniciar o .NET CLR para executar o UDF. O **Microsoft.Spark.Worker** fornece uma coleção de classes para o Spark que habilitam essa funcionalidade.

1. Selecione uma versão do netcoreapp do Linux do [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) para ser implantada em seu cluster.

   Por exemplo, se você quiser `.NET for Apache Spark v1.0.0` usar `netcoreapp3.1` o, você baixará [Microsoft. Spark. Worker. netcoreapp 3.1. Linux-x64-1.0.0. tar. gz](https://github.com/dotnet/spark/releases/download/v1.0.0/Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-1.0.0.tar.gz).

2. Carregue `Microsoft.Spark.Worker.<release>.tar.gz` e [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh) para um sistema de arquivos distribuído (por exemplo, S3) ao qual seu cluster tem acesso.

## <a name="prepare-your-net-for-apache-spark-app"></a>Preparar seu aplicativo .NET para Apache Spark

1. Siga o tutorial de [Introdução](get-started.md) para compilar seu aplicativo.

2. Publique seu aplicativo .NET do Spark como independente.

   Execute o comando a seguir no Linux.

   ```dotnetcli
   dotnet publish -c Release -f netcoreapp3.1 -r ubuntu.16.04-x64
   ```

3. Produza `<your app>.zip` para os arquivos publicados.

   Execute o comando a seguir no Linux usando `zip`.

   ```bash
   zip -r <your app>.zip .
   ```

4. Carregue os seguintes itens para um sistema de arquivos distribuído (por exemplo, S3) ao qual seu cluster tem acesso:

   * `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar`: Esse jar é incluído como parte do pacote NuGet do [Microsoft. Spark](https://www.nuget.org/packages/Microsoft.Spark/) e é colocado no diretório de saída da compilação do seu aplicativo.
   * `<your app>.zip`
   * Arquivos (como arquivos de dependência ou dados comuns acessíveis a cada trabalho) ou assemblies (como DLLs que contêm suas funções definidas pelo usuário ou bibliotecas das quais seu aplicativo depende) serão colocados no diretório de trabalho de cada executor.

## <a name="deploy-to-amazon-emr-spark"></a>Implantar no Amazon EMR Spark

O [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html) é uma plataforma de cluster gerenciada que simplifica a execução de estruturas de Big Data na AWS.

> [!NOTE]
> O Amazon EMR Spark é baseado em Linux. Portanto, se você estiver interessado em implantar seu aplicativo no Amazon EMR Spark, verifique se seu aplicativo é compatível com o .Net Standard e se você usa o [compilador do .NET Core](https://dotnet.microsoft.com/download) para compilar seu aplicativo.

### <a name="deploy-microsoftsparkworker"></a>Implantar o Microsoft.Spark.Worker

Esta etapa só é necessária na criação do cluster.

Execute `install-worker.sh` durante a criação do cluster usando [Ações de Inicialização](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html).

Execute o seguinte comando no Linux usando a CLI da AWS.

```bash
aws emr create-cluster \
--name "Test cluster" \
--release-label emr-5.23.0 \
--use-default-roles \
--ec2-attributes KeyName=myKey \
--applications Name=Spark \
--instance-count 3 \
--instance-type m1.medium \
--bootstrap-actions Path=s3://mybucket/<some dir>/install-worker.sh,Name="Install Microsoft.Spark.Worker",Args=["aws","s3://mybucket/<some dir>/Microsoft.Spark.Worker.<release>.tar.gz","/usr/local/bin"]
```

## <a name="run-your-app"></a>Executar o aplicativo

Há duas maneiras de executar seu aplicativo no Amazon EMR Spark: spark-submit e Etapas do Amazon EMR.

### <a name="use-spark-submit"></a>Usar spark-submit

Você pode usar o comando [spark-submit](https://spark.apache.org/docs/latest/submitting-applications.html) para enviar trabalhos do .NET para Apache Spark para o Amazon EMR Spark.

1. `ssh` em um dos nós no cluster.

2. Execute `spark-submit`.

   ```bash
   spark-submit \
   --master yarn \
   --class org.apache.spark.deploy.dotnet.DotnetRunner \
   --files <comma-separated list of assemblies that contain UDF definitions, if any> \
   s3://mybucket/<some dir>/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar \
   s3://mybucket/<some dir>/<your app>.zip <your app> <app args>
   ```

### <a name="use-amazon-emr-steps"></a>Usar as etapas do Amazon EMR

As [Etapas do Amazon EMR](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-submit-step.html) podem ser usadas para enviar trabalhos para a estrutura do Spark instalada no cluster EMR.

Execute o seguinte comando no Linux usando a CLI da AWS.

```bash
aws emr add-steps \
--cluster-id j-xxxxxxxxxxxxx \
--steps Type=spark,Name="Spark Program",Args=[--master,yarn,--files,s3://mybucket/<some dir>/<udf assembly>,--class,org.apache.spark.deploy.dotnet.DotnetRunner,s3://mybucket/<some dir>/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar,s3://mybucket/<some dir>/<your app>.zip,<your app>,<app arg 1>,<app arg 2>,...,<app arg n>],ActionOnFailure=CONTINUE
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você implantou seu aplicativo .NET para Apache Spark para o Amazon EMR Spark. Para exemplos de projetos do .NET para Apache Spark, continue no GitHub.

> [!div class="nextstepaction"]
> [Exemplos do .NET para Apache Spark](https://github.com/dotnet/spark/tree/master/examples)
