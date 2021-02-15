---
title: Salvar e carregar modelos treinados
description: Saiba como salvar e carregar modelos treinados
ms.date: 05/03/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 681a35956a8959e2f1cbb5a7023e0ef29b67097e
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679528"
---
# <a name="save-and-load-trained-models"></a>Salvar e carregar modelos treinados

Saiba como salvar e carregar modelos treinados em seu aplicativo.

Em todo o processo de criação de modelo, um modelo reside na memória e é acessível em todo o ciclo de vida do aplicativo. No entanto, depois que o aplicativo terminar a execução, se o modelo não for salvo em algum lugar local ou remotamente, ele não ficará mais acessível. Normalmente, os modelos são usados em algum momento após o treinamento em outros aplicativos para inferência de tipos ou novo treinamento. Assim, é importante armazenar o modelo. Salve e carregue modelos usando as etapas descritas nas seções subsequentes deste documento ao usar pipelines de treinamento de modelo e preparação de dados como os detalhados abaixo. Embora este exemplo use um modelo de regressão linear, o mesmo processo se aplica a outros algoritmos do ML.NET.

```csharp
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 600f,
        HistoricalPrices = new float[] { 100000f, 125000f, 122000f },
        CurrentPrice = 170000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 200000f, 250000f, 230000f },
        CurrentPrice = 225000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 126000f, 130000f, 200000f },
        CurrentPrice = 195000f
    }
};

// Create MLContext
MLContext mlContext = new MLContext();

// Load Data
IDataView data = mlContext.Data.LoadFromEnumerable<HousingData>(housingData);

// Define data preparation estimator
EstimatorChain<RegressionPredictionTransformer<LinearRegressionModelParameters>> pipelineEstimator =
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"))
        .Append(mlContext.Regression.Trainers.Sdca());

// Train model
ITransformer trainedModel = pipelineEstimator.Fit(data);

// Save model
mlContext.Model.Save(trainedModel, data.Schema, "model.zip");
```

Porque a maioria dos pipelines de preparação de dados e modelos herda o mesmo conjunto de classes, as assinaturas do método salvar e carregar para esses componentes são iguais. Dependendo do seu caso de uso, você pode combinar o pipeline de preparação de dados e o modelo em um único que produzirá [`EstimatorChain`](xref:Microsoft.ML.Data.TransformerChain%601) um único [`ITransformer`](xref:Microsoft.ML.ITransformer) ou separá-los, criando um separado [`ITransformer`](xref:Microsoft.ML.ITransformer) para cada um.

## <a name="save-a-model-locally"></a>Salvar um modelo localmente

Ao salvar um modelo, você precisa de dois itens:

1. O [`ITransformer`](xref:Microsoft.ML.ITransformer) do modelo.
2. O [`DataViewSchema`](xref:Microsoft.ML.DataViewSchema) da [`ITransformer`](xref:Microsoft.ML.ITransformer) entrada esperada.

Depois de treinar o modelo, use o [`Save`](xref:Microsoft.ML.ModelOperationsCatalog.Save%2A) método para salvar o modelo treinado em um arquivo chamado `model.zip` usando os `DataViewSchema` dados de entrada.

```csharp
// Save Trained Model
mlContext.Model.Save(trainedModel, data.Schema, "model.zip");
```

## <a name="load-a-model-stored-locally"></a>Carregar um modelo armazenado localmente

Os modelos armazenados localmente podem ser usados em outros processos ou aplicativos, como `ASP.NET Core` e `Serverless Web Applications`. Veja os artigos de instruções [Usar ML.NET na API Web](./serve-model-web-api-ml-net.md) e [Implantar aplicativo Web sem servidor do ML.NET](./serve-model-serverless-azure-functions-ml-net.md) para saber mais.

Em um aplicativo ou processo separado, use o [`Load`](xref:Microsoft.ML.ModelOperationsCatalog.Load%2A) método junto com o caminho do arquivo para obter o modelo treinado em seu aplicativo.

```csharp
//Define DataViewSchema for data preparation pipeline and trained model
DataViewSchema modelSchema;

// Load trained model
ITransformer trainedModel = mlContext.Model.Load("model.zip", out modelSchema);
```

## <a name="load-a-model-stored-remotely"></a>Carregar um modelo armazenado remotamente

Para carregar pipelines de preparação de dados e modelos armazenados em um local remoto em seu aplicativo, use um [`Stream`](xref:System.IO.Stream) em vez de um caminho de arquivo no [`Load`](xref:Microsoft.ML.ModelOperationsCatalog.Load%2A) método.

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

// Define DataViewSchema and ITransformers
DataViewSchema modelSchema;
ITransformer trainedModel;

// Load data prep pipeline and trained model
using (HttpClient client = new HttpClient())
{
    Stream modelFile = await client.GetStreamAsync("<YOUR-REMOTE-FILE-LOCATION>");

    trainedModel = mlContext.Model.Load(modelFile, out modelSchema);
}
```

## <a name="working-with-separate-data-preparation-and-model-pipelines"></a>Trabalhando com pipelines de modelo e preparação de dados separados

> [!NOTE]
> Trabalhar com pipelines de treinamento de modelo e preparação de dados separados é opcional. A separação de pipelines facilita a inspeção dos parâmetros do modelo aprendido. Para obter previsões, é mais fácil de salvar e carregar um único pipeline que inclua as operações de treinamento de modelo e preparação de dados.

Ao trabalhar com modelos e pipelines de preparação de dados separados, aplica-se o mesmo processo que o para pipelines únicos, exceto que agora os dois pipelines precisam ser salvos e carregados simultaneamente.

Dados pipelines de treinamento de modelo e preparação de dados separados:

```csharp
// Define data preparation estimator
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data preparation transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// Define StochasticDualCoordinateAscent regression algorithm estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Pre-process data using data prep operations
IDataView transformedData = dataPrepTransformer.Transform(data);

// Train regression model
RegressionPredictionTransformer<LinearRegressionModelParameters> trainedModel = sdcaEstimator.Fit(transformedData);
```

### <a name="save-data-preparation-pipeline-and-trained-model"></a>Salve o pipeline de preparação de dados e o modelo treinado

Para salvar o pipeline de preparação de dados e o modelo treinado, use os seguintes comandos:

```csharp
// Save Data Prep transformer
mlContext.Model.Save(dataPrepTransformer, data.Schema, "data_preparation_pipeline.zip");

// Save Trained Model
mlContext.Model.Save(trainedModel, transformedData.Schema, "model.zip");
```

### <a name="load-data-preparation-pipeline-and-trained-model"></a>Carregar o pipeline de preparação de dados e o modelo treinado

Em um processo ou aplicativo separado, carregue o modelo treinado e o pipeline de preparação de dados simultaneamente da seguinte maneira:

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

// Define data preparation and trained model schemas
DataViewSchema dataPrepPipelineSchema, modelSchema;

// Load data preparation pipeline and trained model
ITransformer dataPrepPipeline = mlContext.Model.Load("data_preparation_pipeline.zip",out dataPrepPipelineSchema);
ITransformer trainedModel = mlContext.Model.Load("model.zip", out modelSchema);
```
