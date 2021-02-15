---
title: Como usar a API de ML automatizado do ML.NET
description: A API de ML automatizado do ML.NET automatiza o processo de criação de modelo e gera um modelo pronto para implantação. Saiba as opções que você pode usar para configurar tarefas de aprendizado de máquina automatizada.
ms.date: 12/18/2019
ms.custom: mvc,how-to
ms.openlocfilehash: b1ef526301e01e1e75e71e0646f4d11e68215d69
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540726"
---
# <a name="how-to-use-the-mlnet-automated-machine-learning-api"></a>Como usar a API de aprendizado de máquina automatizado do ML.NET

AutoML (aprendizado de máquina automatizado) automatiza o processo de aplicar o aprendizado de máquina a dados. Dado um conjunto de dados, você pode executar um **experimento** de AutoML para iterar em diferentes personalizações de dados, algoritmos de aprendizado de máquina e hiperparâmetros para selecionar o melhor modelo.

> [!NOTE]
> Este tópico refere-se à API de aprendizado de máquina automatizado para ML.NET, que está atualmente em versão prévia. O material pode estar sujeito a alterações.

## <a name="load-data"></a>Carregar dados

O aprendizado de máquina automatizado dá suporte para carregar um conjunto de dados para uma [IDataView](xref:Microsoft.ML.IDataView). Os dados podem estar na forma de arquivos TSV (valor separado por tabulações) e CSV (valor separado por vírgulas).

Exemplo:

```csharp
using Microsoft.ML;
using Microsoft.ML.AutoML;
    // ...
    MLContext mlContext = new MLContext();
    IDataView trainDataView = mlContext.Data.LoadFromTextFile<SentimentIssue>("my-data-file.csv", hasHeader: true);
```

## <a name="select-the-machine-learning-task-type"></a>Selecione o tipo de tarefa de aprendizado de máquina

Antes de criar um experimento, determine o tipo de problema de aprendizado de máquina que você deseja resolver. Aprendizado de máquina automatizado é compatível com as seguintes tarefas de ML:

* Classificação Binária
* Classificação Multiclasse
* Regressão
* Recomendação

## <a name="create-experiment-settings"></a>Criar configurações de experimento

Criar configurações de experimento para o tipo de tarefa de ML determinado:

* Classificação Binária

  ```csharp
  var experimentSettings = new BinaryExperimentSettings();
  ```

* Classificação Multiclasse

  ```csharp
  var experimentSettings = new MulticlassExperimentSettings();
  ```

* Regressão

  ```csharp
  var experimentSettings = new RegressionExperimentSettings();
  ```

* Recomendação

  ```csharp
  var experimentSettings = new RecommendationExperimentSettings();
  ```

## <a name="configure-experiment-settings"></a>Definir as configurações de teste

Os experimentos são altamente configuráveis. Veja os [documentos de API de AutoML](/dotnet/api/microsoft.ml.automl?view=ml-dotnet-preview) para obter uma lista completa de definições de configuração.

Alguns exemplos incluem:

1. Especifique o tempo máximo pelo qual o experimento pode ser executado.

    ```csharp
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    ```

1. Use um token de cancelamento para cancelar o experimento antes de seu término agendado.

    ```csharp
    experimentSettings.CancellationToken = cts.Token;

    // Cancel experiment after the user presses any key
    CancelExperimentAfterAnyKeyPress(cts);
    ```

1. Especifique uma métrica de otimização diferente.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.OptimizingMetric = RegressionMetric.MeanSquaredError;
    ```

1. A configuração `CacheDirectory` é um ponteiro para um diretório em que todos os modelos treinados durante a tarefa AutoML serão salvos. Se `CacheDirectory` for definido como nulo, os modelos serão mantidos na memória, em vez de gravados em disco.

    ```csharp
    experimentSettings.CacheDirectory = null;
    ```

1. Instrua ML automatizado a não usar determinados treinadores.

    Uma lista padrão de treinadores para otimizar é explorada por tarefa. Essa lista pode ser modificada para cada experimento. Por exemplo, treinadores executados lentamente em seu conjunto de dados podem ser removidos da lista. Para otimizar um treinador específico, chame `experimentSettings.Trainers.Clear()` e adicione o treinador que você deseja usar.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.Trainers.Remove(RegressionTrainer.LbfgsPoissonRegression);
    experimentSettings.Trainers.Remove(RegressionTrainer.OnlineGradientDescent);
    ```

A lista de treinadores com suporte por tarefa de ML pode ser encontrada no link correspondente abaixo:

* [Algoritmos de Classificação Binária com Suporte](xref:Microsoft.ML.AutoML.BinaryClassificationTrainer)
* [Algoritmos de Classificação Multiclasse com Suporte](xref:Microsoft.ML.AutoML.MulticlassClassificationTrainer)
* [Algoritmos de Regressão com Suporte](xref:Microsoft.ML.AutoML.RegressionTrainer)
* [Algoritmos de recomendação com suporte](xref:Microsoft.ML.AutoML.RecommendationTrainer)

## <a name="optimizing-metric"></a>Métrica de otimização

A métrica da otimiza, conforme mostrado no exemplo acima, determina a métrica a ser otimizada durante o treinamento de modelo. A métrica de otimização que você pode selecionar é determinada pelo tipo de tarefa que você escolher. Abaixo está uma lista de métricas disponíveis.

