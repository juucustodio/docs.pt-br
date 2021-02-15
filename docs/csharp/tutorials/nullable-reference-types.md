---
title: Criar com tipos de referência que permitem valor nulo
description: Este tutorial avançado fornece uma introdução aos tipos de referência que permitem valor nulo. Você aprenderá a expressar sua intenção de design quando os valores de referência puderem ser nulos e ter o compilador obrigatório quando eles não puderem ser nulos.
ms.date: 02/19/2019
ms.technology: csharp-null-safety
ms.custom: mvc
ms.openlocfilehash: bd575b226a2ff61e938719b064ff5ede0cf66013
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805174"
---
# <a name="tutorial-express-your-design-intent-more-clearly-with-nullable-and-non-nullable-reference-types"></a>Tutorial: Expressar sua intenção de design mais claramente com tipos de referência que permitem valor nulo e tipos que não permitem valor nulo

O C# 8,0 apresenta [tipos de referência anuláveis](../nullable-references.md), que complementam os tipos de referência da mesma maneira que os tipos de valores de valor nulo complementam tipos Value Para declarar que uma variável é um **tipo de referência que permite valor nulo**, anexe um `?` ao tipo. Por exemplo, `string?` representa uma `string` que permite valor nulo. Você pode usar esses novos tipos para expressar mais claramente sua intenção de design: algumas variáveis * devem sempre ter um valor *, outras * podem ter um valor * ausente.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Incorporar tipos de referência que permitem valores nulos e tipos de referência que não permitem valores nulos aos designs
> - Habilitar verificações de tipo de referência que permitem valor nulo em todo o código.
> - Gravar código em locais onde o compilador imponha essas decisões de design.
> - Usar o recurso de referência que permite valor nulo em seus próprios designs

## <a name="prerequisites"></a>Pré-requisitos

Você precisará configurar seu computador para executar o .NET Core, incluindo o compilador C# 8,0. O compilador C# 8,0 está disponível com o [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)ou o [.NET Core 3,0](https://dotnet.microsoft.com/download/dotnet-core/3.0).

Este tutorial pressupõe que você esteja familiarizado com o C# e .NET, incluindo o Visual Studio ou a CLI do .NET Core.

## <a name="incorporate-nullable-reference-types-into-your-designs"></a>Incorporar tipos de referência que permitem valor nulo aos designs

Neste tutorial, você criará uma biblioteca para modelar a executar uma pesquisa. O código usa tipos de referência que permitem valores nulos e tipos de referência que não permitem valores nulos para representar os conceitos do mundo real. As perguntas da pesquisa nunca podem ser um valor nulo. Um entrevistado pode optar por não responder a uma pergunta. As respostas podem estar `null` nesse caso.

O código que você gravará para este exemplo expressa essa intenção e o compilador a aplica.

## <a name="create-the-application-and-enable-nullable-reference-types"></a>Criar o aplicativo e habilitar os tipos de referência que permitem valor nulo

Crie um novo aplicativo de console no Visual Studio ou na linha de comando usando `dotnet new console`. Dê o nome `NullableIntroduction` ao aplicativo. Depois de criar o aplicativo, você precisará especificar que todo o projeto será compilado em um **contexto de anotação anulável**habilitado. Abra o arquivo *. csproj* e adicione um `Nullable` elemento ao `PropertyGroup` elemento. Defina seu valor como `enable`. Você deve optar pelo recurso **tipos de referência anulável** , mesmo em projetos C# 8,0. Isso porque, quando o recurso é ativado, as declarações de variáveis de referência existentes tornam-se **tipos de referência que não permitem valor nulo**. Embora essa decisão ajude a encontrar problemas em que o código existente pode não ter verificações nulas adequadas, ele pode não refletir com precisão sua intenção de design original:

```xml
<Nullable>enable</Nullable>
```

### <a name="design-the-types-for-the-application"></a>Criar os tipos para o aplicativo

Este aplicativo de pesquisa requer a criação de várias classes:

- Uma classe que modela a lista de perguntas.
- Uma classe que modela uma lista de pessoas contatadas para a pesquisa.
- Uma classe que modela as respostas de uma pessoa que participou da pesquisa.

Esses tipos usarão os tipos de referência que permitem valor nulo e tipos de referência que não permitem valor nulo para expressar quais membros são obrigatórios e quais são opcionais. Os tipos de referência que permitem valor nulo informam claramente essa intenção de design:

- As perguntas que fazem parte da pesquisa nunca podem ser valores nulos: não faz sentido fazer uma pergunta vazia.
- Os entrevistados nunca poderão ser nulos. Convém controlar as pessoas contatadas, mesmo os entrevistados que se recusaram a participar.
- Qualquer resposta a uma pergunta pode ser um valor nulo. Os entrevistados podem se recusar a responder a algumas ou a todas as perguntas.

