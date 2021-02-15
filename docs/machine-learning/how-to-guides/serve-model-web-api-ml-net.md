---
title: Implantar um modelo em uma API Web do ASP.NET Core
description: Usar um modelo de Machine Learning para Análise de Sentimento com ML.NET pela internet usando o ASP.NET Web API
ms.date: 11/07/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: f588d4681ee277ad15b50d5553473b1c9e84d578
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608758"
---
# <a name="deploy-a-model-in-an-aspnet-core-web-api"></a>Implantar um modelo em uma API Web do ASP.NET Core

Saiba como fornecer um modelo de machine Learning do ML.NET previamente treinado na Web usando uma API Web do ASP.NET Core. Veicular um modelo por uma API Web habilita previsões por meio de métodos HTTP padrão.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) ou posterior ou visual Studio 2017 versão 15,6 ou posterior com a carga de trabalho "desenvolvimento de plataforma cruzada do .NET Core" instalada.
- PowerShell.
- Modelo previamente treinado. Use o [tutorial de Análise de Sentimento do ML.NET](../tutorials/sentiment-analysis.md) para criar seu próprio modelo ou baixe este [modelo de machine learning de análise de sentimento pré-treinado](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)

## <a name="create-aspnet-core-web-api-project"></a>Criar o projeto da API Web do ASP.NET Core

1. Abra o Visual Studio 2017. No menu, selecione **Arquivo > Novo > Projeto**. Na caixa de diálogo Novo projeto, selecione o nó **Visual C#** seguido pelo nó **Web**. Em seguida, selecione o modelo de projeto **Aplicativo ASP.NET Core Web**. Na caixa de texto **Nome**, digite "SentimentAnalysisWebAPI" e, depois, selecione o botão **OK**.

1. Na janela que exibe os diferentes tipos de projetos do ASP.NET Core, selecione **API** e, depois, o botão **OK**.

1. Crie um diretório chamado *MLModels* em seu projeto para salvar os arquivos de modelo de machine learning criados previamente:

    No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione Adicionar > Nova Pasta. Digite "MLModels" e pressione ENTER.

1. Instalar o **Pacote NuGet Microsoft.ML**:

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a Origem do pacote, selecione a guia Procurar, pesquise por **Microsoft.ML**, selecione o pacote na lista e escolha o botão Instalar. Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo Aceitação da Licença, se concordar com o termos de licença para os pacotes listados.

1. Instalar o **Pacote do Nuget Microsoft.Extensions.ML**:

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a origem do pacote, selecione a guia Procurar, pesquise **Microsoft.Extensions.ML**, selecione o pacote na lista e selecione o botão Instalar. Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo Aceitação da Licença, se concordar com o termos de licença para os pacotes listados.

### <a name="add-model-to-aspnet-core-web-api-project"></a>Adicionar um modelo ao projeto da API Web do ASP.NET Core

1. Copie seu modelo previamente criado para o diretório *MLModels*
1. No Gerenciador de Soluções, clique com o botão direito do mouse no arquivo zip e selecione Propriedades. Em Avançado, altere o valor de Copiar para diretório de saída para Copiar se for mais novo.

## <a name="create-data-models"></a>Criar modelo de dados

Você precisa criar algumas classes para os dados e previsões de entrada. Adicione uma nova classe ao seu projeto:

1. Crie um diretório chamado *DataModels* em seu projeto para salvar os modelos de dados:

    No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione Adicionar > Nova Pasta. Digite "datamodels" e pressione **Enter**.

2. No Gerenciador de Soluções, clique com o botão direito do mouse no diretório *DataModels* e selecione Adicionar > Novo item.
3. Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *SentimentData.cs*. Em seguida, selecione o botão **Adicionar**. O arquivo *SentimentData.cs* é aberto no editor de códigos. Adicione a seguinte instrução using na parte superior do *SentimentData.cs*:

    ```csharp
    using Microsoft.ML.Data;
    ```

    Remova a definição de classe existente e adicione o seguinte código ao arquivo **SentimentData.cs** :

    ```csharp
    public class SentimentData
    {
        [LoadColumn(0)]
        public string SentimentText;

        [LoadColumn(1)]
        [ColumnName("Label")]
        public bool Sentiment;
    }
    ```

4. Em Gerenciador de Soluções, clique com o botão direito do mouse no diretório *datamodelos* e selecione **Adicionar > novo item**.
5. Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *SentimentPrediction.cs*. Em seguida, selecione o botão Adicionar. O arquivo *SentimentPrediction.cs* é aberto no editor de códigos. Adicione a seguinte instrução "using" na parte superior do *SentimentPrediction.cs*:

    ```csharp
    using Microsoft.ML.Data;
    ```

    Remova a definição de classe existente e adicione o seguinte código ao arquivo *SentimentPrediction.cs*:

    ```csharp
    public class SentimentPrediction : SentimentData
    {

        [ColumnName("PredictedLabel")]
        public bool Prediction { get; set; }

        public float Probability { get; set; }

        public float Score { get; set; }
    }
    ```

    `SentimentPrediction` herda de `SentimentData`. Isso torna mais fácil ver os dados originais na propriedade `SentimentText` junto com a saída gerada pelo modelo.

## <a name="register-predictionenginepool-for-use-in-the-application"></a>Registrar PredictionEnginePool para uso no aplicativo

