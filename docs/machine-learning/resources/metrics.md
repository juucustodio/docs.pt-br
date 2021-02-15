---
title: Métricas do ML.NET
description: Entenda as métricas que são usadas para avaliar o desempenho de um modelo do ML.NET
ms.date: 12/17/2019
ms.openlocfilehash: 046e0a3feea2da702dfef5ca9ce4f498fce5fb26
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91804816"
---
# <a name="evaluate-your-mlnet-model-with-metrics"></a>Avaliar seu modelo ML.NET com métricas

Entenda as métricas usadas para avaliar um modelo ML.NET.

As métricas de avaliação são específicas para o tipo de tarefa de aprendizado de máquina que um modelo executa.

Por exemplo, para a tarefa de classificação, o modelo é avaliado medindo o quão bem uma categoria prevista corresponde à categoria real. E para o clustering, a avaliação é baseada em como os itens clusterizados são fechados e a quantidade de separação entre os clusters.

## <a name="evaluation-metrics-for-binary-classification"></a>Métricas de avaliação para classificação binária

| Métricas   |      Descrição      |  Procurar |
|-----------|-----------------------|-----------|
| **Precisão** |  [Precisão](https://en.wikipedia.org/wiki/Accuracy_and_precision#In_binary_classification) é a proporção de previsões corretas com um conjunto de dados de teste. É a taxa do número de previsões corretas para o número total de amostras de entrada. Ele funciona bem se houver um número semelhante de amostras que pertencem a cada classe.| **Quanto mais próximo de 1,00, melhor**. Mas exatamente 1,00 indica um problema (geralmente: vazamento de rótulo/destino, ajuste excessivo ou teste com os dados de treinamento). Quando os dados de teste são desequilibrados (em que a maioria das instâncias pertencem a uma das classes), o conjunto é pequeno ou a abordagem de pontuações 0, 0 ou 1, 0, a precisão não captura realmente a eficácia de um classificador e você precisa verificar métricas adicionais. |
| **AUC** |    [aucROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) ou *Area sob a curva* mede a área sob a curva criada examinando a taxa real positiva versus a taxa de falsos positivos.  |   **Quanto mais próximo de 1,00, melhor**. Deve ser maior que 0,50 para que um modelo seja aceitável. Um modelo com AUC de 0,50 ou menos é inúteis. |
| **AUCPR** | aucPR ou *área sob a curva de uma curva de Precision-Recall*: medida útil do sucesso da previsão quando as classes são desbalanceadas (conjuntos de valores altamente distorcidos). |  **Quanto mais próximo de 1,00, melhor**. Pontuações elevadas próximas de 1,00 mostram que o classificador retorna resultados precisos (precisão alta), além de retornar uma maioria de todos os resultados positivos (recall alto). |
| **Pontuação F1** | A [pontuação F1](https://en.wikipedia.org/wiki/F1_score), também conhecida como *pontuação F balanceada ou medida F*. É a média harmônica da precisão e do recall. A pontuação F1 é útil quando você deseja buscar um equilíbrio entre a precisão e o recall.| **Quanto mais próximo de 1,00, melhor**.  Uma pontuação F1 atinge seu melhor valor em 1,00 e o pior em 0,00. Ela informa o nível de precisão do classificador. |

Para obter mais detalhes sobre as métricas de classificação binária, leia os artigos a seguir:

- [Precisão, precisão, Recall ou F1?](https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9)
- [Classe de métricas de classificação binária](xref:Microsoft.ML.Data.BinaryClassificationMetrics)
- [A relação entre a recall de precisão e curvas ROC](http://pages.cs.wisc.edu/~jdavis/davisgoadrichcamera2.pdf)

## <a name="evaluation-metrics-for-multi-class-classification"></a>Métricas de avaliação para classificação de várias classes

| Métricas   |      Descrição      |  Procurar |
|-----------|-----------------------|-----------|
| **Microprecisão** |  A [precisão de micromédia](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.MicroAccuracy) agrega as contribuições de todas as classes para computar a métrica média. Ela é a fração de instâncias previstas corretamente. A micromédia não leva membros da classe em consideração. Basicamente, cada par de classe de exemplo contribui igualmente para a métrica de precisão. | **Quanto mais próximo de 1,00, melhor**. Em uma tarefa de classificação multiclasse, a microprecisão será preferível à macroprecisão se você suspeitar que há desequilíbrio de classe (ou seja, você pode ter muitos outros exemplos de uma classe do que de outras classes).|
| **Macroprecisão** | A [precisão de macromédia](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.MacroAccuracy) é a precisão média no nível de classe. A precisão para cada classe é calculada e a macroprecisão é a média desses precisões. Basicamente, cada classe contribui igualmente para a métrica de precisão. Classes minoritárias recebem o mesmo peso que as classes maiores. A métrica de macromédia fornece o mesmo peso a cada classe, não importa quantas instâncias dessa classe o conjunto de dados contém. |  **Quanto mais próximo de 1,00, melhor**.  Ele calcula a métrica de forma independente para cada classe e, em seguida, usa a média (tratando assim todas as classes igualmente) |
| **Perda de log**| A perda logarítmica mede o desempenho de um modelo de classificação em que a entrada de previsão é um valor de probabilidade entre 0,00 e 1,00. A perda logarítmica aumenta à medida que a probabilidade prevista diverge do rótulo real. | **Quanto mais próximo de 0,00, melhor**. Um modelo perfeito teria uma perda logarítmica de 0,00. A meta dos nossos modelos de machine learning é minimizar esse valor.|
| **Redução de perda logarítmica** | A [redução de perda logarítmica](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.LogLossReduction) pode ser interpretada como a vantagem do classificador sobre uma previsão aleatória.| **Varia de -inf a 1,00, em que 1,00 é uma previsão perfeita e 0,00 indica previsões péssimas**. Por exemplo, se o valor for igual a 0,20, ele poderá ser interpretado como "a probabilidade de uma previsão correta é 20% melhor do que a previsão aleatória"|

A microprecisão geralmente se alinha melhor com as necessidades de negócios de previsões de ML. Se você desejar selecionar uma única métrica para escolher a qualidade de uma tarefa de classificação multiclasse, geralmente ela deverá ser microprecisão.

Exemplo de uma tarefa de classificação do tíquete de suporte: (mapeia tíquetes de entrada para equipes de suporte)

- Microprecisão – com que frequência um tíquete de entrada é classificado para a equipe certa?
- Macroprecisão – para uma equipe de média, com que frequência um tíquete de entrada é correto para sua equipe?

A precisão de macros se espesa em pequenas equipes neste exemplo; uma equipe pequena que obtém apenas 10 tíquetes por ano, tanto quanto uma equipe grande com 10.000 tíquetes por ano. Nesse caso, a microprecisão se correlaciona melhor com a necessidade de negócios de "a quantidade de tempo e dinheiro que a empresa pode salvar automatizando meu processo de roteamento de tíquetes".

Para obter mais detalhes sobre métricas de classificação multiclasse, leia os artigos a seguir:

- [Micro e macro-média de precisão, recuperação e pontuação de F](https://rushdishams.blogspot.com/2011/08/micro-and-macro-average-of-precision.html)
- [Classificação multiclasse com conjunto de dados em desequilíbrio](https://towardsdatascience.com/machine-learning-multiclass-classification-with-imbalanced-data-set-29f6a177c1a)

## <a name="evaluation-metrics-for-regression-and-recommendation"></a>Métricas de avaliação para regressão e recomendação

As tarefas de regressão e de recomendação preveem um número. No caso de regressão, o número pode ser qualquer propriedade de saída influenciada pelas propriedades de entrada. Para recomendação, o número geralmente é um valor de classificação (entre 1 e 5, por exemplo) ou uma recomendação Sim/não (representada por 1 e 0, respectivamente).

| Metric   |      Descrição      |  Procurar |
|----------|-----------------------|-----------|
| **R quadrado** |  O [R2 (R quadrado)](https://en.wikipedia.org/wiki/Coefficient_of_determination) ou *coeficiente de determinação* representa a capacidade de previsão do modelo como um valor entre -inf e 1,00. 1,00 significa que há um ajuste perfeito e o ajuste pode ser arbitrariamente ruim. Portanto, as pontuações podem ser negativas. Uma pontuação de 0,00 significa quo modelo está adivinhando o valor esperado para o rótulo. R2 mede o quão próximos os valores de dados de teste reais são dos valores previstos. | **Quanto mais próximo de 1,00, melhor a qualidade**. No entanto, às vezes, valores de R quadrado baixos (por exemplo, 0,50) podem ser totalmente normais suficientemente bons para seu cenário, enquanto valores de R quadrado altos nem sempre são bons. Convém sempre suspeitar. |
| **Perda absoluta** |  A [perda absoluta](https://en.wikipedia.org/wiki/Mean_absolute_error) ou *MAE (erro de média absoluta)* mede o quão próximas as previsões são dos resultados reais. É a média de todos os erros do modelo, em que o erro do modelo é a distância absoluta entre o valor de rótulo previsto e o valor de rótulo correto. Esse erro de previsão é calculado para cada registro do conjunto de dados de teste. Por fim, o valor médio é calculado para todos os erros absolutos gravados.| **Quanto mais próximo de 0,00, melhor a qualidade.** O erro de média absoluta usa a mesma escala que os dados que estão sendo medidos (não é normalizado para um intervalo específico). Perda absoluta, perda quadrática e perda de RMS somente podem ser usadas para fazer comparações entre modelos para o mesmo conjunto de dados ou com um conjunto de dados com uma distribuição de valor de rótulo similar. |
| **Perda de quadrado** |  A [perda quadrada](https://en.wikipedia.org/wiki/Mean_squared_error) ou o *MSE (erro de quadrado médio)*, também chamado de *desvio quadrado médio (MSD)*, informa como fechar uma linha de regressão é para um conjunto de valores de dados de teste, levando as distâncias dos pontos para a linha de regressão (essas distâncias são os erros e) e elevando-as. Elevar ao quadrado dá mais peso para diferenças maiores. | É sempre positivo, e **valores mais próximos de 0,00 são melhores**. Dependendo de seus dados, pode ser impossível obter um valor muito pequeno para o erro médio quadrático.|
| **Perda de RMS** |  [RMS-perda](https://en.wikipedia.org/wiki/Root-mean-square_deviation) ou *erro de quadrado médio de raiz (RMSE)* (também chamado de *desvio quadrado de raiz média, RMSD*), mede a diferença entre os valores previstos por um modelo e os valores observados do ambiente que está sendo modelado. A perda de RMS é a raiz quadrada da perda quadrática e tem as mesmas unidades que o rótulo, de modo semelhante à perda absoluta, mas dando mais peso para diferenças maiores. A raiz do erro médio quadrático normalmente é usada em climatologia, previsão e análise de regressão para verificar resultados experimentais. | É sempre positivo, e **valores mais próximos de 0,00 são melhores**. RMSD é uma medida de precisão, para comparar os erros de previsão de modelos diferentes para um conjunto de dados específico e não entre conjuntos de dados, já que ela é dependente de escala.|

Para obter mais detalhes sobre as métricas de regressão, leia os artigos a seguir:

- [Análise de regressão: Como faço para interpretar o R-quadrado e avaliar a imescolha de adequação?](https://blog.minitab.com/blog/adventures-in-statistics-2/regression-analysis-how-do-i-interpret-r-squared-and-assess-the-goodness-of-fit)
- [Como interpretar R quadrado na análise de regressão](https://statisticsbyjim.com/regression/interpret-r-squared-regression)
- [Definição de R quadrado](https://www.investopedia.com/terms/r/r-squared.asp)
- [Definição de erro médio quadrático](https://www.statisticshowto.datasciencecentral.com/mean-squared-error/)
- [O que são o erro médio quadrático e a raiz do erro médio quadrático?](https://www.vernier.com/til/1014/)

## <a name="evaluation-metrics-for-clustering"></a>Métricas de avaliação para clustering

| Metric   |      Descrição      |  Procurar |
|----------|-----------------------|-----------|
|**Distância média**|Média da distância entre os pontos de dados e o centro do seu cluster atribuído. A distância média é uma medida de proximidade dos pontos de dados para o cluster de centróides. É uma medida de quão ' rígida ' o cluster é.|Os valores mais próximos de **0** são melhores. Quanto mais próximo de zero for a distância média, mais clusterizado os dados serão. No entanto, observe que essa métrica diminuirá se o número de clusters for aumentado e, no caso extremo (em que cada ponto de dados distinto for seu próprio cluster), ele será igual a zero.
|**Davies índice Bouldin**|A taxa média de distâncias dentro do cluster para distâncias entre clusters. Quanto mais estreita for o cluster, e mais distantes os clusters forem, menor será o valor.|Os valores mais próximos de **0** são melhores. Os clusters que estão mais distantes e menos dispersos resultarão em uma pontuação melhor.|
|**Informações mútuas normalizadas**|Pode ser usado quando os dados de treinamento usados para treinar o modelo de clustering também vêm com rótulos de verdade de terra (ou seja, clustering supervisionado). A métrica de informações mútuas normalizadas mede se os pontos de dados semelhantes são atribuídos ao mesmo cluster e pontos de dados distintos são atribuídos a diferentes clusters. As informações mútuas normalizadas são um valor entre 0 e 1|Valores mais próximos de **1** são melhores|

## <a name="evaluation-metrics-for-ranking"></a>Métricas de avaliação para classificação

| Metric   |      Descrição      |  Procurar |
|----------|-----------------------|-----------|
|**Ganhos cumulativos com desconto**|O DCG (lucro cumulativo com desconto) é uma medida de qualidade de classificação. Ele é derivado de duas suposições. Um: itens altamente relevantes são mais úteis quando aparecem acima na ordem de classificação. Dois: a utilidade controla a relevância, quanto maior a relevância, mais útil é um item. O lucro cumulativo com desconto é calculado para uma determinada posição na ordem de classificação. Ele soma a importância da relevância dividida pelo logaritmo do índice de classificação até a posição de interesse. Ele é calculado usando $ \ sum_ {i = 0} ^ {p} \frac {rel_i} {\ log_ {e} {i + 1}} $ relevância as gradações são fornecidas a um algoritmo de treinamento de classificação como rótulos de verdade de terra. Um valor de DCG é fornecido para cada posição na tabela de classificação, portanto, o nome **obtém ganhos** cumulativos. |**Valores mais altos são melhores**|
|**Ganhos cumulativos descontados normalizados**|Normalizar DCG permite que a métrica seja comparada para listas de classificação de diferentes comprimentos|**Valores mais próximos de 1 são melhores**|

## <a name="evaluation-metrics-for-anomaly-detection"></a>Métricas de avaliação para detecção de anomalias

| Metric   |      Descrição      |  Procurar |
|----------|-----------------------|-----------|
|**Área sob curva ROC**|A área sob a curva operador de receptor mede o quão bem o modelo separa os pontos de dados anormais e usuais.|**Os valores mais próximos de 1 são melhores**. Somente valores maiores que 0,5 demonstram a eficácia do modelo. Os valores de 0,5 ou abaixo indicam que o modelo não é melhor que alocar aleatoriamente as entradas para categorias anormais e usuais|
|**Taxa de detecção em contagem de falsos positivos**|Taxa de detecção em falso positivo contagem é a taxa do número de anomalias identificadas corretamente para o número total de anomalias em um conjunto de teste, indexadas por cada falso positivo. Ou seja, há um valor para taxa de detecção na contagem de falsos positivos para cada item falso positivo.|**Os valores mais próximos de 1 são melhores**. Se não houver nenhum positivo falso, esse valor será 1|
