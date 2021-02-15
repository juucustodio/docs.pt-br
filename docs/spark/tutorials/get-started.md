---
title: Introdução ao .NET para Apache Spark
description: Descubra como executar um .NET para Apache Spark aplicativo usando o .NET Core no Windows, no macOS e no Ubuntu.
ms.date: 10/09/2020
ms.topic: tutorial
ms.custom: mvc
ms.author: luquinta
author: luisquintanilla
ms.openlocfilehash: 52d37f3c6b4907361bf0933942d8f1757669be24
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99426782"
---
# <a name="tutorial-get-started-with-net-for-apache-spark"></a>Tutorial: introdução ao .NET para Apache Spark

Este tutorial ensina como executar um .NET para Apache Spark aplicativo usando o .NET Core no Windows, no macOS e no Ubuntu.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
>
> * Prepare seu ambiente para .NET para Apache Spark
> * Escreva seu primeiro .NET para Apache Spark aplicativo
> * Crie e execute seu .NET para Apache Spark aplicativo

## <a name="prepare-your-environment"></a>Prepare o seu ambiente

Antes de começar a escrever seu aplicativo, você precisa configurar algumas dependências de pré-requisito. Se você puder executar `dotnet` `java` o,, `spark-shell` no ambiente de linha de comando, seu ambiente já estará preparado e você poderá pular para a próxima seção. Se você não puder executar um ou todos os comandos, execute as etapas a seguir.

### <a name="1-install-net"></a>1. instalar o .NET

Para começar a criar aplicativos .NET, você precisa baixar e instalar o SDK do .NET (Software Development Kit).

