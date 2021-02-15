---
title: 'Tutorial: analisar sentimentos – classificação binária'
description: Este tutorial mostra como criar um aplicativo Razor Pages que classifica as opiniões dos comentários do site e executa a ação apropriada. O classificador de sentimentos binários usa o construtor de modelos no Visual Studio.
ms.date: 11/21/2019
author: luisquintanilla
ms.author: luquinta
ms.topic: tutorial
ms.custom: mvc,mlnet-tooling
ms.openlocfilehash: 7761240055c90ae9c713b1c460e9e83316d256f9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2020
ms.locfileid: "81278945"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-in-a-web-application-using-mlnet-model-builder"></a>Tutorial: analisar o sentimentos dos comentários do site em um aplicativo Web usando o ML.NET Model Builder

Saiba como analisar sentimentos de comentários em tempo real dentro de um aplicativo Web.

Este tutorial mostra como criar um aplicativo ASP.NET Core Razor Pages que classifica as opiniões dos comentários do site em tempo real.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Criar um aplicativo de Razor Pages de ASP.NET Core
> - Preparar e compreender os dados
> - Escolha um cenário
> - Carregar os dados
> - Treinar o modelo
> - Avaliar o modelo
> - Usar o modelo para previsões

> [!NOTE]
> O Construtor de Modelo está atualmente na Versão Prévia.

