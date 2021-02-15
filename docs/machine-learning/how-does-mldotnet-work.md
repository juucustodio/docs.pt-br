---
title: O que é ML.NET e como ele funciona?
description: O ML.NET oferece a capacidade de adicionar aprendizado de máquina a aplicativos .NET, em cenários online ou offline. Com essa funcionalidade, você pode fazer previsões automáticas usando os dados disponíveis para o aplicativo sem precisar estar conectado a uma rede para usar o ML.NET. Este artigo explica os conceitos básicos do aprendizado de máquina em ML.NET.
ms.date: 11/5/2019
ms.topic: overview
ms.custom: mvc
ms.openlocfilehash: 2c44a83b4d45c95cbe45f125523207811f6368c2
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97634060"
---
# <a name="what-is-mlnet-and-how-does-it-work"></a>O que é ML.NET e como ele funciona?

O ML.NET oferece a capacidade de adicionar aprendizado de máquina a aplicativos .NET, em cenários online ou offline. Com essa funcionalidade, você pode fazer previsões automáticas usando os dados disponíveis ao seu aplicativo. Os aplicativos de Machine Learning fazem uso de padrões nos dados para fazer previsões em vez de precisarem ser programados explicitamente.

Central para o ML.NET é um **modelo** de aprendizado de máquina. O modelo especifica as etapas necessárias para transformar os dados de entrada em uma previsão. Com o ML.NET, você pode treinar um modelo personalizado especificando um algoritmo ou pode importar modelos TensorFlow e ONNX pré-treinados.

Depois de ter um modelo, você pode adicioná-lo ao seu aplicativo para fazer as previsões.

O ML.NET é executado no Windows, no Linux e no macOS usando o .NET Core ou o Windows usando .NET Framework. Há suporte para 64 bits em todas as plataformas. Há suporte para 32 bits no Windows, exceto para a funcionalidade relacionada a TensorFlow, LightGBM e ONNX.

Exemplos do tipo de previsões que você pode fazer com ML.NET:

|||
|-|-|
|Classificação/Categorização|Dividir automaticamente os comentários dos clientes em categorias positivas e negativas|
|Regressão/Prever valores contínuos|Prever o preço de residências com base em tamanho e localização|
|Detecção de anomalias|Detectar transações bancárias fraudulentas |
|Recomendações|Sugerir produtos que compradores online talvez queiram comprar com base em suas compras anteriores|
|Série temporal/dados sequenciais|Prever as vendas do clima/produto|
|Classificação de imagens|Categorizar pathologies em imagens médicas|

## <a name="hello-mlnet-world"></a>Olá, Mundo do ML.NET

O código no snippet a seguir demonstra o aplicativo do ML.NET mais simples. Este exemplo cria um modelo de regressão linear para prever os preços de residências usando dados de tamanho e preço de residências.

 ```csharp
    using System;
    using Microsoft.ML;
    using Microsoft.ML.Data;

    class Program
    {
        public class HouseData
        {
            public float Size { get; set; }
            public float Price { get; set; }
        }

        public class Prediction
        {
            [ColumnName("Score")]
            public float Price { get; set; }
        }

        static void Main(string[] args)
        {
            MLContext mlContext = new MLContext();

            // 1. Import or create training data
            HouseData[] houseData = {
                new HouseData() { Size = 1.1F, Price = 1.2F },
                new HouseData() { Size = 1.9F, Price = 2.3F },
                new HouseData() { Size = 2.8F, Price = 3.0F },
                new HouseData() { Size = 3.4F, Price = 3.7F } };
            IDataView trainingData = mlContext.Data.LoadFromEnumerable(houseData);

            // 2. Specify data preparation and model training pipeline
            var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
                .Append(mlContext.Regression.Trainers.Sdca(labelColumnName: "Price", maximumNumberOfIterations: 100));

            // 3. Train model
            var model = pipeline.Fit(trainingData);

            // 4. Make a prediction
            var size = new HouseData() { Size = 2.5F };
            var price = mlContext.Model.CreatePredictionEngine<HouseData, Prediction>(model).Predict(size);

            Console.WriteLine($"Predicted price for size: {size.Size*1000} sq ft= {price.Price*100:C}k");

            // Predicted price for size: 2500 sq ft= $261.98k
        }
    }
```

## <a name="code-workflow"></a>Fluxo de trabalho de código

O diagrama a seguir representa a estrutura de código do aplicativo, bem como o processo iterativo de desenvolvimento do modelo:

