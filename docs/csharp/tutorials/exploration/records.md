---
title: Usar tipos de registro-tutorial em C#
description: Saiba mais sobre como usar tipos de registro, criar hierarquias de registros e quando escolher registros em classes.
ms.date: 11/12/2020
ms.openlocfilehash: 8a2cb6966ab4f93432723fd6f82618efa86b26aa
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688580"
---
# <a name="create-record-types"></a>Criar tipos de registro

O C# 9 apresenta *registros*, um novo tipo de referência que você pode criar em vez de classes ou estruturas. Os registros são distintos das classes nos tipos de registro que usam *igualdade baseada em valor*. Duas variáveis de um tipo de registro são iguais se as definições de tipo de registro são idênticas e se para cada campo, os valores em ambos os registros são iguais. Duas variáveis de um tipo de classe são iguais se os objetos referenciados são o mesmo tipo de classe e as variáveis referem-se ao mesmo objeto. A igualdade baseada em valor implica em outros recursos que você provavelmente desejará em tipos de registro. O compilador gera muitos desses membros quando você declara um `record` em vez de um `class` .

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Decida se você deve declarar um `class` ou um `record` .
> - Declare tipos de registro e tipos de registro posicionais.
> - Substitua seus métodos por métodos gerados pelo compilador em registros.

## <a name="prerequisites"></a>Pré-requisitos

Você precisará configurar seu computador para executar o .NET 5 ou posterior, incluindo o compilador C# 9,0 ou posterior. O compilador C# 9,0 está disponível a partir do [Visual Studio 2019 versão 16,8](https://visualstudio.microsoft.com/vs) ou do [SDK do .NET 5,0](https://dotnet.microsoft.com/download).

## <a name="characteristics-of-records"></a>Características dos registros

Você define um *registro* declarando um tipo com a `record` palavra-chave, em vez da `class` `struct` palavra-chave ou. Um registro é um tipo de referência e segue a semântica de igualdade baseada em valor. Para impor a semântica de valor, o compilador gera vários métodos para o tipo de registro:

- Uma substituição de <xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> .
- Um `Equals` método virtual cujo parâmetro é o tipo de registro.
- Uma substituição de <xref:System.Object.GetHashCode?displayProperty=nameWithType> .
- Métodos para `operator ==` e `operator !=` .
- Implementações de tipos de registro <xref:System.IEquatable%601?displayProperty=nameWithType> .

Além disso, os registros fornecem uma substituição de <xref:System.Object.ToString?displayProperty=nameWithType> . O compilador sintetiza métodos para exibir registros usando <xref:System.Object.ToString?displayProperty=nameWithType> . Você irá explorar esses membros enquanto escreve o código para este tutorial. Registra `with` expressões de suporte para habilitar a mutação não destrutiva de registros.

Você também pode declarar *registros posicionais* usando uma sintaxe mais concisa. O compilador sintetiza mais métodos para você quando você declara registros posicionais:

- Um construtor primário cujos parâmetros correspondem aos parâmetros posicionais na declaração de registro.
- Propriedades públicas somente de inicialização para cada parâmetro de um construtor primário.
- Um `Deconstruct` método para extrair propriedades do registro.

## <a name="build-temperature-data"></a>Criar dados de temperatura

Os dados e as estatísticas estão entre os cenários em que você desejará usar registros. Para este tutorial, você criará um aplicativo que calcula os *dias de grau* para diferentes usos. Os *dias de grau* são uma medida de calor (ou falta de calor) durante um período de dias, semanas ou meses. Os dias de grau controlam e preveem o uso de energia. Mais mais quente dias significa mais ar condicionado e mais frios significa mais uso de Furnace. Os dias de grau ajudam a gerenciar populações de planta. Os dias de grau correlacionam-se ao crescimento da fábrica à medida que as estações mudam. Os dias de grau ajudam a acompanhar as migrações de animais para espécies que viajam para o clima de correspondência.

A fórmula é baseada na temperatura média em um determinado dia e em uma temperatura de linha de base. Para calcular os dias de grau ao longo do tempo, você precisará da temperatura alta e baixa por dia por um período de tempo. Vamos começar criando um novo aplicativo. Crie um novo aplicativo de console. Crie um novo tipo de registro em um novo arquivo chamado "DailyTemperature.cs":

:::code language="csharp" source="snippets/record-types/InterimSteps.cs" ID="DailyRecord":::

O código anterior define um *registro posicional*. Você criou um tipo de referência que contém duas propriedades: `HighTemp` e `LowTemp` . Essas propriedades são *apenas Propriedades de inicialização*, o que significa que elas podem ser definidas no construtor ou usando um inicializador de propriedade. O `DailyTemperature` tipo também tem um *Construtor principal* que tem dois parâmetros que correspondem às duas propriedades. Você usa o Construtor principal para inicializar um `DailyTemperature` registro:

:::code language="csharp" source="snippets/record-types/Program.cs" ID="DeclareData":::

Você pode adicionar suas próprias propriedades ou métodos a registros, incluindo registros posicionais. Você precisará calcular a temperatura média para cada dia. Você pode adicionar essa propriedade ao `DailyTemperature` registro:

:::code language="csharp" source="snippets/record-types/DailyTemperature.cs" ID="TemperatureRecord":::

Vamos garantir que você possa usar esses dados. Adicione o código a seguir ao método `Main`:

```csharp
foreach (var item in data)
    Console.WriteLine(item);
```

Execute o aplicativo e você verá uma saída parecida com a seguinte exibição (várias linhas removidas para o espaço):

```dotnetcli
DailyTemperature { HighTemp = 57, LowTemp = 30, Mean = 43.5 }
DailyTemperature { HighTemp = 60, LowTemp = 35, Mean = 47.5 }


DailyTemperature { HighTemp = 80, LowTemp = 60, Mean = 70 }
DailyTemperature { HighTemp = 85, LowTemp = 66, Mean = 75.5 }
```

O código anterior mostra a saída da substituição de `ToString` sintetizada pelo compilador. Se preferir um texto diferente, você poderá escrever sua própria versão do `ToString` . Isso impede que o compilador sintetizasse uma versão para você.

## <a name="compute-degree-days"></a>Dias de computação

Para calcular os dias de grau, você assume a diferença de uma temperatura de linha de base e a temperatura média em um determinado dia. Para medir o calor ao longo do tempo, descarte os dias em que a temperatura média está abaixo da linha de base. Para medir frio ao longo do tempo, descartar os dias em que a temperatura média está acima da linha de base. Por exemplo, os EUA usam 65F como a base para os dias de aquecimento e resfriamento. Essa é a temperatura onde não é necessário aquecimento ou resfriamento. Se um dia tiver uma temperatura média de 70F, esse dia será de 5 dias de resfriamento e 0 dias de aquecimento. Por outro lado, se a temperatura média for 55F, esse dia será de 10 dias de aquecimento e 0 dias de resfriamento.

Você pode expressar essas fórmulas como uma pequena hierarquia de tipos de registro: um tipo de dia de grau abstrato e dois tipos concretos para dias de aquecimento e dias de resfriamento. Esses tipos também podem ser registros posicionais. Eles usam uma temperatura de linha de base e uma sequência de registros de temperatura diária como argumentos para o construtor primário:

:::code language="csharp" source="snippets/record-types/InterimSteps.cs" ID="DegreeDaysRecords":::

O `DegreeDays` registro abstrato é a classe base compartilhada para os `HeatingDegreeDays` registros e `CoolingDegreeDays` . As declarações de Construtor primários nos registros derivados mostram como gerenciar a inicialização do registro base. O registro derivado declara parâmetros para todos os parâmetros no Construtor principal de registro de base. O registro base declara e inicializa essas propriedades. O registro derivado não os oculta, mas só cria e inicializa Propriedades para parâmetros que não são declarados em seu registro base. Neste exemplo, os registros derivados não adicionam novos parâmetros de Construtor primários. Teste seu código adicionando o seguinte código ao seu `Main` método:

:::code language="csharp" source="snippets/record-types/Program.cs" ID="HeatingAndCooling":::

Você obterá uma saída semelhante à mostrada a seguir:

```dotnetcli
HeatingDegreeDays { BaseTemperature = 65, TempRecords = record_types.DailyTemperature[], DegreeDays = 85 }
CoolingDegreeDays { BaseTemperature = 65, TempRecords = record_types.DailyTemperature[], DegreeDays = 71.5 }
```

## <a name="define-compiler-synthesized-methods"></a>Definir métodos sintetizados pelo compilador

Seu código calcula o número correto de dias de aquecimento e resfriamento durante esse período de tempo. Mas este exemplo mostra por que você pode querer substituir alguns dos métodos sintetizados por registros. Você pode declarar sua própria versão de qualquer um dos métodos sintetizados pelo compilador em um tipo de registro, exceto o método clone. O método clone tem um nome gerado pelo compilador e você não pode fornecer uma implementação diferente. Esses métodos sintetizados incluem um construtor de cópia, os membros da <xref:System.IEquatable%601?displayProperty=nameWithType> interface, os testes de igualdade e desigualdade e <xref:System.Object.GetHashCode> . Para essa finalidade, você resumirá `PrintMembers` . Você também pode declarar seu próprio `ToString` , mas `PrintMembers` fornece uma opção melhor para cenários de herança. Para fornecer sua própria versão de um método sintetizado, a assinatura deve corresponder ao método sintetizado.

O `TempRecords` elemento na saída do console não é útil. Ele exibe o tipo, mas nada mais. Você pode alterar esse comportamento fornecendo sua própria implementação do método sintetizado `PrintMembers` . A assinatura depende dos modificadores aplicados à `record` declaração:

- Se um tipo de registro for `sealed` , a assinatura será `private bool PrintMembers(StringBuilder builder);`
- Se um tipo de registro não for `sealed` e for derivado de `object` (ou seja, não declarar um registro base), a assinatura será `protected virtual bool PrintMembers(StringBuilder builder);`
- Se um tipo de registro não for `sealed` e for derivado de outro registro, a assinatura será `protected override bool PrintMembers(StringBuilder builder);`