Para fazer uma única previsão, você precisa criar um [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) . [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) Não é thread-safe. Além disso, você precisa criar uma instância dela em qualquer lugar em que seja necessário dentro de seu aplicativo. À medida que seu aplicativo cresce, esse processo pode se tornar não gerenciável. Para melhorar o desempenho e a segurança do thread, use uma combinação de injeção de dependência e o `PredictionEnginePool` serviço, que cria um [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) dos [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) objetos para uso em todo o aplicativo.

O link a seguir fornece mais informações se você quiser saber mais sobre [injeção de dependência em ASP.NET Core](/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1).

1. Abra a classe *Startup.cs* e adicione a seguinte instrução using à parte superior do arquivo:

    ```csharp
    using Microsoft.AspNetCore.Builder;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

2. Adicione o seguinte código ao método *ConfigureServices*:

    ```csharp
    services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
        .FromFile(modelName: "SentimentAnalysisModel", filePath:"MLModels/sentiment_model.zip", watchForChanges: true);
    ```

Em um alto nível, esse código inicializa os objetos e os serviços automaticamente para uso posterior quando solicitado pelo aplicativo em vez de ter que fazê-lo manualmente.

Os modelos de aprendizado de máquina não são estáticos. À medida que novos dados de treinamento ficam disponíveis, o modelo é retreinado e reimplantado. Uma maneira de obter a versão mais recente do modelo em seu aplicativo é reimplantar o aplicativo inteiro. No entanto, isso introduz o tempo de inatividade do aplicativo. O `PredictionEnginePool` serviço fornece um mecanismo para recarregar um modelo atualizado sem desativar o aplicativo.

Defina o `watchForChanges` parâmetro como `true` e o `PredictionEnginePool` inicia um [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher) que escuta as notificações de alteração do sistema de arquivos e gera eventos quando há uma alteração no arquivo. Isso solicita que o `PredictionEnginePool` recarregue automaticamente o modelo.

O modelo é identificado pelo `modelName` parâmetro para que mais de um modelo por aplicativo possa ser recarregado após a alteração.

> [!TIP]
> Como alternativa, você pode usar o `FromUri` método ao trabalhar com modelos armazenados remotamente. Em vez de observar os eventos de alteração de arquivo, `FromUri` o pesquisa o local remoto em busca de alterações. O padrão do intervalo de sondagem é de 5 minutos. Você pode aumentar ou diminuir o intervalo de sondagem com base nos requisitos do seu aplicativo. No exemplo de código abaixo, o `PredictionEnginePool` sonda o modelo armazenado no URI especificado a cada minuto.
>
>```csharp
>services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
>   .FromUri(
>       modelName: "SentimentAnalysisModel",
>       uri:"https://github.com/dotnet/samples/raw/master/machine-learning/models/sentimentanalysis/sentiment_model.zip",
>       period: TimeSpan.FromMinutes(1));
>```

## <a name="create-predict-controller"></a>Criar o Controlador de Previsão

Para processar as solicitações HTTP de entrada, crie um controlador.

1. No Gerenciador de Soluções, clique com o botão direito do mouse no diretório *Controladores* e selecione **Adicionar > Controlador**.
1. Na caixa de diálogo **Adicionar Novo Item**, selecione **Controlador de API Vazio** e, então, **Adicionar**.
1. No prompt, altere o campo do **Nome do Controlador** para *PredictController.cs*. Em seguida, selecione o botão Adicionar. O arquivo *PredictController.cs* é aberto no editor de códigos. Adicione a seguinte instrução using na parte superior do *PredictController.cs*:

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

    Remova a definição de classe existente e adicione o seguinte código ao arquivo *PredictController.cs*:

    ```csharp
    public class PredictController : ControllerBase
    {
        private readonly PredictionEnginePool<SentimentData, SentimentPrediction> _predictionEnginePool;

        public PredictController(PredictionEnginePool<SentimentData,SentimentPrediction> predictionEnginePool)
        {
            _predictionEnginePool = predictionEnginePool;
        }

        [HttpPost]
        public ActionResult<string> Post([FromBody] SentimentData input)
        {
            if(!ModelState.IsValid)
            {
                return BadRequest();
            }

            SentimentPrediction prediction = _predictionEnginePool.Predict(modelName: "SentimentAnalysisModel", example: input);

            string sentiment = Convert.ToBoolean(prediction.Prediction) ? "Positive" : "Negative";

            return Ok(sentiment);
        }
    }
    ```

Esse código atribui o `PredictionEnginePool` passando-o para o construtor do controlador que você obtém por meio da injeção de dependência. Em seguida, o `Predict` método do controlador `Post` usa o `PredictionEnginePool` para fazer previsões usando o `SentimentAnalysisModel` registrado na `Startup` classe e retorna os resultados de volta para o usuário, se for bem-sucedido.

## <a name="test-web-api-locally"></a>Testar a API Web localmente

Depois que tudo estiver definido, é hora de testar o aplicativo.

1. Executar o aplicativo.
1. Abra o PowerShell e insira o código a seguir, em que porta é a porta na qual seu aplicativo está escutando.

    ```powershell
    Invoke-RestMethod "https://localhost:<PORT>/api/predict" -Method Post -Body (@{SentimentText="This was a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    Se houver êxito, a saída deverá ser semelhante ao texto abaixo:

    ```powershell
    Negative
    ```

Parabéns! Você usou com êxito seu modelo para fazer previsões pela internet usando um ASP.NET Core API Web.

## <a name="next-steps"></a>Próximas etapas

- [Implantar no Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure)
