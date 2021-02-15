---
title: Glossário de aprendizado de máquina
description: Um glossário de termos essenciais sobre o aprendizado de máquina, que são úteis ao criar seus modelos personalizados no ML.NET.
ms.topic: reference
ms.date: 07/31/2019
ms.openlocfilehash: 32ccb6df1cb08db45ebd25a0d1c0ea4396a6c50b
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223739"
---
# <a name="machine-learning-glossary-of-important-terms"></a>Glossário de aprendizado de máquina com termos importantes

A lista a seguir é uma compilação de termos essenciais sobre o aprendizado de máquina, que são úteis ao criar seus modelos personalizados no ML.NET.

## <a name="accuracy"></a>Precisão

Na [classificação](#classification), a precisão consiste no número de itens classificados corretamente dividido pelo número total de itens no conjunto de testes. Varia de 0 (menos preciso) a 1 (mais preciso). A precisão é uma das métricas de avaliação do desempenho do modelo. Considere isso em conjunção com [precisão](#precision), [recall](#recall)e [F-score](#f-score).

## <a name="area-under-the-curve-auc"></a>Área sob a curva (AUC)

Na [classificação binária](#binary-classification), uma métrica de avaliação que é o valor da área sob a curva que plota a taxa de positivos reais (no eixo y) em relação à taxa de falsos positivos (no eixo x). Varia de 0,5 (pior) a 1 (melhor). Também conhecida como a área sob a curva ROC, isto é, a curva característica de operação do receptor. Para obter mais informações, consulte o artigo [Característica de operação do receptor](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) na Wikipédia.

## <a name="binary-classification"></a>Classificação binária

Um caso de [classificação](#classification), em que o [rótulo](#label) é apenas uma das duas classes. Para saber mais, confira a seção [Classificação binária](tasks.md#binary-classification) do tópico [Tarefas de aprendizado de máquina](tasks.md).

## <a name="calibration"></a>Calibragem

Calibragem é o processo de mapear uma pontuação bruta em uma associação de classe para classificação binária e multiclasse. Alguns treinadores do ML.NET têm um sufixo `NonCalibrated`. Esses algoritmos produzem uma pontuação bruta que deve ser mapeada para uma probabilidade de classe.

## <a name="catalog"></a>Catálogo

No ML.NET, um catálogo é uma coleção de funções de extensão agrupadas por um objetivo em comum.

Por exemplo, cada tarefa de aprendizado de máquina (classificação binária, regressão, classificação etc.) tem um catálogo de algoritmos de aprendizado de máquina disponível (treinadores). O catálogo para os treinadores de classificação binária é: <xref:Microsoft.ML.BinaryClassificationCatalog.BinaryClassificationTrainers>.

## <a name="classification"></a>Classificação

Quando os dados são usados ​​para prever uma categoria, a tarefa de [aprendizado de máquina supervisionado](#supervised-machine-learning) é chamada de classificação. [Classificação binária](#binary-classification) refere-se à previsão de apenas duas categorias (por exemplo, classificar uma imagem como uma figura de um "gato" ou um "cachorro"). [Classificação multiclasse](#multiclass-classification) refere-se à previsão de várias categorias (por exemplo, ao classificar uma imagem como uma imagem de uma raça específica de cão).

## <a name="coefficient-of-determination"></a>Coeficiente de determinação

Na [regressão](#regression), uma métrica de avaliação que indica como os dados se ajustam a um modelo. Varia de 0 a 1. Um valor de 0 significa que os dados são aleatórios ou não podem ser ajustados ao modelo. Um valor de 1 significa que o modelo corresponde exatamente aos dados. Geralmente denominado como r<sup>2</sup>, R<sup>2</sup>, ou r-quadrado.

## <a name="data"></a>Dados

Os dados são essenciais para qualquer aplicativo de aprendizado de máquina. No ML.NET, os dados são representados por objetos <xref:Microsoft.ML.IDataView>. Objetos de exibição de dados:

- são compostos por colunas e linhas
- são avaliados lentamente, ou seja, apenas carregam dados quando uma operação exige
- contém um esquema que define o tipo, o formato e o tamanho de cada coluna

## <a name="estimator"></a>Avaliador

Uma classe em ML.NET que implementa a interface <xref:Microsoft.ML.IEstimator%601>.

Um estimador é uma especificação de uma transformação (transformação de preparação de dados e transformação de treinamento do modelo de machine learning). Estimadores podem ser encadeados em um pipeline de transformações. Os parâmetros de um estimador ou pipeline de estimadores são aprendidos quando <xref:Microsoft.ML.IEstimator%601.Fit%2A> é chamado. O resultado de <xref:Microsoft.ML.IEstimator%601.Fit%2A> é um [Transformador](#transformer).

## <a name="extension-method"></a>Método de extensão

Um método do .NET que faz parte de uma classe, mas é definido fora da classe. O primeiro parâmetro de um método de extensão é uma referência `this` estática à classe à qual o método de extensão pertence.

Métodos de extensão são usados amplamente no ML.NET para construir instâncias de [estimadores](#estimator).

## <a name="feature"></a>Recurso

Uma propriedade mensurável do fenômeno que está sendo medido, normalmente um valor numérico (duplo). Vários recursos são referidos como **Vetor de recursos** e normalmente armazenados como `double[]`. As características definem as características importantes do fenômeno que está sendo medido. Para obter mais informações, consulte o artigo [Recurso](https://en.wikipedia.org/wiki/Feature_(machine_learning)) na Wikipédia.

## <a name="feature-engineering"></a>Engenharia de recursos

A engenharia de recursos é o processo que envolve a definição de um conjunto de [recursos](#feature) e o desenvolvimento de software que produz vetores de recursos a partir de dados de fenômenos disponíveis, ou seja, a extração de recursos. Para obter mais informações, consulte o artigo [Engenharia de recursos](https://en.wikipedia.org/wiki/Feature_engineering) na Wikipédia.

## <a name="f-score"></a>F-score

Na [classificação](#classification), uma métrica de avaliação que equilibra [precisão](#precision) e [recall](#recall).

## <a name="hyperparameter"></a>Hiperparâmetro

Um parâmetro de um algoritmo de aprendizado de máquina. Os exemplos incluem o número de árvores a serem aprendidas em uma floresta de decisão ou o tamanho da etapa em um algoritmo descendente de gradiente. Os valores de *Hiperparâmetros* são definidos antes de treinar o modelo e controlar o processo de localização dos parâmetros da função de previsão, por exemplo, os pontos de comparação em uma árvore de decisão ou os pesos em um modelo de regressão linear. Para obter mais informações, consulte o artigo [Hiperparâmetro](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) na Wikipédia.

## <a name="label"></a>Rotular

O elemento a ser previsto com o modelo de aprendizado de máquina. Por exemplo, a raça do cão ou um preço futuro da ação.

## <a name="log-loss"></a>Perda de log

Na [classificação](#classification), uma métrica de avaliação que caracteriza a precisão de um classificador. Quanto menor a perda de log, mais preciso é um classificador.

## <a name="loss-function"></a>Função de perda

Uma função de perda é a diferença entre os valores de rótulo de treinamento e a previsão feita pelo modelo. Os parâmetros do modelo são estimados minimizando a função de perda.

Treinadores diferentes podem ser configurados com funções de perda diferentes.

## <a name="mean-absolute-error-mae"></a>Erro de média absoluta (MAE)

Na [regressão](#regression), uma métrica de avaliação que é a média de todos os erros de modelo, em que erro de modelo consiste na distância entre o valor do [rótulo](#label) previsto e o valor do rótulo correto.

## <a name="model"></a>Modelar

Tradicionalmente, os parâmetros para a função de previsão. Por exemplo, os pesos em um modelo de regressão linear ou os pontos de divisão em uma árvore de decisão. No ML.NET, um modelo contém todas as informações necessárias para prever o [rótulo](#label) de um objeto de domínio (por exemplo, imagem ou texto). Isso significa que os modelos ML.NET incluem as etapas de personalização necessárias, bem como os parâmetros para a função de previsão.

## <a name="multiclass-classification"></a>Classificação multiclasse

Um caso de [classificação](#classification) em que o [rótulo](#label) é uma entre três ou mais classes. Para saber mais, confira a seção [Classificação multiclasse](tasks.md#multiclass-classification) do tópico [Tarefas de aprendizado de máquina](tasks.md).

## <a name="n-gram"></a>N-grama

Um esquema de extração de recursos para dados de texto: qualquer sequência de N palavras se transforma em um valor de [recurso](#feature).

## <a name="normalization"></a>Normalização

A normalização é o processo de escala de dados de ponto flutuante para valores entre 0 e 1. Muitos dos algoritmos de treinamento usados no ML.NET exigem que os dados do recurso de entrada sejam normalizados. O ML.NET fornece uma série de [transformações para normalização](transforms.md#normalization-and-scaling)

## <a name="numerical-feature-vector"></a>Vetor de recurso numérico

Um vetor de [recurso](#feature) consistindo apenas em valores numéricos. Similar ao `double[]`.

## <a name="pipeline"></a>Pipeline

Todas as operações necessárias para ajustar um modelo a um conjunto de dados. Um pipeline consiste em etapas de importação, transformação, personalização e aprendizado de dados. Uma vez que um pipeline é treinado, ele se torna um modelo.

## <a name="precision"></a>Precisão

Na [classificação](#classification), a precisão de uma classe é o número de itens preditos corretamente como pertencentes a essa classe dividido pelo número total de itens previstos como pertencentes à classe.

## <a name="recall"></a>Chamar de volta

Na [classificação](#classification), o recall de uma classe é o número de itens preditos corretamente como pertencentes a essa classe dividido pelo número total de itens que realmente pertencem à classe.

## <a name="regularization"></a>Regularização

 Regularização penaliza um modelo linear por ser complicado demais. Há dois tipos de regularização:

- A regularização $L_1$ zera pesos para recursos insignificantes. O tamanho do modelo salvo pode ficar menor após esse tipo de regularização.
- $L _2 $ regularização minimiza o intervalo de peso para recursos insignificantes. Esse é um processo mais geral e é menos sensível a exceções.

## <a name="regression"></a>Regressão

Uma tarefa de [aprendizado de máquina supervisionado](#supervised-machine-learning) em que a saída é um valor real, por exemplo, duplo. Exemplos incluem a previsão de preços de ações. Para saber mais, confira a seção [Regressão](tasks.md#regression) do tópico [Tarefas de aprendizado de máquina](tasks.md).

## <a name="relative-absolute-error"></a>Erro absoluto relativo

Na [regressão](#regression), uma métrica de avaliação que é a soma de todos os erros absolutos dividida pela soma das distâncias entre os valores de [rótulo](#label) corretos e a média de todos os valores de rótulo corretos.

## <a name="relative-squared-error"></a>Erro quadrático relativo

Na [regressão](#regression), uma métrica de avaliação que é a soma de todos os erros absolutos quadráticos dividida pela soma das distâncias quadráticas entre os valores de [rótulo](#label) corretos e a média de todos os valores de rótulo corretos.

## <a name="root-of-mean-squared-error-rmse"></a>Raiz do erro quadrático médio (RMSE)

Na [regressão](#regression), uma métrica de avaliação que é a raiz quadrada da média dos quadrados dos erros.

## <a name="scoring"></a>Pontuação

A pontuação é o processo de aplicar novos dados a um modelo de machine learning treinado e gerar previsões. A pontuação também é conhecida como inferência. Dependendo do tipo de modelo, a pontuação pode ser um valor bruto, uma probabilidade ou uma categoria.

## <a name="supervised-machine-learning"></a>Aprendizado de máquina supervisionado

Uma subclasse de aprendizado de máquina na qual um modelo desejado prevê o rótulo para dados ainda não vistos. Exemplos incluem a classificação, regressão e previsão estruturada. Para obter mais informações, consulte o artigo [Aprendizado supervisionado](https://en.wikipedia.org/wiki/Supervised_learning) na Wikipédia.

## <a name="training"></a>Treinamento

O processo de identificar um [modelo](#model) para um determinado conjunto de dados de treinamento. Para um modelo linear, isso significa encontrar os pesos. Para uma árvore, isso envolve a identificação dos pontos de divisão.

## <a name="transformer"></a>Transformador

Uma classe do ML.NET que implemente a interface <xref:Microsoft.ML.ITransformer>.

Um transformador transforma um <xref:Microsoft.ML.IDataView> em outro. Um transformador é criado pelo treinamento de um [estimador](#estimator) ou um pipeline de estimador.

## <a name="unsupervised-machine-learning"></a>Aprendizado de máquina não supervisionado

Uma subclasse de aprendizado de máquina na qual um modelo desejado encontra estrutura oculta (ou latente) nos dados. Exemplos incluem clustering, modelagem de tópico e redução de dimensionalidade. Para obter mais informações, consulte o artigo [Aprendizado não supervisionado](https://en.wikipedia.org/wiki/Unsupervised_learning) na Wikipédia.