Se você tiver programado em C#, talvez esteja acostumado a se acostumar com tipos de referência que permitem que `null` os valores que você tenha perdido outras oportunidades declarem instâncias não anuláveis:

- O conjunto de perguntas não deve permitir um valor nulo.
- O conjunto de entrevistados não deve permitir um valor nulo.

Ao escrever o código, você verá que um tipo de referência não anulável como o padrão para referências evita erros comuns que poderiam levar a <xref:System.NullReferenceException> s. Uma lição deste tutorial é que você tomou decisões sobre quais variáveis poderiam ou não ser `null` . O idioma não forneceu sintaxe para expressar essas decisões. Agora ele já fornece.

O aplicativo que você criará faz as seguintes etapas:

1. Cria uma pesquisa e adiciona perguntas a ela.
1. Cria um conjunto pseudo aleatório de entrevistados para a pesquisa.
1. Os participantes do contato até que o tamanho da pesquisa concluída atinja o número da meta.
1. Grava estatísticas importantes nas respostas da pesquisa.

## <a name="build-the-survey-with-nullable-and-non-nullable-reference-types"></a>Criar a pesquisa com tipos de referência anuláveis e não anuláveis

O primeiro código gravado criará a pesquisa. Você escreverá classes para modelar uma pergunta da pesquisa e uma execução da pesquisa. A pesquisa tem três tipos de perguntas, diferenciadas pelo formato da resposta: respostas do tipo Sim/Não, respostas com números e respostas com texto. Criar uma `public SurveyQuestion` classe:

```csharp
namespace NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
```

O compilador interpreta cada declaração de variável de tipo de referência como um tipo de referência **não anulável** para o código em um contexto de anotação anulável habilitado. Para ver seu primeiro aviso, adicione propriedades ao texto da pergunta e tipo de pergunta, conforme mostrado no código a seguir:

```csharp
namespace NullableIntroduction
{
    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }

    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
```

Como você não inicializou `QuestionText`, o compilador emitirá um aviso informando que uma propriedade que não permite valor nulo não foi inicializada. Seu design exige que o texto da pergunta não seja um valor nulo, portanto, você inclui um construtor para inicializá-lo e o valor `QuestionType` também. A definição da classe concluída se parece com o código a seguir:

[!code-csharp[DefineQuestion](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyQuestion.cs)]

A adição do construtor removerá o aviso. O argumento do construtor também é um tipo de referência que não permite valor nulo, portanto, o compilador não emite avisos.

Em seguida, crie uma classe `public` chamada `SurveyRun`. Esta classe contém uma lista de métodos e objetos `SurveyQuestion` para adicionar perguntas à pesquisa, conforme mostrado no código a seguir:

```csharp
using System.Collections.Generic;

namespace NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new List<SurveyQuestion>();

        public void AddQuestion(QuestionType type, string question) =>
            AddQuestion(new SurveyQuestion(type, question));
        public void AddQuestion(SurveyQuestion surveyQuestion) => surveyQuestions.Add(surveyQuestion);
    }
}
```

Como foi feito anteriormente, você deve inicializar o objeto de lista com um valor não nulo ou o compilador emitirá um aviso. Não há verificações de valores nulos na segunda sobrecarga de `AddQuestion`, pois elas são desnecessárias: você declarou que a variável não permite valor nulo. Seu valor não pode ser `null`.

Alterne para *Program.cs* no seu editor e substitua o conteúdo de `Main` pelas seguintes linhas de código:

