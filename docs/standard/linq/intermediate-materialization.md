---
title: Materialização intermediária (C#)
description: Saiba como o uso de alguns operadores de consulta padrão pode causar a materialização de coleções em uma consulta e alterar drasticamente o perfil de memória e de desempenho do seu aplicativo.
ms.date: 07/20/2015
ms.assetid: 7922d38f-5044-41cf-8e17-7173d6553a5e
ms.openlocfilehash: 8dca4bb29886973762351049d06bcf5d3ba352db
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551866"
---
# <a name="intermediate-materialization-c"></a>Materialização intermediária (C#)

Se você não tiver cuidado, poderá, em algumas situações, alterar drasticamente o perfil de memória e desempenho do seu aplicativo, causando uma materialização prematura das coleções em suas consultas. Alguns operadores de consulta padrão faz com que o materialization de sua coleção de origem antes de produzir um único elemento. Por exemplo, <xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType> primeiro itera através da coleção inteira de origem, então classe todos os itens, e então produz basicamente o primeiro item. Isso significa que é caro obter o primeiro item de uma coleção ordenada; em seguida, cada item não é caro. Isso faz sentido: Seria impossível para esse operador de consulta de fazer outra maneira.

## <a name="example-add-a-method-that-calls-tolist-causing-materialization"></a>Exemplo: adicionar um método que chama `ToList` , causando materialização

Este exemplo altera o exemplo no [exemplo de consultas de cadeia (C#)](chain-queries-example.md): o `AppendString` método é alterado para chamar <xref:System.Linq.Enumerable.ToList%2A> antes de iterar pela origem, o que causa a materialização.

```csharp
public static class LocalExtensions
{
    public static IEnumerable<string>
      ConvertCollectionToUpperCase(this IEnumerable<string> source)
    {
        foreach (string str in source)
        {
            Console.WriteLine("ToUpper: source >{0}<", str);
            yield return str.ToUpper();
        }
    }

    public static IEnumerable<string>
      AppendString(this IEnumerable<string> source, string stringToAppend)
    {
        // the following statement materializes the source collection in a List<T>
        // before iterating through it
        foreach (string str in source.ToList())
        {
            Console.WriteLine("AppendString: source >{0}<", str);
            yield return str + stringToAppend;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        string[] stringArray = { "abc", "def", "ghi" };

        IEnumerable<string> q1 =
            from s in stringArray.ConvertCollectionToUpperCase()
            select s;

        IEnumerable<string> q2 =
            from s in q1.AppendString("!!!")
            select s;

        foreach (string str in q2)
        {
            Console.WriteLine("Main: str >{0}<", str);
            Console.WriteLine();
        }
    }
}
```

 Esse exemplo gera a saída a seguir:

```output
ToUpper: source >abc<
ToUpper: source >def<
ToUpper: source >ghi<
AppendString: source >ABC<
Main: str >ABC!!!<

AppendString: source >DEF<
Main: str >DEF!!!<

AppendString: source >GHI<
Main: str >GHI!!!<
```

Nesse exemplo, você pode ver que a chamada a <xref:System.Linq.Enumerable.ToList%2A> faz com que `AppendString` enumerar sua fonte inteiro antes de como o primeiro item. Se a origem foi uma matriz grande, essa alteraria significativamente o perfil de memória do aplicativo.

Os operadores de consulta padrão também podem ser encadeados, conforme mostrado no artigo final deste tutorial:

- [Operadores de consulta padrão de cadeia juntos (C#)](chain-standard-query-operators-together.md)

## <a name="see-also"></a>Confira também

- [Execução retardada e avaliação lenta](deferred-execution-lazy-evaluation.md)
