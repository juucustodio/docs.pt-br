---
title: Operadores de consulta padrão de cadeia juntos (C#)-LINQ to XML
description: Saiba como encadear operadores de consulta juntos.
ms.date: 07/20/2015
dev_langs:
- csharp
ms.assetid: 66f2b0a9-2c23-4735-988e-bbc9dfb55c7b
ms.openlocfilehash: ed3ca44c853ebbeee690cb31232a13e35b383d1b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551847"
---
# <a name="chain-standard-query-operators-together-c-linq-to-xml"></a>Operadores de consulta padrão de cadeia juntos (C#) (LINQ to XML)

Os operadores de consulta padrão podem ser encadeados juntos. Por exemplo, você pode levantar o <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType> operador (chamado pela `where` cláusula) e funciona de maneira lenta; ou seja, nenhum resultado intermediário é materializado por ele.

## <a name="example-interject-a-where-clause"></a>Exemplo: levantar uma cláusula WHERE

Nesse exemplo, o método de <xref:System.Linq.Enumerable.Where%2A> é chamado antes de chamar `ConvertCollectionToUpperCase`. O método de <xref:System.Linq.Enumerable.Where%2A> opera quase exatamente a mesma maneira que os métodos lentos usados em exemplos anteriores neste tutorial, `ConvertCollectionToUpperCase` e `AppendString`.

Uma diferença é que, nesse caso, o <xref:System.Linq.Enumerable.Where%2A> método itera por meio de sua coleção de origem, determina que o primeiro item não passa o predicado e, em seguida, obtém o próximo item, que passa. Produz no segundo item.

No entanto, a ideia básica é a mesma: as coleções intermediárias não são materializadas, a menos que tenham que ser.

Quando expressões de consulta são usadas, elas são convertidas em chamadas para os operadores de consulta padrão e os mesmos princípios se aplicam.

Todos os exemplos nesta seção que estão vendo documentos do Office Open XML usam o mesmo princípio. A execução retardada e a avaliação lenta são alguns dos conceitos fundamentais que você deve entender para usar o LINQ e LINQ to XML, com eficiência.

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
            where s.CompareTo("D") >= 0
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
AppendString: source >DEF<
Main: str >DEF!!!<

ToUpper: source >ghi<
AppendString: source >GHI<
Main: str >GHI!!!<
```

Este é o artigo final do tutorial [: encadeamento de consultas em conjunto (C#)](chain-queries-example.md) .