Baixe e instale o [SDK do .NET Core](https://dotnet.microsoft.com/download/dotnet-core/3.1). A instalação do SDK adiciona a cadeia de ferramentas `dotnet` a seu caminho.

Depois de instalar o SDK do .NET Core, abra um novo prompt de comando ou terminal e execute `dotnet` .

Se o comando executar e imprimir as informações sobre como usar dotnet, o poderá passar para a próxima etapa. Se você receber um `'dotnet' is not recognized as an internal or external command` erro, verifique se você abriu um **novo** prompt de comando ou terminal antes de executar o comando.

### <a name="2-install-java"></a>2. instalar o Java

Instale o [Java 8,1](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) para Windows e MacOS, ou [OpenJDK 8](https://openjdk.java.net/install/) para Ubuntu.

Selecione a versão apropriada para seu sistema operacional. Por exemplo, selecione **jdk-8u201-windows-x64.exe** para um computador x64 do Windows (como mostrado abaixo) ou **JDK-8u231-MacOSX-x64. dmg** para MacOS. Em seguida, use o comando `java` para verificar a instalação.

![Download do Java](https://dotnet.microsoft.com/static/images/java-jdk-downloads-windows.png?v=6BbJHoNyDO-PyYVciImr5wzh2AW_YHNcyb3p093AwPA)

### <a name="3-install-compression-software"></a>3. instalar o software de compactação

Apache Spark é baixado como um arquivo. tgz compactado. Use um programa de extração, como [7-zip](https://www.7-zip.org/) ou [WinZip](https://www.winzip.com/), para extrair o arquivo.

### <a name="4-install-apache-spark"></a>4. instalar o Apache Spark

[Baixe e instale o Apache Spark](https://spark.apache.org/downloads.html). Você precisará selecionar a partir da versão 2,3. * ou 2.4.0, 2.4.1, 2.4.3, 2.4.4, 2.4.5, 2.4.6, 2.4.7, 3.0.0 ou 3.0.1 (.NET para Apache Spark não é compatível com outras versões do Apache Spark).

Os comandos usados nas etapas a seguir pressupõem que você tenha [baixado e instalado Apache Spark 3.0.1](https://spark.apache.org/downloads.html). Se você quiser usar uma versão diferente, substitua o **3.0.1** pelo número de versão apropriado. Em seguida, extraia o arquivo **. tar** e os arquivos de Apache Spark.

Para extrair o arquivo **. tar** aninhado:

* Localize o arquivo **Spark-3.0.1-bin-Hadoop 2.7. tgz** que você baixou.
* Clique com o botão direito do mouse no arquivo e selecione **7-zip-> extrair aqui**.
* o **Spark-3.0.1-bin-Hadoop 2.7. tar** é criado junto com o arquivo **. tgz** que você baixou.

Para extrair os arquivos de Apache Spark:

* Clique com o botão direito do mouse em **Spark-3.0.1-bin-Hadoop 2.7. tar** e selecione **7-zip-> extrair arquivos...**
* Insira **C:\bin** no campo **extrair para** .
* Desmarque a caixa de seleção abaixo do campo **extrair para** .
* Selecione **OK**.
* Os arquivos de Apache Spark são extraídos para C:\bin\spark-3.0.1-bin-hadoop2.7\

![Instalar Spark](./media/spark-extract-with-7-zip.png)

Execute os comandos a seguir para definir as variáveis de ambiente usadas para localizar Apache Spark. No Windows, certifique-se de executar o prompt de comando no modo de administrador.

#### <a name="windows"></a>[Windows](#tab/windows)

```console
setx /M HADOOP_HOME C:\bin\spark-3.0.1-bin-hadoop2.7\
setx /M SPARK_HOME C:\bin\spark-3.0.1-bin-hadoop2.7\
setx /M PATH "%PATH%;%HADOOP_HOME%;%SPARK_HOME%\bin" # Warning: Don't run this if your path is already long as it will truncate your path to 1024 characters and potentially remove entries!
```

#### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
export SPARK_HOME=~/bin/spark-3.0.1-bin-hadoop2.7/
export PATH="$SPARK_HOME/bin:$PATH"
source ~/.bashrc
```

---

Depois de instalar tudo e definir suas variáveis de ambiente, abra um **novo** prompt de comando ou terminal e execute o seguinte comando:

```text
spark-submit --version
```

Se o comando executar e imprimir as informações de versão, você poderá passar para a próxima etapa.

Se você receber um `'spark-submit' is not recognized as an internal or external command` erro, certifique-se de ter aberto um **novo** prompt de comando.

### <a name="5-install-net-for-apache-spark"></a>5. instalar o .NET para Apache Spark

Baixe a versão [Microsoft. Spark. Worker](https://github.com/dotnet/spark/releases) do .net para Apache Spark github. Por exemplo, se você estiver em um computador Windows e planeja usar o .NET Core, [Baixe a versão Windows x64 netcoreapp 3.1](https://github.com/dotnet/spark/releases).

Para extrair o Microsoft. Spark. Worker:

* Localize o arquivo de **Microsoft.Spark.Worker.netcoreapp3.1.win-x64-1.0.0.zip** que você baixou.
* Clique com o botão direito do mouse e selecione **7-zip-> extrair arquivos...**.
* Insira **C:\bin** no campo **extrair para** .
* Desmarque a caixa de seleção abaixo do campo **extrair para** .
* Selecione **OK**.

### <a name="6-install-winutils-windows-only"></a>6. instalar o WinUtils (somente Windows)

O .NET para Apache Spark requer que o WinUtils seja instalado junto com Apache Spark. [Baixar winutils.exe](https://github.com/steveloughran/winutils/blob/master/hadoop-2.7.1/bin/winutils.exe). Em seguida, copie WinUtils para **C:\bin\spark-3.0.1-bin-hadoop2.7\bin**.

> [!NOTE]
> Se você estiver usando uma versão diferente do Hadoop, que é anotada no final do nome da pasta de instalação do Spark, [Selecione a versão do WinUtils](https://github.com/steveloughran/winutils) que é compatível com sua versão do Hadoop.

### <a name="7-set-dotnet_worker_dir-and-check-dependencies"></a>7. definir DOTNET_WORKER_DIR e verificar dependências

Execute um dos comandos a seguir para definir a `DOTNET_WORKER_DIR` variável de ambiente, que é usada pelos aplicativos .net para localizar o .net para Apache Spark binários de trabalho. Certifique-se de substituir `<PATH-DOTNET_WORKER_DIR>` pelo diretório onde você baixou e extraiu o `Microsoft.Spark.Worker` . No Windows, certifique-se de executar o prompt de comando no modo de administrador.

#### <a name="windows"></a>[Windows](#tab/windows)

```console
setx /M DOTNET_WORKER_DIR <PATH-DOTNET-WORKER-DIR>
```

#### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
export DOTNET_WORKER_DIR=<PATH-DOTNET-WORKER-DIR>
```

---

Por fim, verifique se você pode executar `dotnet` , `java` , `spark-shell` na linha de comando antes de passar para a próxima seção.

## <a name="write-a-net-for-apache-spark-app"></a>Escrever um aplicativo .NET para Apache Spark

### <a name="1-create-a-console-app"></a>1. criar um aplicativo de console

No prompt de comando ou terminal, execute os seguintes comandos para criar um novo aplicativo de console:

```dotnetcli
dotnet new console -o MySparkApp
cd MySparkApp
```

O `dotnet` comando cria um `new` aplicativo do tipo `console` para você. O `-o` parâmetro cria um diretório chamado *MySparkApp* onde seu aplicativo é armazenado e o preenche com os arquivos necessários. O `cd MySparkApp` comando altera o diretório para o diretório do aplicativo que você criou.

### <a name="2-install-nuget-package"></a>2. instalar o pacote NuGet

Para usar o .NET para Apache Spark em um aplicativo, instale o pacote Microsoft. Spark. No prompt de comando ou terminal, execute o seguinte comando:

```dotnetcli
dotnet add package Microsoft.Spark
```

> [!NOTE]
> Este tutorial usa a versão mais recente do `Microsoft.Spark` pacote NuGet, a menos que especificado de outra forma.

### <a name="3-write-your-app"></a>3. Escreva seu aplicativo

Abra *Program.cs* no Visual Studio Code, ou em qualquer editor de texto, e substitua todo o código pelo seguinte:

```csharp
using Microsoft.Spark.Sql;
using static Microsoft.Spark.Sql.Functions;

namespace MySparkApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create Spark session
            SparkSession spark =
                SparkSession
                    .Builder()
                    .AppName("word_count_sample")
                    .GetOrCreate();

            // Create initial DataFrame
            string filePath = args[0];
            DataFrame dataFrame = spark.Read().Text(filePath);

            //Count words
            DataFrame words =
                dataFrame
                    .Select(Split(Col("value")," ").Alias("words"))
                    .Select(Explode(Col("words")).Alias("word"))
                    .GroupBy("word")
                    .Count()
                    .OrderBy(Col("count").Desc());

            // Display results
            words.Show();

            // Stop Spark session
            spark.Stop();
        }
    }
}
```

[SparkSession](xref:Microsoft.Spark.Sql.SparkSession) é o ponto de entrada de aplicativos Apache Spark, que gerencia o contexto e as informações do seu aplicativo. Usando o método [Text](xref:Microsoft.Spark.Sql.DataFrameReader.Text%2A) , os dados de texto do arquivo especificado pelo `filePath` são lidos em um [dataframe](xref:Microsoft.Spark.Sql.DataFrame). Um dataframe é uma maneira de organizar dados em um conjunto de colunas nomeadas. Em seguida, uma série de transformações é aplicada para dividir as frases no arquivo, agrupar cada uma das palavras, contá-las e ordená-las em ordem decrescente. O resultado dessas operações é armazenado em outro dataframe. Observe que neste ponto, nenhuma operação ocorreu porque o .NET para Apache Spark avalia os dados lentamente. Não é até que o método [show](xref:Microsoft.Spark.Sql.DataFrame.Show%2A) seja chamado para exibir o conteúdo do `words` dataframe transformado para o console que as operações definidas nas linhas acima executam. Depois que você não precisar mais da sessão do Spark, use o método [Stop](xref:Microsoft.Spark.Sql.SparkSession.Stop%2A) para interromper a sessão.

### <a name="4-create-data-file"></a>4. criar arquivo de dados

Seu aplicativo processa um arquivo que contém linhas de texto. Crie um arquivo chamado *input.txt* arquivo no diretório *MySparkApp* , contendo o seguinte texto:

```text
Hello World
This .NET app uses .NET for Apache Spark
This .NET app counts words with Apache Spark
```

Salve as alterações e feche o arquivo.

## <a name="run-your-net-for-apache-spark-app"></a>Executar seu aplicativo .NET para Apache Spark

Execute o seguinte comando para compilar seu aplicativo:

```dotnetcli
dotnet build
```

Navegue até o diretório de saída da compilação e use o `spark-submit` comando para enviar seu aplicativo para execução em Apache Spark. Certifique-se de substituir  `<version>` pela versão do seu trabalho do .net e `<path-of-input.txt>` pelo caminho de seu arquivo de *input.txt* está armazenado.

### <a name="windows"></a>[Windows](#tab/windows)

```console
spark-submit ^
--class org.apache.spark.deploy.dotnet.DotnetRunner ^
--master local ^
microsoft-spark-3-0_2.12-<version>.jar ^
dotnet MySparkApp.dll <path-of-input.txt>
```

### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
spark-submit \
--class org.apache.spark.deploy.dotnet.DotnetRunner \
--master local \
microsoft-spark-3-0_2.12-<version>.jar \
dotnet MySparkApp.dll <path-of-input.txt>
```

---

> [!NOTE]
> Esse comando pressupõe que você tenha baixado Apache Spark e adicionado-o à variável de ambiente PATH para poder usar `spark-submit` . Caso contrário, você precisaria usar o caminho completo (por exemplo, *C:\bin\apache-spark\bin\spark-Submit* ou *~/Spark/bin/Spark-Submit*).

Quando seu aplicativo é executado, os dados de contagem de palavras do arquivo de *input.txt* são gravados no console do.

```console
+------+-----+
|  word|count|
+------+-----+
|  .NET|    3|
|Apache|    2|
|   app|    2|
|  This|    2|
| Spark|    2|
| World|    1|
|counts|    1|
|   for|    1|
| words|    1|
|  with|    1|
| Hello|    1|
|  uses|    1|
+------+-----+
```

Parabéns! Você criou e executou com êxito um aplicativo .NET para Apache Spark.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
>
> * Prepare seu ambiente para .NET para Apache Spark
> * Escreva seu primeiro .NET para Apache Spark aplicativo
> * Crie e execute seu .NET para Apache Spark aplicativo

Para ver um vídeo explicando as etapas acima, confira a [série de vídeos .net para Apache Spark 101](https://channel9.msdn.com/Series/NET-for-Apache-Spark-101/Run-Your-First-NET-for-Apache-Spark-App).

Confira a página de recursos para saber mais.
> [!div class="nextstepaction"]
> [Recursos do .NET para Apache Spark](../resources/index.md)
