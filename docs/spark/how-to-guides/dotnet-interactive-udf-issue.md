---
title: Escreva e chame UDFs no .NET para Apache Spark ambientes interativos.
description: Saiba como escrever e chamar UDFs no .NET para Apache Spark shells interativos.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 8fb729a0b8220d15af641f916383bbd6146e2e33
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94441070"
---
# <a name="write-and-call-udfs-in-net-for-apache-spark-interactive-environments"></a>Escreva e chame UDFs no .NET para Apache Spark ambientes interativos

Neste artigo, você aprenderá a usar as UDFs (funções definidas pelo usuário) em um ambiente do .NET para Apache Spark interativo.

## <a name="prerequisites"></a>Pré-requisitos

1. Instalar o [.net Interactive](https://github.com/dotnet/interactive)
2. Instalar o [Jupyter Lab](https://jupyter.org/)

## <a name="net-for-apache-spark-interactive-experience"></a>.NET para Apache Spark experiência interativa

O [.net para Apache Spark](https://github.com/dotnet/spark) usa o [.net Interactive](https://devblogs.microsoft.com/dotnet/net-interactive-is-here-net-notebooks-preview-2/) para fornecer suporte ao .net para experiência interativa no Spark. Para entender como configurar o ambiente para experimentar o .NET Interactive com notebooks Jupyter, consulte o [repositório interativo do .net](https://github.com/dotnet/interactive).

Além disso, é recomendável seguir [Este artigo sobre a SERIALIZAÇÃO UDF no .net para Apache Spark](udf-guide.md) entender quais UDFs são e como elas são serializadas no .net para Apache Spark.
Este guia usa blocos de anotações do Jupyter para ilustrar como usar UDFs em uma experiência interativa.

## <a name="define-a-udf-in-net-interactive"></a>Definir um UDF no .NET Interactive

Na experiência interativa, uma célula pode ser considerada como o trecho de código que está sendo enviado como parte de uma iteração do [repl](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop). Por exemplo, veja o bloco de anotações a seguir para entender o que isso significa:

![Jupyter Notebook células](./media/dotnet-interactive/dotnet-interactive-cells.png)

Cada um desses blocos marcados pela seta vermelha é uma célula ou um envio de código para Spark. Agora, ao definir um UDF que faz referência a um objeto personalizado definido pelo usuário, é necessário que o UDF seja definido na mesma célula em que o objeto ao qual ele faz referência é definido. Vejamos o que parece ser um exemplo:

![UDF de trabalho](./media/dotnet-interactive/working-udf.png)

## <a name="call-a-udf-on-a-dataframe"></a>Chamar um UDF em um dataframe

Ao chamar um UDF previamente definido em um, `DataFrame` é importante verificar se o UDF está definido em uma célula enviada anteriormente, antes de chamá-lo, como pode ser visto no exemplo anterior.

Agora, vamos ver o que acontece se chamarmos o UDF na mesma célula onde ele está definido.

![falha na chamada UDF](./media/dotnet-interactive/udf_fails.png)

O erro realçado acima é porque os assemblies UDF precisam primeiro ser compilados e enviados para os trabalhadores antes que possam ser chamados em um dataframe.

Essas são algumas coisas importantes para se ter em mente ao implementar UDFs no .NET para Apache Spark experiência interativa (como [notebooks Synapse do Azure](/azure/synapse-analytics/spark/apache-spark-development-using-notebooks)).

## <a name="faqs"></a>Perguntas frequentes

1. **Por que meu UDF que faz referência a um objeto personalizado definido pelo usuário gera o erro `Type Submission#_ is not marked as serializable` ?**
    O .NET Interactive encapsula cada uma dessas células com uma classe wrapper do número de envio da célula para identificar exclusivamente cada célula que está sendo enviada. Agora, conforme explicado em detalhes neste [guia](udf-guide.md), quando um UDF que faz referência a um objeto personalizado está sendo serializado, seu destino também é selecionado para serialização, que, no caso do .net Interactive, é encapsulado pela classe wrapper da célula onde o objeto personalizado é definido.
    Agora vamos ver como isso afeta nossa definição de UDF no bloco de anotações:

    ![Erro de serialização UDF](./media/dotnet-interactive/udf-serialization-error.png)

    Como pode ser visto no caso do `udf2_fails` , vemos a mensagem de erro dizendo que o tipo `Submission#7` não está marcado como serializável, isso ocorre porque o .net Interactive encapsula cada objeto definido em uma célula com sua `Submission#` classe, que é gerada imediatamente e, portanto, não é marcada como `Serializable` .

    Por esse motivo, é **necessário que um UDF referenciando um objeto personalizado seja definido na mesma célula que o objeto**.

2. **Por que não difundir variáveis funcionam com o .NET interativo?**
    Pelos motivos explicados anteriormente, as variáveis de difusão não funcionam com o .NET Interactive. É uma boa ideia seguir [este guia sobre variáveis de difusão](broadcast-guide.md) para obter uma compreensão mais profunda de quais variáveis de difusão são e como usá-las. O motivo pelo qual as variáveis de difusão não funcionam com cenários interativos é devido ao design interativo do .NET de acrescentar cada objeto definido em uma célula com sua classe de envio de célula, que, como não está marcada como serializável, falha com a mesma exceção que foi mostrado anteriormente.
    Vamos nos aprofundar um pouco mais com o exemplo a seguir:

    ![Falha nas variáveis de difusão](./media/dotnet-interactive/broadcast-fails.png)

    Conforme recomendado nas seções anteriores, definimos o UDF e o objeto que ele está referenciando (variável de difusão, nesse caso) na mesma célula, mas ainda vemos o erro reclamando `SerializationException` `Microsoft.Spark.Sql.Session` não estar marcado como serializável. Isso ocorre porque, quando o compilador tenta serializar o objeto de variável de difusão `bv` , ele encontra seu nome a ser anexado ao [`SparkSession`](https://github.com/dotnet/spark/blob/master/src/csharp/Microsoft.Spark/Sql/SparkSession.cs#L20) objeto `spark` , o que exige que seja marcado como serializável. Isso pode ser demonstrado com mais facilidade fazendo uma inspeção no assembly descompilado deste envio de célula:

    ![Código de assembly descompilado](./media/dotnet-interactive/decompiledAssembly.png)

    Se marcarmos a [`SparkSession`](https://github.com/dotnet/spark/blob/master/src/csharp/Microsoft.Spark/Sql/SparkSession.cs#L20) classe como `[Serializable]` , podemos fazer com que isso funcione, mas essa não é uma solução ideal, pois não queremos dar ao usuário a capacidade de serializar um objeto SparkSession, pois isso poderia levar a um comportamento estranho e indesejável. Esse é um [problema conhecido](https://github.com/dotnet/spark/issues/619) e será resolvido em versões futuras.
