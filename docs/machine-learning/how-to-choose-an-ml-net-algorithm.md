---
title: Como escolher um algoritmo do ML.NET
description: Saiba como escolher um algoritmo do ML.NET para seu modelo de machine learning
ms.topic: overview
ms.date: 06/05/2019
ms.openlocfilehash: 04cf191401c7c25f1fa341acaf9312dc19752260
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593084"
---
# <a name="how-to-choose-an-mlnet-algorithm"></a>Como escolher um algoritmo do ML.NET

Para cada [tarefa do ML.NET](resources/tasks.md), há vários algoritmos de treinamento para escolher. Qual escolher depende do problema que você está tentando resolver, das características de seus dados e dos recursos de computação e armazenamento disponíveis. É importante observar que o treinamento de um modelo de machine learning é um processo iterativo. Você talvez precise experimentar vários algoritmos para encontrar aquele que funciona melhor.

Algoritmos operam em **recursos**. Recursos são valores numéricos calculados usando seus dados de entrada. Eles são entradas ideais para algoritmos de machine learning. Você transforma seus dados brutos de entrada em recursos usando uma ou mais [transformações de dados](resources/transforms.md). Por exemplo, dados de texto são transformados em um conjunto de contagens de palavras e contagens de combinação de palavras. Depois que os recursos tiverem sido extraídos de um tipo de dados brutos usando transformações de dados, eles serão denominados **personalizados**. Por exemplo, texto personalizado ou dados de imagem personalizados.

## <a name="trainer--algorithm--task"></a>Treinador = Algoritmo + Tarefa

Um algoritmo é o cálculo executado para produzir um **modelo**. Diferentes algoritmos produzem modelos com características diferentes.

Com o do ML.NET, o mesmo algoritmo pode ser aplicado para tarefas diferentes. Por exemplo, estocásticos de coordenadas duplas podem ser usadas para classificação binária, classificação multiclasse e regressão. A diferença está em como a saída do algoritmo é interpretada de acordo com a tarefa.

Para cada combinação de algoritmo/tarefa, o ML.NET fornece um componente que executa o algoritmo de treinamento e faz a interpretação. Esses componentes são chamados de treinadores. Por exemplo, o <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer> usa o algoritmo **StochasticDualCoordinatedAscent** aplicado à tarefa **Regressão**.

## <a name="linear-algorithms"></a>Algoritmos lineares

Algoritmos lineares produzem um modelo que calcula **pontuações** de uma combinação linear de dados de entrada e um conjunto de **pesos**. Os pesos são os parâmetros do modelo estimado durante o treinamento.

