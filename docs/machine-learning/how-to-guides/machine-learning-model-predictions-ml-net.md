---
title: Fazer previsões com um modelo treinado
description: Aprenda a fazer previsões usando um modelo treinado
ms.date: 09/18/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 2e8263db289bed50e7437b695134458b8c07e0e5
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679567"
---
# <a name="make-predictions-with-a-trained-model"></a>Fazer previsões com um modelo treinado

Saiba como usar um modelo treinado para fazer previsões

## <a name="create-data-models"></a>Criar modelo de dados

### <a name="input-data"></a>Dados de entrada

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }

    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

### <a name="output-data"></a>Dados de saída

Como os nomes de coluna de entrada `Features` e `Label`, do ML.NET tem nomes padrão para as colunas de valor previsto produzidas por um modelo. Dependendo da tarefa, o nome pode diferir.

Como o algoritmo usado neste exemplo é um algoritmo de regressão linear, o nome padrão da coluna de saída é `Score` definido pelo [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) atributo na `PredictedPrice` propriedade.

```csharp
class HousingPrediction
{
    [ColumnName("Score")]
    public float PredictedPrice { get; set; }
}
```

## <a name="set-up-a-prediction-pipeline"></a>Configurar um pipeline de previsão

Seja fazendo uma previsão única ou em lotes, o pipeline de previsão precisa ser carregado no aplicativo. Esse pipeline contém as transformações de pré-processamento de dados, bem como o modelo treinado. O snippet de código a seguir carrega o pipeline de previsão de um arquivo chamado `model.zip`.

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

// Load Trained Model
DataViewSchema predictionPipelineSchema;
ITransformer predictionPipeline = mlContext.Model.Load("model.zip", out predictionPipelineSchema);
```

## <a name="single-prediction"></a>Previsão única

Para fazer uma única previsão, crie uma [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) usando o pipeline de previsão carregado.

```csharp
// Create PredictionEngines
PredictionEngine<HousingData, HousingPrediction> predictionEngine = mlContext.Model.CreatePredictionEngine<HousingData, HousingPrediction>(predictionPipeline);
```

Em seguida, use o [`Predict`](xref:Microsoft.ML.PredictionEngineBase%602.Predict%2A) método e transmita seus dados de entrada como um parâmetro. Observe que o uso do [`Predict`](xref:Microsoft.ML.PredictionEngineBase%602.Predict%2A) método não requer que a entrada seja um [`IDataView`](xref:Microsoft.ML.IDataView) ). Isso ocorre porque ele internaliza convenientemente a manipulação do tipo de dados de entrada para que você possa passar um objeto do tipo de dados de entrada. Além disso, uma vez que `CurrentPrice` é o destino ou o rótulo que você está tentando prever usando novos dados, supõe-se não há nenhum valor para ele no momento.

```csharp
// Input Data
HousingData inputData = new HousingData
{
    Size = 900f,
    HistoricalPrices = new float[] { 155000f, 190000f, 220000f }
};

// Get Prediction
HousingPrediction prediction = predictionEngine.Predict(inputData);
```

Se você acessar a propriedade `Score` do objeto `prediction`, deverá obter um valor semelhante ao `150079`.

## <a name="multiple-predictions"></a>Várias previsões

Dado os dados a seguir, carregue-os em um [`IDataView`](xref:Microsoft.ML.IDataView) . Nesse caso, o nome do [`IDataView`](xref:Microsoft.ML.IDataView) é `inputData` . Uma vez que `CurrentPrice` é o destino ou o rótulo que você está tentando prever usando novos dados, supõe-se que não há valor para ele no momento.

```csharp
// Actual data
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f, 175000f, 210000f }
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f }
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f }
    }
};
```

Em seguida, use o [`Transform`](xref:Microsoft.ML.ITransformer.Transform%2A) método para aplicar as transformações de dados e gerar previsões.

```csharp
// Predicted Data
IDataView predictions = predictionPipeline.Transform(inputData);
```

Inspecione os valores previstos usando o [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn%2A) método.

```csharp
// Get Predictions
float[] scoreColumn = predictions.GetColumn<float>("Score").ToArray();
```

Os valores previstos da coluna de pontuação devem ser semelhantes aos seguintes:

| Observação | Previsão |
|---|---|
| 1 | 144638,2 |
| 2 | 150079,4 |
| 3 | 107789,8 |