[!code-csharp[AddQuestions](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#AddQuestions)]

Como o projeto inteiro está em um contexto de anotação anulável habilitado, você receberá avisos quando passar `null` para qualquer método que espera um tipo de referência não anulável. Experimente adicionar a seguinte linha a `Main`:

```csharp
surveyRun.AddQuestion(QuestionType.Text, default);
```

## <a name="create-respondents-and-get-answers-to-the-survey"></a>Criar entrevistados e obter respostas para a pesquisa

Em seguida, grave o código que gerará respostas para a pesquisa. Esse processo envolve várias tarefas pequenas:

1. Criar um método para gerar objetos dos entrevistados. Eles representam pessoas solicitadas a preencher a pesquisa.
1. Criar lógica para simular a realização de perguntas para um pesquisado e coletar respostas ou perceber que um pesquisado não respondeu.
1. Repetir até que entrevistados suficientes tenham respondido à pesquisa.

Será necessária uma classe para representar uma resposta da pesquisa. Adicione-a agora. Habilitar o suporte para tipos que permitem valor nulo. Adicione uma propriedade `Id` e um construtor para inicializá-la, conforme mostrado no código a seguir:

```csharp
namespace NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }

        public SurveyResponse(int id) => Id = id;
    }
}
```

Em seguida, adicione um método `static` para criar novos participantes ao gerar uma ID aleatória:

[!code-csharp[GenerateRespondents](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#Random)]

A principal responsabilidade dessa classe é gerar as respostas de um participante para as perguntas da pesquisa. Essa responsabilidade conta com algumas etapas:

1. Peça para participar da pesquisa. Se a pessoa não consentir, retorne uma resposta de ausente (ou de valor nulo).
1. Faça as perguntas e registre a resposta. As respostas também pode ser ausentes (ou de valor nulo).

Adicione o seguinte código à classe `SurveyResponse`:

[!code-csharp[AnswerSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#AnswerSurvey)]

O armazenamento das respostas da pesquisa é um `Dictionary<int, string>?`, indicando que ele pode ser um valor nulo. Você está usando o novo recurso de idioma para declarar sua intenção de design, tanto para o compilador quanto para qualquer pessoa que leia seu código posteriormente. Se você já desreferenciar `surveyResponses` sem verificar o `null` valor primeiro, obterá um aviso do compilador. Você não receberá um aviso no método `AnswerSurvey` porque o compilador pode determinar que a variável `surveyResponses` foi definida como um valor não nulo acima.

O uso de `null` para respostas ausentes destaca um ponto importante para trabalhar com tipos de referência anuláveis: seu objetivo não é remover todos os valores `null` de seu programa. Em vez disso, sua meta é garantir que o código escrito expresse a intenção do seu design. Os valores ausentes representam um conceito que precisa ser expresso em seu código. O valor `null` é uma forma clara de expressar esses valores ausentes. Tentar remover todos os valores `null` leva somente à definição de alguma outra maneira de expressar esses valores ausentes sem `null`.

Em seguida, é necessário gravar o método `PerformSurvey` na classe `SurveyRun`. Adicione o seguinte código à classe `SurveyRun`:

[!code-csharp[PerformSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#PerformSurvey)]

Aqui, novamente, sua opção por uma `List<SurveyResponse>?` que permite valor nulo indica que a resposta pode ser um valor nulo. Isso indica que a pesquisa ainda não foi entregue a nenhum pesquisado. Observe que os entrevistados são adicionados até que um suficiente de pessoas tiver consentido.

A última etapa para executar a pesquisa é adicionar uma chamada para executar a pesquisa no final do método `Main`:

[!code-csharp[RunSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#RunSurvey)]

## <a name="examine-survey-responses"></a>Examinar as respostas da pesquisa

A última etapa é exibir os resultados da pesquisa. Você adicionará código a várias classes gravadas. Este código demonstra o valor da distinção dos tipos de referência que permitem valor nulo e tipos de referência que não permitem valor nulo. Comece adicionando os dois membros com corpo de expressão à classe `SurveyResponse`:

[!code-csharp[ReportResponses](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#SurveyStatus)]

Como `surveyResponses` é um tipo de referência anulável, verificações nulas são necessárias antes de fazer referência a ela. O `Answer` método retorna uma cadeia de caracteres não anulável, portanto, precisamos abordar o caso de uma resposta ausente usando o operador de União nula.

Em seguida, adicione esses três membros com corpo de expressão à classe `SurveyRun`:

[!code-csharp[ReportResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#RunReport)]

O membro `AllParticipants` deve levar em conta que a variável `respondents` pode ser um valor nulo, mas o valor de retorno não pode ser nulo. Se você alterar essa expressão removendo `??` e a sequência vazia que se segue, o compilador avisará que o método poderá retornar `null` e sua assinatura de retorno retornará um tipo que não permite valor nulo.

Por fim, adicione o seguinte loop à parte inferior do método `Main`:

[!code-csharp[DisplaySurveyResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#WriteAnswers)]

Você não precisa de verificações de `null` neste código porque criou as interfaces subjacentes para que todas elas retornem tipos de referência que não permitem valor nulo.

## <a name="get-the-code"></a>Obter o código

Obtenha o código do tutorial concluído em nosso repositório de [amostras](https://github.com/dotnet/samples) na pasta [csharp/NullableIntroduction](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction).

Experimente alterar as declarações de tipo entre os tipos de referência que permitem valor nulo e tipos de referência que não permitem valor nulo. Veja como isso gera avisos diferentes para garantir que um `null` não será acidentalmente cancelado.

## <a name="next-steps"></a>Próximas etapas

Saiba mais migrando um aplicativo existente para usar tipos de referência anuláveis:
> [!div class="nextstepaction"]
> [Atualizar um aplicativo a fim de usar tipos de referência anuláveis](upgrade-to-nullable-references.md)

Saiba como usar o tipo de referência anulável ao usar Entity Framework:
> [Conceitos básicos de Entity Framework Core: trabalhando com tipos de referência anuláveis](/ef/core/miscellaneous/nullable-reference-types)