Algoritmos lineares funcionam bem para recursos que são [separáveis linearmente](https://en.wikipedia.org/wiki/Linear_separability).

Antes do treinamento com um algoritmo linear, os recursos devem ser normalizados. Isso impede que um recurso tenha mais influência sobre o resultado do que outros.

Em geral, os algoritmos lineares são escalonáveis, rápidos, baratos de treinar e são baratos de prever. Eles são dimensionados pelo número de recursos e aproximadamente pelo tamanho do conjunto de dados de treinamento.

Algoritmos lineares fazem várias passagens sobre os dados de treinamento. Se seu conjunto de resultados couber na memória, adicionar um [ponto de verificação de cache](xref:Microsoft.ML.LearningPipelineExtensions.AppendCacheCheckpoint%2A) ao pipeline do ml.net antes de acrescentar o instrutor fará com que o treinamento seja executado mais rapidamente.

**Treinadores Lineares**

|Algoritmo|Propriedades|Treinadores|
|---------|----------|--------|
|Perceptron médio|Melhor para classificação de texto|<xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer>|
|Ascendente de coordenada dupla estocástico|Não é necessário ajuste para o bom desempenho padrão|<xref:Microsoft.ML.Trainers.SdcaLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer>|
|L-BFGS|Use quando o número de recursos for grande. Produz estatísticas de treinamento de regressão logística, mas não é dimensionado tão bem quanto o AveragedPerceptronTrainer|<xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.LbfgsMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.LbfgsPoissonRegressionTrainer>|
|Descendente de gradiente estocástico simbólico|Treinador de classificação binária linear o mais rápido e preciso. É bem dimensionado com vários processadores|<xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer>|

## <a name="decision-tree-algorithms"></a>Algoritmos de árvore de decisão

Algoritmos de árvore de decisão criam um modelo que contém uma série de decisões: efetivamente um fluxograma pelos valores de dados.

Recursos não precisam ser separáveis linearmente para usar esse tipo de algoritmo. E os recursos não precisam ser normalizados, pois os valores individuais no vetor de recurso são usados de modo independente no processo de decisão.

Algoritmos de árvore de decisão geralmente são muito precisos.

Exceto por GAMs (Modelos Aditivos Generalizados), modelos de árvore podem carecer da capacidade de explicação quando o número de recursos é grande.

Algoritmos de árvore de decisão consomem mais recursos e não são dimensionados tão bem quanto os lineares. Eles têm um bom desempenho em conjuntos de dados que cabem na memória.

Árvores de decisão aprimoradas são um conjunto de árvores de pequenas em que cada árvore pontua os dados de entrada e passa a pontuação para a árvore seguinte para produzir uma pontuação melhor, e assim por diante, em que cada árvore no conjunto melhora a anterior.

**Treinadores da árvore de decisão**

|Algoritmo|Propriedades|Treinadores|
|---------|----------|--------|
|Computador aprimorado com gradiente de luz|Mais rápido e mais preciso entre os treinadores da árvore de classificação binária. Altamente ajustável|<xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmMulticlassTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRegressionTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRankingTrainer>|
|Árvore rápida|Use para dados de imagem destacados. Resiliente a dados desbalanceados. Altamente ajustável | <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRegressionTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeTweedieTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRankingTrainer>|
|Floresta rápida|Funciona bem para dados ruidosos|<xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastForestRegressionTrainer>|
|GAM (modelo generalizado aditivo)|Melhor para problemas que funcionam bem com algoritmos de árvore, mas em que a capacidade de explicação é uma prioridade|<xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.GamRegressionTrainer>|

## <a name="matrix-factorization"></a>Fatoração de matriz

|Propriedades|Treinadores|
|----------|--------|
|Melhor para dados categóricos esparsos com grandes conjuntos de dados|<xref:Microsoft.ML.Trainers.FieldAwareFactorizationMachineTrainer>|

## <a name="meta-algorithms"></a>Meta-algoritmos

Esses treinadores criam um instrutor multiclasse de um instrutor binário. Use com <xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer>, <xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer>, <xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer>, <xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer>.

|Algoritmo|Propriedades|Treinadores|
|---------|----------|--------|
|Um versus todos|Esse classificador multiclasse treina um classificador binário para cada classe, que distingue essa classe de todas as outras. É limitado em escala pelo número de classes para categorizar|[OneVersusAllTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.OneVersusAllTrainer) |
|Acoplamento por pares|Esse classificador multiclasse treina um algoritmo de classificação binária em cada par de classes. É limitado em escala pelo número de classes, uma vez que cada combinação de duas classes deve ser treinada.|[PairwiseCouplingTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.PairwiseCouplingTrainer)|

## <a name="k-means"></a>K-Means

|Propriedades|Treinadores|
|----------|--------|
|Use para clustering|<xref:Microsoft.ML.Trainers.KMeansTrainer>|

## <a name="principal-component-analysis"></a>Análise de componente principal

|Propriedades|Treinadores|
|----------|--------|
|Use para detecção de anomalias|<xref:Microsoft.ML.Trainers.RandomizedPcaTrainer>|

## <a name="naive-bayes"></a>Naive Bayes

|Propriedades|Treinadores|
|----------|--------|
|Use este treinador de classificação multiclasse quando os recursos são independentes e o conjunto de dados de treinamento é pequeno.|<xref:Microsoft.ML.Trainers.NaiveBayesMulticlassTrainer>|

## <a name="prior-trainer"></a>Treinador anterior

|Propriedades|Treinadores|
|----------|--------|
|Use esse treinador de classificação binária para definir a linha de base de desempenho de outros treinadores. Para ser eficaz, as métricas dos outros treinadores devem ser melhores do que a do treinador anterior. |<xref:Microsoft.ML.Trainers.PriorTrainer>|