Você pode encontrar o código-fonte deste tutorial no repositório [dotnet/MachineLearning-Samples](https://github.com/dotnet/machinelearning-samples) .

## <a name="pre-requisites"></a>Pré-requisitos

Para obter uma lista de pré-requisitos e instruções de instalação, visite o [guia de instalação do Construtor de Modelo](../how-to-guides/install-model-builder.md).

## <a name="create-a-razor-pages-application"></a>Criar um aplicativo Razor Pages

1. Crie um **aplicativo de Razor pages de ASP.NET Core**.

    1. Abra o Visual Studio e selecione **arquivo > novo projeto de >** na barra de menus.
    1. Na caixa de diálogo Novo projeto, selecione o nó **Visual C#** seguido pelo nó **Web**.
    1. Em seguida, selecione o modelo de projeto **Aplicativo ASP.NET Core Web**.
    1. Na caixa de texto **nome** , digite "SentimentRazor".
    1. Verifique se a opção **Colocar solução e projeto no mesmo diretório** está **desmarcada** (vs 2019) ou **criar diretório para solução** está **marcado** (vs 2017).
    1. Selecione o botão **OK** .
    1. Escolha **aplicativo Web** na janela que exibe os diferentes tipos de projetos de ASP.NET Core e, em seguida, selecione o botão **OK** .

## <a name="prepare-and-understand-the-data"></a>Preparar e compreender os dados

Baixe o [conjunto de Detox Wikipédia](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv). Quando a página da Web for aberta, clique com o botão direito do mouse na página, selecione **salvar como** e salve o arquivo em qualquer lugar no computador.

Cada linha no conjunto de *Detox da Wikipédia--line-data-250 o DataSet. tsv* representa uma revisão diferente deixada por um usuário na Wikipédia. A primeira coluna representa a folga do texto (0 é não tóxicos, 1 é tóxicos) e a segunda coluna representa o comentário deixado pelo usuário. As colunas são separadas por tabulações. Os dados são parecidos com os seguintes:

| Sentimento | SentimentText |
| :---: | :---: |
1 | = = RUDE = = cara, você é um carregamento rude que Carl imagem de volta ou outra coisa.
1 | = = OK! = = IM INDO PARA VANDALIZE DE CURINGAS E, EM SEGUIDA,!!!
0 | Espero que isso ajude.

## <a name="choose-a-scenario"></a>Escolha um cenário

![Assistente do construtor de modelos no Visual Studio](./media/sentiment-analysis-model-builder/model-builder-screen.png)

Para treinar seu modelo, você precisa selecionar na lista de cenários disponíveis de aprendizado de máquina fornecidos pelo Construtor de Modelo.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto *SentimentRazor* e selecione **Adicionar**  >  **Machine Learning**.
1. Para este exemplo, o cenário é análise de sentimentos. Na etapa *cenário* da ferramenta Construtor de modelos, selecione o cenário de **análise de sentimento** .

## <a name="load-the-data"></a>Carregar os dados

O construtor de modelos aceita dados de duas fontes, de um SQL Server um ou de um arquivo local no `csv` `tsv` formato ou.

1. Na etapa de dados da ferramenta do Construtor de Modelo, selecione **Arquivo** na lista suspensa da fonte de dados.
1. Selecione o botão ao lado da caixa de texto **selecionar um arquivo** e use o explorador de arquivos para procurar e selecionar o arquivo *Wikipédia-Detox-250-line-Data. tsv* .
1. Escolha **sentimentos** na **coluna para prever (rótulo)** DropDown.
1. Deixe os valores padrão para a lista suspensa **colunas de entrada (recursos)** .
1. Selecione o link **treinar** para mover para a próxima etapa na ferramenta do construtor de modelos.

## <a name="train-the-model"></a>Treinar o modelo

A tarefa de aprendizado de máquina usada para treinar o modelo de análise de sentimentos neste tutorial é a classificação binária. Durante o processo de treinamento do modelo, o construtor de modelos treina modelos separados usando diferentes algoritmos de classificação binária e configurações para encontrar o modelo de melhor desempenho para seu conjunto de seus conjuntos de seus.

O tempo necessário para treinar o modelo é proporcional à quantidade de dados. O construtor de modelos seleciona automaticamente um valor padrão para o **tempo de treinamento (segundos)** com base no tamanho da fonte de dados.

1. Embora o construtor de modelos defina o valor de **tempo para treinar (segundos)** como 10 segundos, aumente-o para 30 segundos. O treinamento para um período de tempo maior permite que o construtor de modelos Explore um número maior de algoritmos e uma combinação de parâmetros na pesquisa do melhor modelo.
1. Selecione **Iniciar Treinamento**.

    Durante o processo de treinamento, os dados de progresso são exibidos na seção `Progress` da etapa de treinamento.

    - O status exibe o status de conclusão do processo de treinamento.
    - A melhor precisão exibe a precisão do modelo de melhor desempenho encontrado pelo Construtor do Modelo até o momento. Maior precisão significa que o modelo é previsto mais corretamente nos dados de teste.
    - O melhor algoritmo exibe o nome do algoritmo de melhor desempenho executado encontrado pelo Construtor de Modelo até o momento.
    - O último algoritmo exibe o nome do algoritmo usado mais recentemente pelo Construtor de Modelo para treinar o modelo.

1. Quando o treinamento estiver concluído, selecione o link **avaliar** para passar para a próxima etapa.

## <a name="evaluate-the-model"></a>Avaliar o modelo

O resultado da etapa de treinamento será um modelo que tem o melhor desempenho. Na etapa avaliar da ferramenta Construtor de modelos, a seção saída conterá o algoritmo usado pelo melhor modelo de desempenho na melhor entrada de **modelo** , juntamente com as métricas na **melhor precisão do modelo**. Além disso, uma tabela de resumo contendo os cinco principais modelos e suas métricas é mostrada.

Se você não estiver satisfeito com suas métricas de precisão, algumas maneiras fáceis de tentar melhorar a precisão do modelo são aumentar a quantidade de tempo para treinar o modelo ou usar mais dados. Caso contrário, selecione o link de **código** para mover para a etapa final na ferramenta do construtor de modelos.

## <a name="add-the-code-to-make-predictions"></a>Adicionar o código para fazer previsões

Dois projetos serão criados como resultado do processo de treinamento.

### <a name="reference-the-trained-model"></a>Referenciar o modelo treinado

1. Na etapa de *código* da ferramenta Construtor de modelos, selecione **adicionar projetos** para adicionar os projetos gerados automaticamente à solução.

    Os projetos a seguir devem aparecer no **Gerenciador de soluções**:

    - *SentimentRazorML. ConsoleApp*: um aplicativo de console do .NET Core que contém o treinamento do modelo e o código de previsão.
    - *SentimentRazorML. Model*: um .net Standard biblioteca de classes que contém os modelos de dados que definem o esquema de dados de modelo de entrada e saída, bem como a versão salva do modelo de melhor desempenho durante o treinamento.

    Para este tutorial, somente o projeto *SentimentRazorML. Model* é usado porque as previsões serão feitas no aplicativo Web *SentimentRazor* , e não no console. Embora o *SentimentRazorML. ConsoleApp* não seja usado para pontuação, ele pode ser usado para treinar novamente o modelo usando novos dados em um momento posterior. No entanto, o novo treinamento está fora do escopo deste tutorial.

### <a name="configure-the-predictionengine-pool"></a>Configurar o pool PredictionEngine

Para fazer uma única previsão, você precisa criar um <xref:Microsoft.ML.PredictionEngine%602> . <xref:Microsoft.ML.PredictionEngine%602> não é thread-safe. Além disso, você precisa criar uma instância dela em qualquer lugar em que seja necessário dentro de seu aplicativo. À medida que seu aplicativo cresce, esse processo pode se tornar não gerenciável. Para melhorar o desempenho e a segurança do thread, use uma combinação de injeção de dependência e o `PredictionEnginePool` serviço, que cria um <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601> dos <xref:Microsoft.ML.PredictionEngine%602> objetos para uso em todo o aplicativo.

1. Instale o pacote NuGet do *Microsoft.Extensions.ml* :

    1. No **Gerenciador de Soluções**, clique com o botão direito no projeto e escolha **Gerenciar Pacotes NuGet**.
    1. Escolha "nuget.org" como a origem do pacote.
    1. Selecione a guia **procurar** e procure **Microsoft.Extensions.ml**.
    1. Selecione o pacote na lista e selecione o botão **instalar** .
    1. Selecione o botão **OK** na caixa de diálogo **Visualizar alterações**
    1. Selecione o botão **aceito** na caixa de diálogo de **aceitação da licença** se você concordar com os termos de licença dos pacotes listados.

1. Abra o arquivo *Startup.cs* no projeto *SentimentRazor* .
1. Adicione as seguintes instruções using para fazer referência ao pacote NuGet do *Microsoft.Extensions.ml* e ao projeto *SentimentRazorML. Model* :

    ```csharp
    using System.IO;
    using Microsoft.Extensions.ML;
    using SentimentRazorML.Model;
    ```

1. Crie uma variável global para armazenar o local do arquivo de modelo treinado.

    ```csharp
    private readonly string _modelPath;
    ```

1. O arquivo de modelo é armazenado no diretório de compilação junto com os arquivos de assembly do seu aplicativo. Para facilitar o acesso, crie um método auxiliar chamado `GetAbsolutePath` após o `Configure` método

    ```csharp
    public static string GetAbsolutePath(string relativePath)
    {
        FileInfo _dataRoot = new FileInfo(typeof(Program).Assembly.Location);
        string assemblyFolderPath = _dataRoot.Directory.FullName;

        string fullPath = Path.Combine(assemblyFolderPath, relativePath);
        return fullPath;
    }
    ```

1. Use o `GetAbsolutePath` método no `Startup` Construtor de classe para definir o `_modelPath` .

    ```csharp
    _modelPath = GetAbsolutePath("MLModel.zip");
    ```

1. Configure o `PredictionEnginePool` para seu aplicativo no `ConfigureServices` método:

    ```csharp
    services.AddPredictionEnginePool<ModelInput, ModelOutput>()
            .FromFile(_modelPath);
    ```

### <a name="create-sentiment-analysis-handler"></a>Criar manipulador de análise de sentimentos

As previsões serão feitas dentro da página principal do aplicativo. Portanto, um método que leva a entrada do usuário e usa o `PredictionEnginePool` para retornar uma previsão precisa ser adicionado.

1. Abra o arquivo *index.cshtml.cs* localizado no diretório *pages* e adicione as seguintes instruções using:

    ```csharp
    using Microsoft.Extensions.ML;
    using SentimentRazorML.Model;
    ```

    Para usar o `PredictionEnginePool` configurado na `Startup` classe, é necessário inseri-lo no construtor do modelo em que você deseja usá-lo.

1. Adicione uma variável para referenciar o `PredictionEnginePool` dentro da `IndexModel` classe.

    ```csharp
    private readonly PredictionEnginePool<ModelInput, ModelOutput> _predictionEnginePool;
    ```

1. Crie um construtor na `IndexModel` classe e insira o `PredictionEnginePool` serviço nele.

    ```csharp
    public IndexModel(PredictionEnginePool<ModelInput, ModelOutput> predictionEnginePool)
    {
        _predictionEnginePool = predictionEnginePool;
    }
    ```

1. Crie um manipulador de método que usa o `PredictionEnginePool` para fazer previsões da entrada do usuário recebida da página da Web.

    1. Abaixo do `OnGet` método, crie um novo método chamado `OnGetAnalyzeSentiment`

        ```csharp
        public IActionResult OnGetAnalyzeSentiment([FromQuery] string text)
        {

        }
        ```

    1. Dentro do `OnGetAnalyzeSentiment` método, retorne um sentimentos *neutro* se a entrada do usuário estiver em branco ou for nula.

        ```csharp
        if (String.IsNullOrEmpty(text)) return Content("Neutral");
        ```

    1. Dada uma entrada válida, crie uma nova instância do `ModelInput` .

        ```csharp
        var input = new ModelInput { SentimentText = text };
        ```

    1. Use o `PredictionEnginePool` para prever sentimentos.

        ```csharp
        var prediction = _predictionEnginePool.Predict(input);
        ```

    1. Converta o `bool` valor previsto em tóxicos ou não tóxicos com o código a seguir.

        ```csharp
        var sentiment = Convert.ToBoolean(prediction.Prediction) ? "Toxic" : "Not Toxic";
        ```

    1. Por fim, retorne a resposta para a página da Web.

        ```csharp
        return Content(sentiment);
        ```

### <a name="configure-the-web-page"></a>Configurar a página da Web

Os resultados retornados pelo `OnGetAnalyzeSentiment` serão exibidos dinamicamente na `Index` página da Web.

1. Abra o arquivo *index. cshtml* no diretório *pages* e substitua seu conteúdo pelo código a seguir:

    [!code-cshtml [IndexPage](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml)]

1. Em seguida, adicione o código de estilo CSS ao final da página *site. css* no diretório *wwwroot\css* :

    [!code-css [CssStyling](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/css/site.css#L61-L105)]

1. Depois disso, adicione o código para enviar entradas da página da Web para o `OnGetAnalyzeSentiment` manipulador.

    1. No arquivo de *site.js* localizado no diretório *wwwroot\js* , crie uma função chamada `getSentiment` para fazer uma solicitação HTTP Get com a entrada do usuário para o `OnGetAnalyzeSentiment` manipulador.

        [!code-javascript [GetSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L5-L10)]

    1. Abaixo disso, adicione outra função chamada `updateMarker` para atualizar dinamicamente a posição do marcador na página da Web como uma opinião é prevista.

        [!code-javascript [UpdateMarkerMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L12-L15)]

    1. Crie uma função de manipulador de eventos chamada `updateSentiment` para obter a entrada do usuário, enviá-la para a `OnGetAnalyzeSentiment` função usando a `getSentiment` função e atualizar o marcador com a `updateMarker` função.

        [!code-javascript [UpdateSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L17-L34)]

    1. Por fim, registre o manipulador de eventos e vincule-o ao `textarea` elemento com o `id=Message` atributo.

        [!code-javascript [UpdateSentimentEvtHandler](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L36)]

## <a name="run-the-application"></a>Executar o aplicativo

Agora que seu aplicativo está configurado, execute o aplicativo, que deve ser iniciado no navegador.

Quando o aplicativo for iniciado, insira o *Construtor de modelos é legal!* na área de texto. As opiniões previstas exibidas *não* devem ser tóxicos.

![Executando a janela com a janela de opiniões prevista](./media/sentiment-analysis-model-builder/web-app.png)

Se você precisar fazer referência aos projetos gerados pelo construtor de modelos em um momento posterior dentro de outra solução, você poderá encontrá-los dentro do `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` diretório.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
>
> - Criar um aplicativo de Razor Pages de ASP.NET Core
> - Preparar e compreender os dados
> - Escolha um cenário
> - Carregar os dados
> - Treinar o modelo
> - Avaliar o modelo
> - Usar o modelo para previsões

### <a name="additional-resources"></a>Recursos adicionais

Para saber mais sobre os tópicos mencionados neste tutorial, visite os seguintes recursos:

- [Cenários do Construtor de Modelo](../automate-training-with-model-builder.md#scenario)
- [Classificação binária](../resources/glossary.md#binary-classification)
- [Métricas do modelo de classificação binária](../resources/metrics.md#evaluation-metrics-for-binary-classification)