- Coletar e carregar dados de treinamento em um objeto **IDataView**
- Especifique um pipeline de operações para extrair recursos e aplicar um algoritmo de aprendizado de máquina
- Treinar um modelo chamando **Fit()** no pipeline
- Avaliar o modelo e iterar para melhorar
- Salvar o modelo em um formato binário para uso em um aplicativo
- Carregar o modelo de volta para um objeto **ITransformer**
- Fazer previsões chamando **CreatePredictionEngine.Predict()**

![Fluxo de desenvolvimento de aplicativo do ML.NET incluindo componentes para geração de dados, desenvolvimento de pipeline, treinamento do modelo, avaliação de modelo e uso do modelo](./media/mldotnet-annotated-workflow.png)

Vamos nos aprofundar um pouco mais nesses conceitos.

## <a name="machine-learning-model"></a>Modelo de Machine Learning

Um modelo do ML.NET é um objeto que contém transformações para executar em seus dados de entrada para chegar na saída prevista.

### <a name="basic"></a>Basic

O modelo mais básico é regressão linear bidimensional, em que uma quantidade contínua é proporcional a outro, como no exemplo de preço de residência acima.

![Modelo de regressão linear com os parâmetros de peso e desvio](./media/linear-regression-model.svg)

O modelo é simplesmente: $Price = b + Size * w$. Os parâmetros $b$ e $w$ são estimados ajustando uma linha em um conjunto de pares (tamanho, preço). Os dados usados para localizar os parâmetros do modelo são chamados **dados de treinamento**. As entradas de um modelo de machine learning são chamadas de **recursos**. Neste exemplo, $Size$ é o único recurso. Os valores de zero verdadeiro usados para treinar um modelo de machine learning são chamados de **rótulos**. Aqui, os valores de $Price$ no conjunto de dados de treinamento são os rótulos.

### <a name="more-complex"></a>Mais complexo

Um modelo mais complexo classifica as transações financeiras em categorias usando a descrição de texto de transação.

Cada descrição de transação é dividida em um conjunto de recursos removendo caracteres e palavras redundantes e contando combinações de palavras e caracteres. O conjunto de recursos é usado para treinar um modelo linear com base no conjunto de categorias nos dados de treinamento. Quanto mais semelhante uma nova descrição é daquelas no conjunto de treinamento, mais provavelmente ela será atribuída à mesma categoria.

![Modelo de Classificação de Texto](./media/text-classification-model.svg)

Os modelos de preço de residência e o modelo de classificação de texto são modelos **lineares**. Dependendo da natureza de seus dados e do problema que você está resolvendo, você também pode usar modelos de **árvore de decisão**, modelos **aditivos generalizados** e outros. Você pode encontrar mais informações sobre os modelos em [Tarefas](./resources/tasks.md).

## <a name="data-preparation"></a>Preparação de dados

Na maioria dos casos, os dados que você tem disponíveis não são adequados para serem usados diretamente para treinar um modelo de machine learning. Os dados brutos precisam ser preparados ou pré-processados antes que possam ser usados para localizar os parâmetros do modelo. Seus dados talvez precisem ser convertidos de valores de cadeia de caracteres em uma representação numérica. Você pode ter informações redundantes em seus dados de entrada. Talvez você precise reduzir ou expandir as dimensões de seus dados de entrada. Seus dados talvez precisem ser normalizados ou dimensionados.

Os [tutoriais do ML.NET](./tutorials/index.md) ensinam a você sobre os diferentes pipelines de processamento de dados para texto, imagem, dados numéricos e de série temporal usados para tarefas de aprendizado de máquina específicas.

[Como preparar seus dados](./how-to-guides/prepare-data-ml-net.md) mostra como aplicar a preparação de dados com mais frequência.

Você pode encontrar um apêndice de todas as [transformações disponíveis](./resources/transforms.md) na seção de recursos.

## <a name="model-evaluation"></a>Avaliação de modelos

Depois de treinar seu modelo, como você sabe o quão bem ele fará previsões futuras? Com o do ML.NET, você pode avaliar seu modelo em relação a alguns novos dados de teste.

Cada tipo de tarefa de aprendizado de máquina tem métricas usadas para avaliar a precisão e a exatidão do modelo em relação ao conjunto de dados de teste.

Para nosso exemplo de preço de residência, usamos a tarefa **Regressão**. Para avaliar o modelo, adicione o seguinte código à amostra original.

