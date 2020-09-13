---
title: Exemplo de consultas de encadeamento (C#)-LINQ to XML
description: Saiba o que acontece quando você encadea duas consultas que usam a execução adiada e a avaliação lenta.
ms.date: 07/20/2015
ms.assetid: abbca162-d95e-43af-b92c-e46e6aa2540e
ms.openlocfilehash: c0bbab9061b98eda15523f8a8e64e997bde8b307
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552017"
---
# <a name="chain-queries-example-c-linq-to-xml"></a>Exemplo de consultas de encadeamento (C#) (LINQ to XML)

Este exemplo baseia-se no exemplo no [exemplo de execução adiada](deferred-execution-example.md) e mostra o que acontece quando você encadea duas consultas que usam a execução adiada e a avaliação lenta.

## <a name="example-add-a-second-extension-method-that-uses-yield-return-to-defer-execution"></a>Exemplo: adicionar um segundo método de extensão que o usa `yield return` para adiar a execução

Neste exemplo, outro método de extensão é introduzido, `AppendString` , que acrescenta uma cadeia de caracteres especificada em cada cadeia de caracteres na coleção de origem e, em seguida, produz a cadeia de caracteres alterada.

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
        foreach (string str in source)
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
AppendString: source >ABC<
Main: str >ABC!!!<

ToUpper: source >def<
AppendString: source >DEF<
Main: str >DEF!!!<

ToUpper: source >ghi<
AppendString: source >GHI<
Main: str >GHI!!!<
```

Nesse exemplo, você pode ver que cada método de extensão opera um de cada vez para cada item na coleção de origem.

O que deve ser claro desse exemplo é o mesmo que nós encadeemos juntos consultas que rendem coleções, qualquer coleção intermediária é materializada. Em vez disso, cada item é passado de um método lenta a seguir. Isso resulta em uma pegada muito menor de memória do que uma abordagem que recebe primeiro uma matriz de cadeias de caracteres, então cria uma segunda matriz de cadeias de caracteres que foram convertidos para maiúsculas, e criar finalmente uma terceira matriz de cadeias de caracteres onde cada cadeia de caracteres tem os pontos de exclamação acrescentados a ele.

O próximo artigo deste tutorial ilustra a materialização intermediária:

- [Materialização intermediária (C#)](intermediate-materialization.md)

## <a name="see-also"></a>Confira também

- [Execução retardada e avaliação lenta](deferred-execution-lazy-evaluation.md)
