---
title: Usar o Jupyter Notebooks
titleSuffix: .NET for Apache Spark
description: Use o .NET para Apache Spark em ambientes interativos como Jupyter Notebook, Jupyter Lab ou Visual Studio Code (VS Code)
ms.author: luquinta
author: luisquintanilla
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc, how-to
ms.openlocfilehash: 9c0e713731b5e2ad742bdd257a99f9029f244363
ms.sourcegitcommit: 3a8f1979a98c6c19217a1930e0af5908988eb8ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98536106"
---
# <a name="use-net-for-apache-spark-in-jupyter-notebooks"></a>Usar o .NET para Apache Spark em notebooks Jupyter

Neste artigo, você aprenderá a executar o .NET para trabalhos de Apache Spark interativamente no Jupyter Notebook e no Visual Studio Code (VS Code) com o .NET Interactive.

## <a name="about-jupyter"></a>Sobre o Jupyter

O [Jupyter](https://jupyter.org/) é um ambiente de computação de plataforma cruzada de software livre que fornece uma maneira para os usuários criarem protótipos e desenvolverem aplicativos interativamente. Você pode interagir com o Jupyter por meio de uma ampla variedade de interfaces, como Jupyter Notebook, Jupyter Lab e VS Code.

No contexto do .NET, o [.net Interactive](https://github.com/dotnet/interactive), uma ferramenta global do .NET Core, fornece um kernel para escrever código .net (C#/f #) em ambientes de computação interativa, como Jupyter notebook.

## <a name="prerequisites"></a>Pré-requisitos

- [SDK do .NET Core 3.1](../../core/install/index.yml)
- [Apache Spark](https://spark.apache.org/downloads.html)
- [Apache Spark o trabalho do .NET](https://github.com/dotnet/spark/releases)

Consulte o [tutorial de introdução](../tutorials/get-started.md) para obter mais informações sobre como configurar seu .net para Apache Spark ambiente.

## <a name="prepare-environment"></a>Preparar o ambiente

Para trabalhar com notebooks Jupyter, você precisará de duas coisas.

1. Instalar a [ferramenta global .net interativa do .net](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)
1. Baixe o `Microsoft.Spark` pacote NuGet.
    1. Navegue até a página do pacote NuGet do [Microsoft. Spark](https://www.nuget.org/packages/Microsoft.Spark/) .

        > [!IMPORTANT]
        > Por padrão, a versão mais recente do pacote é baixada. **Certifique-se de que a versão baixada seja a mesma do seu Apache Spark .NET Worker.**

    1. No painel **informações** , selecione **baixar pacote** para baixar a versão mais recente do pacote. O nome do pacote é semelhante a  *Microsoft. Spark. [ PACOTE-versão]. nupkg*.
    1. Descompacte o pacote baixado. O diretório descompactado deve conter um subdiretório chamado *jars*. Anote o caminho, uma vez que ele é usado mais tarde.

## <a name="start-net-for-apache-spark"></a>Iniciar o .NET para Apache Spark

Execute o comando a seguir para iniciar o .NET para Apache Spark no modo de depuração. Esse `spark-submit` comando inicia um processo e aguarda conexões de um [SparkSession](xref:Microsoft.Spark.Sql.SparkSession). Certifique-se de fornecer o caminho para o `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar` para a respectiva versão do .net para Apache Spark que você está usando.

**Ubuntu**

```bash
spark-submit \
    --class org.apache.spark.deploy.dotnet.DotnetRunner \
    --master local \
    <path-to-microsoft-spark-jar> \
    debug
```

**Windows**

```cmd
spark-submit ^
    --class org.apache.spark.deploy.dotnet.DotnetRunner ^
    --master local ^
    <path-to-microsoft-spark-jar> ^
    debug
```

## <a name="create-a-notebook"></a>Criar um notebook

Você pode usar interfaces diferentes para interagir com o Jupyter. Para uma interface baseada em navegador, use Jupyter notebooks ou Jupyter Lab. Para obter uma experiência de editor local, use VS Code.

### <a name="jupyter-notebooks--jupyter-lab"></a>Jupyter notebooks & Jupyter Lab

1. Em outro prompt de comando, inicie o Jupyter Notebook ou o Jupyter Lab usando um dos comandos abaixo:

    **Jupyter Notebook**

    ```bash
    jupyter notebook
    ```

    **Laboratório de Jupyter**

    ```bash
    jupyter lab
    ```

    Esses comandos iniciam uma janela do navegador com a interface de laboratório Jupyter Notebook ou Jupyter.

1. No navegador, crie um novo bloco de anotações.

    **Jupyter Notebook**

    Selecione **novo > .net (C#)** ou **novo > .net (F #)**

    **Laboratório de Jupyter**

    Na janela do iniciador, selecione **.net (C#)** ou **.net (F #)**

### <a name="visual-studio-code-preview"></a>Visual Studio Code (versão prévia)

> [!IMPORTANT]
> Para usar os blocos de anotações do Jupyter no VS Code, você precisa instalar:
>
>- [Pessoas VS Codes](https://code.visualstudio.com/insiders/)
>- [Extensão de blocos de anotações interativos do .NET](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

1. Abra o VS Code.
1. Abra a exibição paleta de comandos **> paleta de comandos**.

    Quando a paleta de comandos for exibida, digite o seguinte comando para criar um novo notebook interativo .NET:

    ```text
    >.NET Interactive: Create new blank notebook
    ```

    Como alternativa, se você quiser abrir um notebook interativo .NET existente com a extensão *. ipynb* , use o seguinte comando:

    ```text
    >.NET Interactive: Open notebook
    ```

## <a name="initialize-a-spark-session"></a>Inicializar uma sessão do Spark

1. Quando o notebook for aberto, instale o `Microsoft.Spark` pacote NuGet. Verifique se a versão instalada é a mesma do trabalho do .NET.

    ```text
    #r "nuget:Microsoft.Spark, 1.0.0"
    ```

1. Adicione a seguinte instrução using ao bloco de anotações.

    ```csharp
    using Microsoft.Spark.Sql;
    ```

1. Inicialize seu [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).

    ```csharp
    var sparkSession =
    SparkSession
        .Builder()
        .AppName("dotnet-interactive-spark")
        .GetOrCreate();
    ```

O notebook deve ser semelhante ao mostrado na imagem a seguir. Este exemplo usa VS Code, mas Jupyter Notebook e Jupyter Lab devem ter a mesma aparência.

> [!div class="mx-imgBorder"]
![.NET para Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)

## <a name="next-steps"></a>Próximas etapas

- [Introdução ao .NET para Apache Spark](../tutorials/get-started.md)
- [Prever sentimentos usando .NET para Apache Spark e ML.NET](../tutorials/ml-sentiment-analysis.md)
- Para obter mais informações sobre o .NET Interactive, consulte a [documentação interativa do .net](https://github.com/dotnet/interactive/blob/main/docs/README.md).