```csharp
        HouseData[] testHouseData =
        {
            new HouseData() { Size = 1.1F, Price = 0.98F },
            new HouseData() { Size = 1.9F, Price = 2.1F },
            new HouseData() { Size = 2.8F, Price = 2.9F },
            new HouseData() { Size = 3.4F, Price = 3.6F }
        };

        var testHouseDataView = mlContext.Data.LoadFromEnumerable(testHouseData);
        var testPriceDataView = model.Transform(testHouseDataView);

        var metrics = mlContext.Regression.Evaluate(testPriceDataView, labelColumnName: "Price");

        Console.WriteLine($"R^2: {metrics.RSquared:0.##}");
        Console.WriteLine($"RMS error: {metrics.RootMeanSquaredError:0.##}");

        // R^2: 0.96
        // RMS error: 0.19
```

As métricas de avaliação dizem que o erro é mais ou menos baixo. Essa correlação entre a saída prevista e a saída do teste é alta. Isso foi fácil. Em exemplos reais, é necessário mais ajuste para obter métricas de modelo válidas.

## <a name="mlnet-architecture"></a>Arquitetura do ML.NET

Nesta seção, vamos repassar os padrões de arquitetura do ML.NET. Se você for um desenvolvedor .NET experiente, alguns destes padrões serão familiares, enquanto outros serão menos conhecidos. Mantenha o foco enquanto nos aprofundamos.

Um aplicativo do ML.NET começa com um objeto <xref:Microsoft.ML.MLContext>. Esse objeto singleton contém **catálogos**. Um catálogo é uma fábrica para carregar e salvar dados, componentes de operação de modelo, treinadores e transformações. Cada objeto de catálogo tem métodos para criar os diferentes tipos de componentes:

|||||
|-|-|-|-|
|Salvamento e carregamento de dados||<xref:Microsoft.ML.DataOperationsCatalog>||
|Preparação de dados||<xref:Microsoft.ML.TransformsCatalog>||
|Treinando algoritmos|Classificação binária|<xref:Microsoft.ML.BinaryClassificationCatalog>||
||Classificação multiclasse|<xref:Microsoft.ML.MulticlassClassificationCatalog>||
||Detecção de anomalias|<xref:Microsoft.ML.AnomalyDetectionCatalog>||
||Clustering|<xref:Microsoft.ML.ClusteringCatalog>||
||Previsão|<xref:Microsoft.ML.ForecastingCatalog>||
||Classificação|<xref:Microsoft.ML.RankingCatalog>||
||Regressão|<xref:Microsoft.ML.RegressionCatalog>||
||Recomendação|<xref:Microsoft.ML.RecommendationCatalog>|adicionar o pacote NuGet `Microsoft.ML.Recommender`|
||TimeSeries|<xref:Microsoft.ML.TimeSeriesCatalog>|adicionar o pacote NuGet `Microsoft.ML.TimeSeries`|
|Uso do modelo ||<xref:Microsoft.ML.ModelOperationsCatalog>||

Você pode navegar para os métodos de criação em cada uma das categorias acima. Usando o Visual Studio, os catálogos aparecem por meio do IntelliSense.

   ![IntelliSense para Treinadores de Regressão](./media/catalog-intellisense.png)

### <a name="build-the-pipeline"></a>Criar o pipeline

Dentro de cada catálogo está um conjunto de métodos de extensão. Vamos examinar como os métodos de extensão são usados para criar um pipeline de treinamento.

```csharp
    var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
        .Append(mlContext.Regression.Trainers.Sdca(labelColumnName: "Price", maximumNumberOfIterations: 100));
```

No snippet, `Concatenate` e `Sdca` são ambos métodos no catálogo. Cada um deles criar um objeto [IEstimator](xref:Microsoft.ML.IEstimator%601) que é acrescentado ao pipeline.

Neste ponto, os objetos são apenas criados. Nenhuma execução aconteceu.

### <a name="train-the-model"></a>Treinar o modelo

Quando os objetos no pipeline foram criados, os dados podem ser usados para treinar o modelo.

```csharp
    var model = pipeline.Fit(trainingData);
```

Chamar `Fit()` usa os dados de treinamento de entrada para estimar os parâmetros do modelo. Isso é conhecido como treinamento do modelo. Lembre-se de que o modelo de regressão linear acima tinha dois parâmetros de modelo: **desvio** e **peso**. Após a chamada `Fit()`, os valores dos parâmetros são conhecidos. A maioria dos modelos terá muito mais parâmetros que isso.

Você pode aprender mais sobre o treinamento de modelo em [como treinar seu modelo](./how-to-guides/train-machine-learning-model-ml-net.md).

O objeto de modelo resultante implementa a interface do <xref:Microsoft.ML.ITransformer>. Ou seja, o modelo transforma dados de entrada em previsões.

