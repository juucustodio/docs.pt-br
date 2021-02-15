---
title: 'Tutorial: detectar anomalias em chamadas telefônicas'
description: Saiba como criar um aplicativo de detecção de anomalias para dados de série temporal. Este tutorial cria um aplicativo de console .NET Core usando C# no Visual Studio 2019.
ms.date: 12/04/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: f001cb912bb695a7edb0917f3306ca9bfbe311ac
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98187776"
---
# <a name="tutorial-detect-anomalies-in-time-series-with-mlnet"></a>Tutorial: detectar anomalias na série temporal com ML.NET

Saiba como criar um aplicativo de detecção de anomalias para dados de série temporal. Este tutorial cria um aplicativo de console .NET Core usando C# no Visual Studio 2019.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
>
> * Carregar os dados
> * Detectar período para uma série temporal
> * Detectar anomalias para uma série de tempo periódico

Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/PhoneCallsAnomalyDetection).

## <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio 2019 versão 16.7.8 ou posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) com a carga de trabalho "desenvolvimento de plataforma cruzada do .NET Core" instalada.

* [O conjunto de phone-calls.csv DataSet](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrEntireDetection/Data/phone-calls.csv).

## <a name="create-a-console-application"></a>Criar um aplicativo de console

1. Crie um **aplicativo de console do .NET Core em C#** chamado "ProductSalesAnomalyDetection".

2. Crie um diretório chamado *dados* em seu projeto para salvar os arquivos do conjunto de dados.

3. Instalar o **Pacote NuGet Microsoft.ML**:

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**. Escolha "nuget.org" como a origem do pacote, selecione a guia procurar, procure **Microsoft.ml** e selecione o botão **instalar** . Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados. Repita essas etapas para **Microsoft. ml. timeseries**.

