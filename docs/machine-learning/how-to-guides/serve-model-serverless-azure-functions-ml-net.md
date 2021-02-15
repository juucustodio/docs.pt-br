---
title: Implantar um modelo no Azure Functions
description: Usar um modelo de machine learning para Análise de Sentimento com o ML.NET para previsão pela internet usando o Azure Functions
ms.date: 02/21/2020
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 74a7a5b941596ba9fffc62ef87a01763937d88c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2020
ms.locfileid: "91608771"
---
# <a name="deploy-a-model-to-azure-functions"></a>Implantar um modelo no Azure Functions

Saiba como implantar um modelo de machine learning do ML.NET pré-treinado para previsões por HTTP por meio de um ambiente sem servidor do Azure Functions.

> [!NOTE]
> Este exemplo executa uma versão de visualização do `PredictionEnginePool` serviço.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) ou posterior ou visual Studio 2017 versão 15,6 ou posterior com as cargas de trabalho "desenvolvimento de plataforma cruzada do .NET Core" e "desenvolvimento do Azure" instalados.
- [Ferramentas do Azure Functions](/azure/azure-functions/functions-develop-vs#check-your-tools-version)
- PowerShell
- Modelo previamente treinado. Use o [tutorial de Análise de Sentimento do ML.NET](../tutorials/sentiment-analysis.md) para criar seu próprio modelo ou baixe este [modelo de machine learning de análise de sentimento pré-treinado](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)

## <a name="azure-functions-sample-overview"></a>Visão geral de Azure Functions de exemplo

Este exemplo é um **gatilho http C# Azure Functions aplicativo** que usa um modelo de classificação binária pretreinado para categorizar a notação de texto como positivo ou negativo. Azure Functions fornece uma maneira fácil de executar pequenas partes de código em escala em um ambiente gerenciado sem servidor na nuvem. O código para este exemplo pode ser encontrado no repositório [dotnet/MachineLearning-Samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction) no github.

## <a name="create-azure-functions-project"></a>Criar um projeto do Azure Functions

1. Abra o Visual Studio 2017. Selecione **arquivo**  >  **novo**  >  **projeto** na barra de menus. Na caixa de diálogo **Novo projeto**, selecione o nó **Visual C#** seguido pelo nó **Nuvem**. Em seguida, selecione o modelo de projeto do **Azure Functions**. Na caixa de texto **Nome**, digite "SentimentAnalysisFunctionsApp" e, em seguida, selecione o botão **OK**.
1. Na caixa de diálogo **Novo Projeto**, abra a lista suspensa acima das opções de projeto e selecione **Azure Functions v2 (.NET Core)**. Depois, selecione o projeto de **Gatilho de HTTP** e, em seguida, o botão **OK**.
1. Crie um diretório chamado *MLModels* em seu projeto para salvar o modelo:

    No **Gerenciador de Soluções**, clique com o botão direito do mouse no seu projeto e selecione **Adicionar** > **Nova Pasta**. Digite "MLModels" e pressione ENTER.

1. Instale o **pacote Microsoft.ml NuGet** versão **1.3.1**:

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a Origem do pacote, selecione a guia Procurar, pesquise por **Microsoft.ML**, selecione o pacote na lista e escolha o botão **Instalar**. Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados.

1. Instale o **Pacote NuGet Microsoft.Azure.Functions.Extensions**:

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a origem do pacote, selecione a guia Procurar, procure por **Microsoft.Azure.Functions.Extensions**, selecione o pacote na lista e selecione o botão **Instalar**. Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados.

1. Instale o **pacote Microsoft.Extensions.ml NuGet** versão **0.15.1**:

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a origem do pacote, selecione a guia procurar, procure **Microsoft.Extensions.ml**, selecione o pacote na lista e selecione o botão **instalar** . Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados.

1. Instale a versão **1.0.31** do **pacote NUGET Microsoft. net. Sdk. Functions** :

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a origem do pacote, selecione a guia instalado, pesquise por **Microsoft. net. Sdk. Functions**, selecione esse pacote na lista, selecione **1.0.31** no menu suspenso versão e selecione o botão **Atualizar** . Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados.

## <a name="add-pre-trained-model-to-project"></a>Adicionar modelo pré-treinado ao projeto

1. Copie o modelo previamente criado para o diretório *MLModels*.
1. No Gerenciador de Soluções, clique com o botão direito do mouse no arquivo do modelo criado previamente e selecione **Propriedades**. Em **avançado**, altere o valor de **copiar para diretório de saída** para **copiar se mais recente**.

## <a name="create-azure-function-to-analyze-sentiment"></a>Criar Função do Azure para analisar o sentimento

Crie uma classe para prever o sentimento. Adicione uma nova classe ao seu projeto:

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Adicionar** > **Novo Item**.

1. Na caixa de diálogo **Adicionar novo item**, selecione **Função do Azure** e altere o campo **Nome** para *AnalyzeSentiment.cs*. Em seguida, selecione o botão **Adicionar**.

1. Na caixa de diálogo **Nova Função do Azure**, selecione **Gatilho de HTTP**. Depois, selecione o botão **OK**.

    O arquivo *AnalyzeSentiment.cs* é aberto no editor de códigos. Adicione a seguinte instrução `using` acima de *AnalyzeSentiment.cs*:

    [!code-csharp [AnalyzeUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L1-L11)]

    Por padrão, a classe `AnalyzeSentiment` é `static`. Remova a palavra-chave `static` da definição da classe.

    ```csharp
    public class AnalyzeSentiment
    {

    }
    ```

## <a name="create-data-models"></a>Criar modelo de dados

Você precisa criar algumas classes para os dados e previsões de entrada. Adicione uma nova classe ao seu projeto:

1. Crie um diretório chamado *Datamodels* em seu projeto para salvar seus modelos de dados: no Gerenciador de soluções, clique com o botão direito do mouse no seu projeto e selecione **Adicionar > nova pasta**. Digite "DataModels" e pressione ENTER.
2. Em Gerenciador de Soluções, clique com o botão direito do mouse no diretório *datamodelos* e selecione **Adicionar > novo item**.
3. Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *SentimentData.cs*. Em seguida, selecione o botão **Adicionar**.

    O arquivo *SentimentData.cs* é aberto no editor de códigos. Adicione a seguinte instrução using na parte superior do *SentimentData.cs*:

    [!code-csharp [SentimentDataUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L1)]

    Remova a definição de classe existente e adicione o seguinte código ao arquivo *SentimentData.cs* :

    [!code-csharp [SentimentData](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L5-L13)]

4. Em Gerenciador de Soluções, clique com o botão direito do mouse no diretório *datamodelos* e selecione **Adicionar > novo item**.
5. Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *SentimentPrediction.cs*. Em seguida, selecione o botão **Adicionar**. O arquivo *SentimentPrediction.cs* é aberto no editor de códigos. Adicione a seguinte instrução "using" na parte superior do *SentimentPrediction.cs*:

    [!code-csharp [SentimentPredictionUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L1)]

    Remova a definição de classe existente e adicione o seguinte código ao arquivo *SentimentPrediction.cs*:

    [!code-csharp [SentimentPrediction](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L5-L14)]

    `SentimentPrediction` herda de `SentimentData`, que dá acesso aos dados originais na propriedade `SentimentText`, bem como a saída gerada pelo modelo.

## <a name="register-predictionenginepool-service"></a>Registrar serviço PredictionEnginePool

Para fazer uma única previsão, você precisa criar um [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) . [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) Não é thread-safe. Além disso, você precisa criar uma instância dela em qualquer lugar em que seja necessário dentro de seu aplicativo. À medida que seu aplicativo cresce, esse processo pode se tornar não gerenciável. Para melhorar o desempenho e a segurança do thread, use uma combinação de injeção de dependência e o `PredictionEnginePool` serviço, que cria um [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) dos [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) objetos para uso em todo o aplicativo.

O link a seguir fornece mais informações se você quiser saber mais sobre [injeção de dependência](https://en.wikipedia.org/wiki/Dependency_injection).

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Adicionar** > **Novo Item**.
1. Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *Startup.cs*. Em seguida, selecione o botão **Adicionar**.
1. Adicione as seguintes instruções using à parte superior de *Startup.cs*:

    [!code-csharp [StartupUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L1-L6)]

1. Remova o código existente abaixo das instruções using e adicione o seguinte código:

    ```csharp
    [assembly: FunctionsStartup(typeof(Startup))]
    namespace SentimentAnalysisFunctionsApp
    {
        public class Startup : FunctionsStartup
        {

        }
    }
    ```

1. Defina variáveis para armazenar o ambiente no qual o aplicativo está sendo executado e o caminho do arquivo em que o modelo está localizado dentro da `Startup` classe

    [!code-csharp [DefineStartupVars](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L13-L14)]

1. Abaixo disso, crie um construtor para definir os valores das `_environment` variáveis e `_modelPath` . Quando o aplicativo é executado localmente, o ambiente padrão é *desenvolvimento*.

    [!code-csharp [StartupCtor](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L16-L29)]

1. Em seguida, adicione um novo método chamado `Configure` para registrar o `PredictionEnginePool` serviço abaixo do construtor.

    [!code-csharp [ConfigureServices](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/Startup.cs#L31-L35)]

Em um alto nível, esse código inicializa os objetos e os serviços automaticamente para uso posterior quando solicitado pelo aplicativo em vez de ter que fazê-lo manualmente.

Os modelos de aprendizado de máquina não são estáticos. À medida que novos dados de treinamento ficam disponíveis, o modelo é retreinado e reimplantado. Uma maneira de obter a versão mais recente do modelo em seu aplicativo é reimplantar o aplicativo inteiro. No entanto, isso introduz o tempo de inatividade do aplicativo. O `PredictionEnginePool` serviço fornece um mecanismo para recarregar um modelo atualizado sem desativar o aplicativo.

Defina o `watchForChanges` parâmetro como `true` e o `PredictionEnginePool` inicia um [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher) que escuta as notificações de alteração do sistema de arquivos e gera eventos quando há uma alteração no arquivo. Isso solicita que o `PredictionEnginePool` recarregue automaticamente o modelo.

O modelo é identificado pelo `modelName` parâmetro para que mais de um modelo por aplicativo possa ser recarregado após a alteração.

> [!TIP]
> Como alternativa, você pode usar o `FromUri` método ao trabalhar com modelos armazenados remotamente. Em vez de observar os eventos de alteração de arquivo, `FromUri` o pesquisa o local remoto em busca de alterações. O padrão do intervalo de sondagem é de 5 minutos. Você pode aumentar ou diminuir o intervalo de sondagem com base nos requisitos do seu aplicativo. No exemplo de código abaixo, o `PredictionEnginePool` sonda o modelo armazenado no URI especificado a cada minuto.
>
>```csharp
>builder.Services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
>   .FromUri(
>       modelName: "SentimentAnalysisModel",
>       uri:"https://github.com/dotnet/samples/raw/master/machine-learning/models/sentimentanalysis/sentiment_model.zip",
>       period: TimeSpan.FromMinutes(1));
>```

## <a name="load-the-model-into-the-function"></a>Carregar o modelo na função

Insira o seguinte código dentro da classe *AnalyzeSentiment*:

[!code-csharp [AnalyzeCtor](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L18-L24)]

Esse código atribui o `PredictionEnginePool` passando-o para o construtor da função que você obtém por meio da injeção de dependência.

## <a name="use-the-model-to-make-predictions"></a>Usar o modelo para fazer previsões

Substitua a implementação existente do método *Run* na classe *AnalyzeSentiment* pelo código a seguir:

[!code-csharp [AnalyzeRunMethod](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L26-L45)]

Quando o método `Run` é executado, os dados de entrada da solicitação HTTP são desserializados e usados como entrada para o `PredictionEnginePool`. O `Predict` método é chamado para fazer previsões usando o `SentimentAnalysisModel` registrado na `Startup` classe e retorna os resultados para o usuário, se for bem-sucedido.

## <a name="test-locally"></a>Testar localmente

Agora que está tudo definido, é hora de testar o aplicativo:

1. Executar o aplicativo
1. Abra o PowerShell e digite o seguinte código no prompt, em que PORT é a porta em que seu aplicativo está sendo executado. Normalmente, a porta é a 7071.

    ```powershell
    Invoke-RestMethod "http://localhost:<PORT>/api/AnalyzeSentiment" -Method Post -Body (@{SentimentText="This is a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    Se houver êxito, a saída deverá ser semelhante ao texto abaixo:

    ```powershell
    Negative
    ```

Parabéns! Você usou com êxito o modelo para fazer previsões pela internet usando uma função do Azure.

## <a name="next-steps"></a>Próximas etapas

- [Implantar no Azure](/azure/azure-functions/functions-develop-vs#publish-to-azure)
