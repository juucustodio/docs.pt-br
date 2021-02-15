---
title: Conectar-se ao armazenamento remoto do computador local
description: Conecte-se às contas de armazenamento do Azure usando .NET para Apache Spark do computador local.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: dc0c3b44279756596f3d456616821e690710ae04
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224012"
---
# <a name="connect-to-azure-data-lake-storage-gen-2-or-wasb-account"></a>Conectar-se à conta do Azure Data Lake Storage Gen 2 ou WASB

Neste artigo, você aprende a se conectar a uma conta do Azure Data Lake Storage (ADLS) Gen 2 ou do Windows Azure Storage Blob (WASB) por meio de uma instância do [.net para Apache Spark](https://github.com/dotnet/spark) em execução localmente em seu computador Windows.

## <a name="set-up-the-environment"></a>Configurar o ambiente

1. Baixe a distribuição Apache Spark compilada sem Hadoop do [site oficial](https://archive.apache.org/dist/spark/) (escolha uma versão [com suporte do .net para Apache Spark](https://github.com/dotnet/spark#supported-apache-spark)) e extraia-a em um diretório. Defina a variável de ambiente `SPARK_HOME` para esse diretório.
2. Baixe o binário Apache Hadoop [aqui](http://hadoop.apache.org/releases.html) e extraia-o para uma pasta e defina a `HADOOP_HOME` variável de ambiente para essa pasta.
3. Baixe os `winutils.exe` `hadoop.dll` arquivos e deste [local](https://github.com/cdarlint/winutils) (dependendo da versão do Hadoop instalada na etapa anterior) e coloque-os na pasta bin do seu Hadoop. Esses binários são necessários no Windows para que tudo seja configurado corretamente (isso é explicado em detalhes no [wiki do Apache aqui](https://cwiki.apache.org/confluence/display/HADOOP2/WindowsProblems)).
4. Configure a instalação do Hadoop fazendo as seguintes alterações no `%HADOOP_HOME%\etc\hadoop\hadoop-env.cmd` arquivo:
    1. Defina a `JAVA_HOME` propriedade usando o caminho dos (já que o Hadoop não gosta de espaços em `JAVA_HOME` ). Isso deve ser semelhante a este: `C:\Progra~1\Java\jdk1.8.0_241` (apontando para qualquer versão do Java que você tenha instalado em seu computador local).
    2. Anexar `%HADOOP_HOME%\share\hadoop\tools\lib\*` a `HADOOP_CLASSPATH` .
    O `hadoop-env.cmd` arquivo final deve ser semelhante a este:

    ![Arquivo Hadoop-env. cmd final](./media/connect-external-sources/hadoop-env.png)

## <a name="configure-your-storage-account-in-hadoop"></a>Configurar sua conta de armazenamento no Hadoop

1. Abra a conta de armazenamento ADLS Gen 2 ou WASB à qual você deseja se conectar por meio da [portal do Azure](https://portal.azure.com) e abra o painel **chaves de acesso** na folha **configurações** e copie o valor da **chave** de em key1.
2. Agora, para configurar o Hadoop para acessar sua conta de ADLS Gen2, você precisaria editar seu `core-site.xml` arquivo (localizado em `%HADOOP_HOME%\etc\hadoop\` ) que contém a configuração em todo o cluster. Adicione as seguintes propriedades dentro das `<configuration>` marcas neste arquivo:

    ```xml
    <configuration>
      <property>
        <name>fs.azure.account.auth.type.YOUR_ACCOUNT_NAME.dfs.core.windows.net</name>
        <value>SharedKey</value>
        <description></description>
      </property>
      <property>
        <name>fs.azure.account.key.YOUR_ACCOUNT_NAME.dfs.core.windows.net</name>
        <value>YOUR ACCESS KEY (copied from Step 1)</value>
        <description>The secret password. Never share these.</description>
      </property>
    </configuration>
    ```

    Se você estiver tentando se conectar a uma conta do WASB, substitua `dfs` por `blob` nos nomes de propriedade. Por exemplo, `fs.azure.account.auth.type.YOUR_ACCOUNT_NAME.blob.core.windows.net`.
3. Você pode testar a conectividade com sua conta de armazenamento do Hadoop executando o seguinte comando em seu `%HADOOP_HOME%` diretório:

    ```bash
    bin\hdfs dfs -ls <URI to your account>
    ```

Isso deve exibir uma lista de todos os arquivos/pastas no caminho fornecido pelo URI.

> [!NOTE]
> O formato para derivar o URI para sua conta de armazenamento é o seguinte:
>
> ```
> For ADLS: abfs[s]://<file_system>@<account_name>.dfs.core.windows.net/<path>/<file_name>
> For WASB: wasb[s]://<file_system>@<account_name>.blob.core.windows.net/<path>/<file_name>
> ```

## <a name="connect-to-your-storage-account"></a>Conectar-se à sua conta de armazenamento

1. Se o comando acima funcionou, agora você pode passar para acessar essa conta de armazenamento por meio do Spark. Primeiro, execute o comando a `hadoop classpath` partir da linha de comando dentro `%HADOOP_HOME%` e copie a saída.
2. Defina a saída do comando executado na etapa 1 para o valor da variável de ambiente `SPARK_DIST_CLASSPATH` .
3. Agora você deve ser capaz de acessar sua conta de armazenamento do ADLS ou WASB por meio do Spark .NET usando o URI do abfs, conforme mostrado no exemplo simples abaixo. (Para este exemplo, usamos o [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) arquivo de exemplo padrão fornecido com cada instalação de Apache Spark.):

    ```csharp
    SparkSession spark = SparkSession
       .Builder()
       .AppName("Connect to Azure Storage locally")
       .GetOrCreate();
    DataFrame df = spark.Read().Json("wasbs://file_system@account_name.blob.core.windows.net/path/people.json");
    //DataFrame df = spark.Read().Json("abfss://file_system@account_name.dfs.core.windows.net/path/file.json");
    df.Show();
    ```

    O resultado, conforme exibido, é o dataframe ( `df` ), conforme mostrado abaixo:

    ```text
    +----+-------+
    | age|   name|
    +----+-------+
    |null|Michael|
    |  30|   Andy|
    |  19| Justin|
    +----+-------+
    ```
