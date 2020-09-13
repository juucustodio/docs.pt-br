---
title: Refatorar em funções puras – LINQ to XML
description: Saiba mais sobre as funções puras e como usá-las para refatorar o código.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 2944a0d4-fd33-4e2e-badd-abb0f9be2fcc
ms.openlocfilehash: 18418a1fc39bee9f08cbe92d42c842e3fc9e148a
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552305"
---
# <a name="refactor-into-pure-functions-linq-to-xml"></a>Refatorar em funções puras (LINQ to XML)

Um aspecto importante de transformações e puras é aprender como o código do refatorar usando funções puras.

> [!NOTE]
> A nomenclatura comuns em programação funcional é que você refatora programa usando funções puras. No Visual Basic e C++, isso alinha com o uso das funções em linguagens respectivos. No entanto, em C#, as funções são chamadas métodos. Para fins desta discussão, uma função pura é implementada como um método em C#.

Conforme observado anteriormente nesta seção, uma função pura tem duas características úteis:

- Não tem efeito colateral. A função não altera nenhuma variável ou os dados de qualquer tipo fora da função.
- É consistente. Dado o mesmo conjunto de dados de entrada, sempre retornará o mesmo valor de saída.

Uma maneira de fazer a transição para programação funcional é o código existente do refatorar para eliminar efeitos colaterais desnecessários e dependências externas. Dessa maneira, você pode criar versões puras de função do código existente.

Este artigo discute o que é uma função pura e o que não é. O tutorial [: manipular conteúdo em um documento do WordprocessingML](xml-shape-wordprocessingml-documents.md) mostra como manipular um documento do WordprocessingML e inclui dois exemplos de como refatorar usando uma função pura.

Os seguintes exemplos contrastam duas funções não puras e uma função pura.

## <a name="example-implement-a-non-pure-function-that-changes-a-static-class-member"></a>Exemplo: implementar uma função não pura que altera um membro de classe estática

No código a seguir, a `HyphenatedConcat` função não é uma função pura, pois modifica o `aMember` membro de classe estática:

```csharp
public class Program
{
    private static string aMember = "StringOne";

    public static void HyphenatedConcat(string appendStr)
    {
        aMember += '-' + appendStr;
    }

    public static void Main()
    {
        HyphenatedConcat("StringTwo");
        Console.WriteLine(aMember);
    }
}
```

```vb
Module Module1
    Dim aMember As String = "StringOne"

    Public Sub HyphenatedConcat(ByVal appendStr As String)
        aMember = aMember & "-" & appendStr
    End Sub

    Sub Main()
        HyphenatedConcat("StringTwo")
        Console.WriteLine(aMember)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
StringOne-StringTwo
```

Observe que é irrelevante se os dados que estão sendo modificados têm `public` ou têm `private` acesso ou é membro `static` , `shared` membro ou membro de instância. Uma função pura não altera nenhum dado fora da função.

## <a name="example-implement-a-non-pure-function-that-changes-a-parameter"></a>Exemplo: implementar uma função não pura que altera um parâmetro

Além disso, a seguinte versão da mesma função não é pura porque modifica o conteúdo de seu parâmetro, `sb` .

```csharp
public class Program
{
    public static void HyphenatedConcat(StringBuilder sb, String appendStr)
    {
        sb.Append('-' + appendStr);
    }

    public static void Main()
    {
        StringBuilder sb1 = new StringBuilder("StringOne");
        HyphenatedConcat(sb1, "StringTwo");
        Console.WriteLine(sb1);
    }
}
```

```vb
Module Module1
    Public Sub HyphenatedConcat(ByVal sb As StringBuilder, ByVal appendStr As String)
        sb.Append("-" & appendStr)
    End Sub

    Sub Main()
        Dim sb1 As StringBuilder = New StringBuilder("StringOne")
        HyphenatedConcat(sb1, "StringTwo")
        Console.WriteLine(sb1)
    End Sub
End Module
```

Esta versão do programa gerenciar as mesmas saída que a primeira versão, porque a função de `HyphenatedConcat` alterou o valor (estado) do primeiro parâmetro chamar a função de membro de <xref:System.Text.StringBuilder.Append%2A> . Observe que essa alteração ocorre apesar do fato que `HyphenatedConcat` usa passagem de parâmetro de chamada por valor.

> [!IMPORTANT]
> Para tipos de referência, se você passa um parâmetro por valor, ele resulta em uma cópia de referência a um objeto que está sendo passado. Esta cópia ainda está associada com os mesmos dados de instância que a referência original (até que a variável de referência é atribuído a um novo objeto). A chamada por referência não é necessariamente necessária para uma função modificar um parâmetro.

## <a name="example-implement-a-pure-function"></a>Exemplo: implementar uma função pura

Esta próxima versão do programa mostra como implementar a função `HyphenatedConcat` como uma função pura.

```csharp
class Program
{
    public static string HyphenatedConcat(string s, string appendStr)
    {
        return (s + '-' + appendStr);
    }

    public static void Main(string[] args)
    {
        string s1 = "StringOne";
        string s2 = HyphenatedConcat(s1, "StringTwo");
        Console.WriteLine(s2);
    }
}
```

```vb
Module Module1
    Public Function HyphenatedConcat(ByVal s As String, ByVal appendStr As String) As String
        Return (s & "-" & appendStr)
    End Function

    Sub Main()
        Dim s1 As String = "StringOne"
        Dim s2 As String = HyphenatedConcat(s1, "StringTwo")
        Console.WriteLine(s2)
    End Sub
End Module
```

Além disso, esta versão gerencia a mesma linha de saída: `StringOne-StringTwo`. Observe que para manter o valor concatenado, ele é armazenado na variável intermediária `s2` .

Uma abordagem que pode ser muito útil é escrever as funções que são localmente impuros (isto é, declare e alteram variáveis locais) mas é global pura. Tais funções têm muitas das características desejáveis de composability, mas impedem alguns de linguagem e mais complicados de programação, como ter que usar a recursão quando um loop simples realizaria a mesma coisa.

## <a name="standard-query-operators"></a>Operadores de consulta padrão

Uma característica importante dos operadores de consulta padrão é que eles são implementados como funções puras.

Para obter mais informações, consulte Visão geral [dos operadores de consulta padrão (C#)](../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md) e [visão geral dos operadores de consulta padrão (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).

## <a name="see-also"></a>Confira também

- [Introdução às transformações funcionais puras](introduction-pure-functional-transformations.md)
- [Programação funcional versus programação imperativa](functional-vs-imperative-programming.md)