```csharp
   IDataView predictions = model.Transform(inputData);
```

### <a name="use-the-model"></a>Usar o modelo

Você pode transformar dados de entrada em previsões em massa ou uma entrada por vez. No exemplo de preço de residência, fizemos ambos: em massa para fins de avaliar o modelo e um por vez para fazer uma nova previsão. Vamos examinar como fazer previsões únicas.

```csharp
    var size = new HouseData() { Size = 2.5F };
    var predEngine = mlContext.CreatePredictionEngine<HouseData, Prediction>(model);
    var price = predEngine.Predict(size);
```

O método `CreatePredictionEngine()` usa uma classe de entrada e uma classe de saída. Os nomes de campo e/ou atributos de código determinam os nomes das colunas de dados usadas durante a previsão e o treinamento do modelo. Para obter mais informações, consulte [fazer previsões com um modelo treinado](how-to-guides/machine-learning-model-predictions-ml-net.md).

### <a name="data-models-and-schema"></a>Esquema e modelos de dados

No núcleo de um pipeline de aprendizado de máquina do ML.NET estão objetos [DataView](xref:Microsoft.ML.IDataView).

Cada transformação no pipeline tem um esquema de entrada (nomes, tipos e tamanhos de dados que a transformação espera ver em sua entrada); e um esquema de saída (nomes, tipos e tamanhos de dados que a transformação produz após a transformação).

Se o esquema de saída de uma transformação no pipeline não corresponder ao esquema de entrada da transformação seguinte, o ML.NET gerará uma exceção.

Um objeto de exibição de dados tem colunas e linhas. Cada coluna tem um nome, um tipo e um comprimento. Por exemplo, as colunas de entrada no exemplo de preço da casa são **tamanho** e **preço**. Eles são ambos os tipos e são quantidades escalares em vez de vetores.

   ![Exemplo de Exibição de Dados do ML.NET com os dados de previsão de preço de residência](./media/ml-net-dataview.png)

Todos os algoritmos do ML.NET procuram por uma coluna de entrada que é um vetor. Por padrão, essa coluna de vetor é chamada **Recursos**. É por isso que estamos concatenados a coluna **Tamanho** em uma nova coluna chamada **Recursos** em nosso exemplo de preço de residência.

 ```csharp
    var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
 ```

Todos os algoritmos também criam novas colunas depois que executaram uma previsão. Os nomes fixos dessas novas colunas dependem do tipo de algoritmo de aprendizado de máquina. Para a tarefa de regressão, uma das novas colunas é chamada **Pontuação**. É por isso que atribuímos nossos dados de preço com esse nome.

```csharp
    public class Prediction
    {
        [ColumnName("Score")]
        public float Price { get; set; }
    }
```

Você pode encontrar mais informações sobre colunas de saída das diferentes tarefas de aprendizado de máquina na guia [Tarefas de Aprendizado de Máquina](resources/tasks.md).

Uma propriedade importante de objetos DataView é que eles são avaliados **lentamente**. Exibições de dados só são carregadas e operadas durante o treinamento e a avaliação do modelo e a previsão de dados. Enquanto você está escrevendo e testando seu aplicativo do ML.NET, pode usar o depurador do Visual Studio para dar uma espiada em qualquer objeto de exibição de dados chamando o método [Preview](xref:Microsoft.ML.DebuggerExtensions.Preview%2A).

```csharp
    var debug = testPriceDataView.Preview();
```

Você pode assistir à variável `debug` no depurador e examinar seu conteúdo. Não use o método Preview em código de produção, pois ele reduz significativamente o desempenho.

### <a name="model-deployment"></a>Implantação de Modelo

Em aplicativos da vida real, seu código de avaliação e modelo de treinamento serão separados da sua previsão. Na verdade, essas duas atividades geralmente são executadas por equipes separadas. Sua equipe de desenvolvimento do modelo pode salvar o modelo para uso no aplicativo de previsão.

```csharp
   mlContext.Model.Save(model, trainingData.Schema,"model.zip");
```

## <a name="next-steps"></a>Próximas etapas

* Saiba como criar aplicativos usando tarefas de aprendizado de máquina diferentes com conjuntos de dados mais realistas nos [tutoriais](./tutorials/index.md).

* Saiba mais sobre tópicos específicos em mais detalhes nos [guias de instruções](./how-to-guides/index.md).

* Se você estiver superando, poderá se aprofundar diretamente na [documentação de referência da API](../../api/index.md?view=ml-dotnet).