|[Classificação binária](xref:Microsoft.ML.AutoML.BinaryClassificationMetric) | [Classificação multiclasse](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric) |[Regressão & recomendação](xref:Microsoft.ML.AutoML.RegressionMetric)
|-- |-- |--
|Precisão| LogLoss | RSquared
|AreaUnderPrecisionRecallCurve | LogLossReduction | MeanAbsoluteError
|AreaUnderRocCurve | MacroAccuracy | MeanSquaredError
|F1Score | MicroAccuracy | RootMeanSquaredError
|NegativePrecision | TopKAccuracy
|NegativeRecall |
|PositivePrecision
|PositiveRecall

## <a name="data-pre-processing-and-featurization"></a>Pré-processamento e personalização de dados

> [!NOTE]
> A coluna de recursos tem suporte apenas para tipos de <xref:System.Boolean> , <xref:System.Single> e <xref:System.String> .

O pré-processamento de dados ocorre por padrão e as etapas a seguir são executadas automaticamente para você:

1. Remover os recursos sem informações úteis

    Remova recursos sem informações úteis do treinamento e dos conjuntos de validação. Eles incluem recursos com todos os valores ausentes, o mesmo valor em todas as linhas ou cardinalidade extremamente alta (por exemplo, hashes, IDs ou GUIDs).

1. Imputação e indicação de valor ausente

    Preencha as células de valor ausente com o valor padrão para o tipo de dados. Acrescente recursos de indicador com o mesmo número de slots de que a coluna de entrada. O valor nos recursos de indicador acrescentados será `1` se o valor na coluna de entrada estiver ausente e `0`, caso contrário.

1. Gerar recursos adicionais

    Para recursos de texto: recursos de conjunto de palavras usando unigrams e Tri-Character-grams.

    Para recursos categóricos: codificação One-Hot para recursos de cardinalidade baixa e codificação de hash One-Hot para recursos categóricos de alta cardinalidade.

1. Transformações e codificações

    Recursos de texto com poucos valores exclusivos transformados em recursos categóricos. Dependendo da cardinalidade de recursos categóricos, execute codificação one-hot ou codificação one-hot hash.

## <a name="exit-criteria"></a>Critérios de saída

Defina os critérios para concluir sua tarefa:

1. Saída após um período – usando `MaxExperimentTimeInSeconds` em suas configurações de experimento, você pode definir quanto tempo em segundos uma tarefa deve continuar em execução.

1. Saída em um token de cancelamento – você pode usar um token de cancelamento que permita cancelar a tarefa antes de seu término agendado.

    ```csharp
    var cts = new CancellationTokenSource();
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    experimentSettings.CancellationToken = cts.Token;
    ```

## <a name="create-an-experiment"></a>Criar uma experiência

Depois de definir as configurações de teste, você está pronto para criar o experimento.

```csharp
RegressionExperiment experiment = mlContext.Auto().CreateRegressionExperiment(experimentSettings);
```

## <a name="run-the-experiment"></a>Execute o experimento

Executar o experimento dispara o pré-processamento de dados, a seleção do algoritmo de aprendizado e o ajuste de hiperparâmetro. AutoML continuará a gerar combinações de personalização, algoritmos de aprendizado e hiperparâmetros até o `MaxExperimentTimeInSeconds` ser atingido ou o experimento ser encerrado.

```csharp
ExperimentResult<RegressionMetrics> experimentResult = experiment
    .Execute(trainingDataView, LabelColumnName, progressHandler: progressHandler);
```

Explore outras sobrecargas para `Execute()` se quiser passar dados de validação, informações de coluna indicando a finalidade de coluna ou pré-personalizações.

## <a name="training-modes"></a>Modos de treinamento

### <a name="training-dataset"></a>Conjunto de dados de treinamento

O AutoML oferece um método de execução de experimento sobrecarregado que possibilita que você forneça dados de treinamento. Internamente, o ML automatizado divide os dados em divisões train-validate.

```csharp
experiment.Execute(trainDataView);
```

### <a name="custom-validation-dataset"></a>Conjunto de dados de validação personalizados

Use o conjunto de dados de validação personalizado se divisão aleatória não for aceitável, como normalmente é o caso para dados de série temporal. É possível especificar seu próprio conjunto de dados de validação. O modelo será avaliado em relação ao conjunto de dados de validação especificado, em vez de um ou mais conjuntos de dados aleatórios.

```csharp
experiment.Execute(trainDataView, validationDataView);
```

## <a name="explore-model-metrics"></a>Explorar as métricas do modelo

Depois de cada iteração de um experimento de ML, as métricas relacionadas à tarefa são armazenadas.

Por exemplo, podemos acessar as métricas de validação da melhor execução:

```csharp
RegressionMetrics metrics = experimentResult.BestRun.ValidationMetrics;
Console.WriteLine($"R-Squared: {metrics.RSquared:0.##}");
Console.WriteLine($"Root Mean Squared Error: {metrics.RootMeanSquaredError:0.##}");
```

Estas são todas as métricas disponíveis por tarefa de ML:

* [Métricas de classificação binária](xref:Microsoft.ML.AutoML.BinaryClassificationMetric)
* [Métricas de classificação multiclasse](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric)
* [Regressão & métricas de recomendação](xref:Microsoft.ML.AutoML.RegressionMetric)

## <a name="see-also"></a>Confira também

Para exemplos de código completos e muito mais, acesse o repositório do GitHub [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master#automate-mlnet-models-generation-preview-state).