4. Adicione as seguintes instruções `using` à parte superior do arquivo *Program.cs*:

    [!code-csharp[AddUsings](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a>Baixar seus dados

1. Baixe o conjunto de dados e salve-o na pasta *Data* criada anteriormente:

    Clique com o botão direito do mouse em [*phone-calls.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrEntireDetection/Data/phone-calls.csv) e selecione "Salvar link (ou destino) como..."

     Salve o arquivo \*.csv na pasta *Data* ou, depois de salvá-lo em outro lugar, mova o arquivo \*.csv para a pasta *Data*.

2. No Gerenciador de Soluções, clique com o botão direito do mouse no arquivo \*.csv e selecione **Propriedades**. Em **avançado**, altere o valor de **copiar para diretório de saída** para **copiar se mais recente**.

A tabela a seguir é uma visualização de dados do seu arquivo \*.csv:

| timestamp  | value |
|--------|--------------|
| 2018/9/3  | 36,69670857  |
| 2018/9/4  | 35,74160571  |
| .....  | .....  |
| 2018/10/3  | 34,49893429  |
| ...    | ....   |

Esse arquivo representa uma série temporal. Cada linha no arquivo é um ponto de dados. Cada ponto de dados tem dois atributos, `timestamp` ou seja, e `value` , para representar o número de chamadas telefônicas a cada dia. O número de chamadas telefônicas é transformado em diferenciação.

### <a name="create-classes-and-define-paths"></a>Criar classes e definir demarcadores

Em seguida, defina suas estruturas de dados de classe de entrada e de previsão.

Adicione uma nova classe ao seu projeto:

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, em seguida, selecione **Adicionar > Novo Item**.

2. Na **caixa de diálogo Adicionar novo item**, selecione **classe** e altere o campo **nome** para *PhoneCallsData.cs*. Em seguida, selecione o botão **Adicionar**.

   O arquivo *PhoneCallsData.cs* é aberto no editor de código.

3. Adicione a seguinte `using` instrução à parte superior de *PhoneCallsData.cs*:

   ```csharp
   using Microsoft.ML.Data;
   ```

4. Remova a definição de classe existente e adicione o código a seguir, que tem duas classes `PhoneCallsData` e `PhoneCallsPrediction` , ao arquivo *PhoneCallsData.cs* :

    [!code-csharp[DeclareTypes](./snippets/phone-calls-anomaly-detection/csharp/PhoneCallsData.cs#DeclareTypes "Declare data record types")]

    `PhoneCallsData` especifica uma classe de dados de entrada. O atributo [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) especifica quais colunas (por índice de coluna) no conjunto de dados devem ser carregadas. Ele tem dois atributos `timestamp` e `value` correspondem aos mesmos atributos no arquivo de dados.

    `PhoneCallsPrediction` especifica a classe de dados de previsão. Para o detector SR-CNN, a previsão depende do [modo de detecção](xref:Microsoft.ML.TimeSeries.SrCnnDetectMode) especificado. Neste exemplo, selecionamos o `AnomalyAndMargin` modo. A saída contém sete colunas. Na maioria dos casos,,, `IsAnomaly` `ExpectedValue` `UpperBoundary` e `LowerBoundary` são informais o suficiente. Eles informam se um ponto é uma anomalia, o valor esperado do ponto e a região de limite inferior/superior do ponto.

5. Adicione o seguinte código à linha à direita acima do `Main` método para especificar o caminho para o arquivo de dados:

    [!code-csharp[Declare global variables](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a>Inicializar variáveis em Main

1. Substitua a linha `Console.WriteLine("Hello World!")` no método `Main` pelo seguinte código para declarar e inicializar a variável `mlContext`:

    [!code-csharp[CreateMLContext](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateMLContext "Create the ML Context")]

    A [classe MLContext](xref:Microsoft.ML.MLContext) é um ponto de partida para todas as operações do ML.NET e a inicialização do `mlContext` cria um ambiente do ML.NET que pode ser compartilhado entre os objetos de fluxo de trabalho da criação de modelo. Ele é semelhante, conceitualmente, a `DBContext` no Entity Framework.

### <a name="load-the-data"></a>Carregar os dados

Os dados do ML.NET são representados como uma [classe IDataView](xref:Microsoft.ML.IDataView). `IDataView` é uma maneira flexível e eficiente de descrever dados tabulares (numéricos e texto). Os dados podem ser carregados de um arquivo de texto ou de outras fontes (por exemplo, banco de dados SQL ou arquivos de log) para um objeto `IDataView`.

1. Adicione o seguinte código como a próxima linha do método `Main`:

    [!code-csharp[LoadData](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#LoadData "loading dataset")]

    O [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) define o esquema de dados e lê o arquivo. Ele usa as variáveis de caminho de dados e retorna uma `IDataView`.

## <a name="time-series-anomaly-detection"></a>Detecção de anomalias de série temporal

Detecção de anomalias de série temporal é o processo de detectar exceções de dados de série temporal; pontos em uma determinada série temporal de entrada em que o comportamento não é o esperado, ou "estranho". Essas anomalias normalmente são indicativas de alguns eventos de interesse no domínio problemático: um ataque cibernético em contas de usuário, queda de energia, disparo de RPS em um servidor, vazamento de memória, etc.

Para localizar anomalias na série temporal, você deve primeiro determinar o período da série. Em seguida, a série temporal pode ser decomposta em vários componentes como `Y = T + S + R` , onde `Y` é a série original, `T` é o componente de tendência, `S` é o componente sazonal e `R` é o componente residual da série. Essa etapa é chamada de [decomposição](https://en.wikipedia.org/wiki/Decomposition_of_time_series). Por fim, a detecção é executada no componente residual para localizar as anomalias. No ML.NET, o algoritmo SR-CNN é um algoritmo avançado e romance baseado em Spectral residuais (SR) e rede neural (CNN) para detectar anomalias na série temporal. Para obter mais informações sobre esse algoritmo, consulte [serviço de detecção de anomalias de série temporal na Microsoft](https://arxiv.org/pdf/1906.03821.pdf).

Neste tutorial, você verá que esses procedimentos podem ser concluídos usando duas funções.

## <a name="detect-period"></a>Período de detecção

Na primeira etapa, invocamos a `DetectSeasonality` função para determinar o período da série.

### <a name="create-the-detectperiod-method"></a>Criar o método DetectPeriod

1. Crie o `DetectPeriod` método, logo abaixo do `Main` método, usando o seguinte código:

    ```csharp
    static void DetectPeriod(MLContext mlContext, IDataView phoneCalls)
    {

    }
    ```

2. Use a <xref:Microsoft.ML.TimeSeriesCatalog.DetectSeasonality%2A> função para detectar o período. Adicione-o ao método `DetectPeriod` com o seguinte código:

    [!code-csharp[DetectSeasonality](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectSeasonality)]

3. Exiba o valor do período adicionando o seguinte como a próxima linha de código no `DetectPeriod` método:

    [!code-csharp[DisplayPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayPeriod)]

4. Adicione a seguinte chamada ao `DetectPeriod` método no `Main` método:

    [!code-csharp[CallDetectPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectPeriod)]

### <a name="period-detection-results"></a>Resultados da detecção de período

Execute o aplicativo. Seus resultados devem ser semelhantes aos seguintes.

```console
Period of the series is: 7.
```

## <a name="detect-anomaly"></a>Detectar anomalias

Nesta etapa, você usa o <xref:Microsoft.ML.TimeSeriesCatalog.DetectEntireAnomalyBySrCnn%2A> método para localizar anomalias.

### <a name="create-the-detectanomaly-method"></a>Criar o método DetectAnomaly

1. Crie o `DetectAnomaly` método, logo abaixo do `DetectPeriod` método, usando o seguinte código:

    ```csharp
    static void DetectAnomaly(MLContext mlContext, IDataView phoneCalls, int period)
    {

    }
    ```

2. Configure <xref:Microsoft.ML.TimeSeries.SrCnnEntireAnomalyDetectorOptions> no `DetectAnomaly` método com o seguinte código:

    [!code-csharp[SetupSrCnnParameters](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#SetupSrCnnParameters)]

3. Detecte anomalias pelo algoritmo SR-CNN adicionando a seguinte linha de código ao `DetectAnomaly` método:

    [!code-csharp[DetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectAnomaly)]

4. Converta a exibição de dados de saída em um tipo fortemente tipado `IEnumerable` para facilitar a exibição usando o [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) método com o seguinte código:

    [!code-csharp[CreateEnumerableForResult](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateEnumerableForResult)]

5. Crie um cabeçalho de exibição com o código a seguir como a próxima linha no método `DetectAnomaly`:

    [!code-csharp[DisplayHeader](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayHeader)]

    Você exibirá as informações a seguir nos resultados da detecção de ponto de alteração:

    * `Index` é o índice de cada ponto.
    * `Anomaly` é o indicador de se cada ponto é detectado como anomalia.
    * `ExpectedValue` é o valor estimado de cada ponto.
    * `LowerBoundary` é o menor valor que cada ponto pode ser não ser anormal.
    * `UpperBoundary` é o maior valor que cada ponto pode ser não ser anormal.

6. Itere por meio do `predictions` `IEnumerable` e exiba os resultados com o seguinte código:

    [!code-csharp[DisplayAnomalyDetectionResults](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayAnomalyDetectionResults)]

7. Adicione a seguinte chamada ao `DetectAnomaly` método no `Main` método:

    [!code-csharp[CallDetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectAnomaly)]

## <a name="anomaly-detection-results"></a>Resultados da detecção de anomalias

Execute o aplicativo. Seus resultados devem ser semelhantes aos seguintes. Durante o processamento, as mensagens são exibidas. Você pode ver avisos ou mensagens de processamento. Algumas mensagens foram removidas dos resultados a seguir para fins de clareza.

```console
Detect period of the series
Period of the series is: 7.
Detect anomaly points in the series
Index   Data    Anomaly AnomalyScore    Mag     ExpectedValue   BoundaryUnit    UpperBoundary   LowerBoundary
0,0,36.841787256739266,41.14206982401966,32.541504689458876
1,0,35.67303618137362,39.97331874865401,31.372753614093227
2,0,34.710132999891826,39.029491313022824,30.390774686760828
3,0,33.44765248883495,37.786086547816545,29.10921842985335
4,0,28.937110922276364,33.25646923540736,24.61775260914537
5,0,5.143895892785781,9.444178460066171,0.843613325505391
6,0,5.163325228419392,9.463607795699783,0.8630426611390014
7,0,36.76414836240396,41.06443092968435,32.46386579512357
8,0,35.77908590657007,40.07936847385046,31.478803339289676
9,0,34.547259536635245,38.847542103915636,30.246976969354854
10,0,33.55193524820608,37.871293561337076,29.23257693507508
11,0,29.091800129624648,33.392082696905035,24.79151756234426
12,0,5.154836630338823,9.455119197619213,0.8545540630584334
13,0,5.234332502492464,9.534615069772855,0.934049935212073
14,0,36.54992549471526,40.85020806199565,32.24964292743487
15,0,35.79526470980883,40.095547277089224,31.494982142528443
16,0,34.34099013096804,38.64127269824843,30.040707563687647
17,0,33.61201516582131,37.9122977331017,29.31173259854092
18,0,29.223563320561812,33.5238458878422,24.923280753281425
19,0,5.170512168851533,9.470794736131923,0.8702296015711433
20,0,5.2614938889462834,9.561776456226674,0.9612113216658926
21,0,36.37103858487317,40.67132115215356,32.07075601759278
22,0,35.813544599026855,40.113827166307246,31.513262031746464
23,0,34.05600492733225,38.356287494612644,29.755722360051863
24,0,33.65828319077884,37.95856575805923,29.358000623498448
25,0,29.381125690882463,33.681408258162854,25.080843123602072
26,0,5.261543539820418,9.561826107100808,0.9612609725400283
27,0,5.4873712582971805,9.787653825577571,1.1870886910167897
28,1,36.504694001629254,40.804976568909645,32.20441143434886  <-- alert is on, detected anomaly
...
```

Parabéns! Agora você criou com êxito modelos de aprendizado de máquina para detectar períodos e anomalias em uma série temporal.

Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/PhoneCallsAnomalyDetection).

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
>
> * Carregar os dados
> * Detectar período nos dados de série temporal
> * Detectar anomalias nos dados de série temporal

## <a name="next-steps"></a>Próximas etapas

Confira o repositório do GitHub de exemplos de Machine Learning para explorar um exemplo de Detecção de Anomalias de Consumo de Energia.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-samples GitHub repository](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)