Essas regras são mais fáceis de compreender ao entender a finalidade de `PrintMembers` . `PrintMembers` Adiciona informações sobre cada propriedade em um tipo de registro a uma cadeia de caracteres. O contrato requer registros base para adicionar seus membros à exibição e supõe que os membros derivados adicionarão seus membros. Cada tipo de registro sintetiza uma `ToString` substituição que é semelhante ao seguinte exemplo para `HeatingDegreeDays` :

```csharp
public override string ToString()
{
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.Append("HeatingDegreeDays");
    stringBuilder.Append(" { ");
    if (PrintMembers(stringBuilder))
    {
        stringBuilder.Append(" ");
    }
    stringBuilder.Append("}");
    return stringBuilder.ToString();
}
```

Você declara um `PrintMembers` método no `DegreeDays` registro que não imprime o tipo da coleção:

:::code language="csharp" source="snippets/record-types/DegreeDays.cs" ID="AddPrintMembers":::

A assinatura declara um `virtual protected` método para corresponder à versão do compilador. Não se preocupe se você obtiver os acessadores incorretos; a linguagem impõe a assinatura correta. Se você esquecer os modificadores corretos para qualquer método sintetizado, o compilador emitirá avisos ou erros que o ajudarão a obter a assinatura correta.

## <a name="non-destructive-mutation"></a>Mutação não destrutiva

Os membros sintetizados em um registro posicional não modificam o estado do registro. O objetivo é que você possa criar registros imutáveis mais facilmente. Examine novamente as declarações anteriores para `HeatingDegreeDays` e `CoolingDegreeDays` . Os membros adicionados executam cálculos nos valores para o registro, mas não modificam o estado. Os registros posicionais facilitam a criação de tipos de referência imutáveis.

A criação de tipos de referência imutáveis significa que você desejará usar mutação não destrutiva. Você cria novas instâncias de registro que são semelhantes às instâncias de registro existentes usando [ `with` expressões](../../language-reference/operators/with-expression.md). Essas expressões são uma construção de cópia com atribuições adicionais que modificam a cópia. O resultado é uma nova instância de registro em que cada propriedade foi copiada do registro existente e, opcionalmente, modificada. O registro original não foi alterado.

Vamos adicionar alguns recursos ao seu programa que demonstram `with` expressões. Primeiro, vamos criar um novo registro para calcular os dias de grau crescente usando os mesmos dados. Os *dias de grau crescente* normalmente usam 41F como a linha de base e mede temperaturas acima da linha de base. Para usar os mesmos dados, você pode criar um novo registro que seja semelhante ao `coolingDegreeDays` , mas com uma temperatura de base diferente:

:::code language="csharp" source="snippets/record-types/Program.cs" ID="GrowingDegreeDays":::

Você pode comparar o número de graus computados com os números gerados com uma temperatura de linha de base maior. Lembre-se de que os registros são *tipos de referência* e essas cópias são cópias superficiais. A matriz para os dados não é copiada, mas ambos os registros fazem referência aos mesmos dados. Esse fato é uma vantagem em um outro cenário. Para os dias de crescimento crescentes, é útil manter o controle do total dos 5 dias anteriores. Você pode criar novos registros com dados de origem diferentes usando `with` expressões. O código a seguir cria uma coleção dessas acumulações e, em seguida, exibe os valores:

:::code language="csharp" source="snippets/record-types/Program.cs" ID="RunningFiveDayTotal":::

Você também pode usar `with` expressões para criar cópias de registros. Não especifique nenhuma propriedade entre as chaves da `with` expressão. Isso significa criar uma cópia e não alterar nenhuma propriedade:

```csharp
var growingDegreeDaysCopy = growingDegreeDays with { };
```

Execute o aplicativo concluído para ver os resultados.

## <a name="summary"></a>Resumo

Este tutorial mostrou vários aspectos de registros. Os registros fornecem sintaxe concisa para tipos de referência em que o uso fundamental está armazenando dados. Para classes orientadas a objeto, o uso fundamental é definir responsabilidades. Este tutorial se concentrou em *registros posicionais*, onde você pode usar uma sintaxe concisa para declarar as propriedades somente de inicialização para um registro. O compilador sintetiza vários membros do registro para copiar e comparar registros. Você pode adicionar outros membros necessários para os tipos de registro. Você pode criar tipos de registro imutáveis sabendo que nenhum dos membros gerados pelo compilador mutaria o estado. Para registros posicionais, as expressões facilitam o `with` suporte à mutação não destrutiva.

Os registros adicionam outra maneira de definir tipos. Você usa `class` definições para criar hierarquias orientadas a objeto que se concentram nas responsabilidades e no comportamento dos objetos. Você cria `struct` tipos para estruturas de dados que armazenam dados e são pequenos o suficiente para copiar com eficiência. Você cria registros quando deseja igualdade e comparação com base em valor, não deseja copiar valores e deseja usar variáveis de referência.

Você pode aprender a descrição completa dos registros lendo a [especificação do tipo de registro proposto](~/_csharplang/proposals/csharp-9.0/records.md).
