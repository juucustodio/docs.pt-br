---
title: Trabalhar com namespaces globais em Visual Basic LINQ to XML
description: Você declara um namespace em Visual Basic com a instrução Imports, se o namespace é um namespace padrão ou tem um prefixo. Este artigo discute as instruções de importação e outros aspectos do trabalho com namespaces.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 0a8064d5-e02f-4315-ad48-6deaa443a2f0
ms.openlocfilehash: f05fcab6788388e36e2b68a2d4f022ea63e74280
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552321"
---
# <a name="work-with-global-namespaces-in-visual-basic-linq-to-xml"></a>Trabalhar com namespaces globais no Visual Basic (LINQ to XML)

Um dos principais recursos de literais XML no Visual Basic é a capacidade de declarar namespaces XML usando a `Imports` instrução. Usando esse recurso, você pode declarar um namespace XML que usa um prefixo, ou você pode declarar um namespace XML padrão.

Esse recurso é útil em duas situações:

- Os namespaces declarados em literais XML não são transferidos para expressões incorporadas. A declaração de namespaces globais reduz a quantidade de trabalho necessária para usar expressões inseridas com namespaces.
- Você deve declarar namespaces globais para usar namespaces com propriedades XML.

Você pode declarar namespaces globais no nível do projeto. Você também pode declarar namespaces globais em nível de módulo, que substitui namespaces globais no nível de projeto. Finalmente, você pode substituir namespaces globais em um literal XML.

Ao usar literais XML ou propriedades XML que estão em namespaces declarados globalmente, você pode ver o nome expandido de literais XML ou Propriedades passando o mouse sobre eles no Visual Studio. Você verá o nome expandido em uma dica de ferramenta.

Você pode obter um objeto de <xref:System.Xml.Linq.XNamespace> que corresponde a um namespace global usando o método `GetXmlNamespace` .

## <a name="example-use-imports-to-declare-a-global-namespace"></a>Exemplo: use `Imports` para declarar um namespace global

O exemplo a seguir declara um namespace global padrão com a `Imports` instrução e inicializa um <xref:System.Xml.Linq.XElement> objeto nesse namespace com um literal XML:

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <Root/>
        Console.WriteLine(root)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```xml
<Root xmlns="http://www.adventure-works.com" />
```

## <a name="example-declare-a-global-namespace-that-has-a-prefix"></a>Exemplo: declarar um namespace global que tem um prefixo

O exemplo a seguir declara um namespace global com um prefixo e inicializa um elemento com um literal XML:

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <aw:Root/>
        Console.WriteLine(root)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```xml
<aw:Root xmlns:aw="http://www.adventure-works.com" />
```

## <a name="example-declare-a-default-namespace-and-use-an-embedded-expression-for-the-child-element"></a>Exemplo: declare um namespace padrão e use uma expressão inserida para o `Child` elemento

Os namespaces que são declarados em literais XML não são transferidos para expressões incorporadas. O exemplo a seguir declara um namespace padrão e, em seguida, usa uma expressão inserida para o `Child` elemento.

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <%= <Child/> %>
    </Root>
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child xmlns="" />
</Root>
```

O XML resultante inclui uma declaração de um namespace padrão para que o `Child` elemento esteja em nenhum namespace.

Você pode declarar um namespace diferente na expressão inserida da seguinte maneira:

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <%= <Child xmlns="http://www.adventure-works.com"/> %>
    </Root>
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child xmlns="http://www.adventure-works.com" />
</Root>
```

No entanto, com o namespace global padrão, você pode usar literais XML sem declarar namespaces. O XML resultante estará no namespace padrão declarado globalmente, como neste exemplo:

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <Root>
                                   <%= <Child/> %>
                               </Root>
        Console.WriteLine(root)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```xml
<Root xmlns="http://www.adventure-works.com">
  <Child />
</Root>
```

## <a name="example-use-namespaces-with-xml-properties"></a>Exemplo: usar namespaces com propriedades XML

Se você estiver trabalhando com uma árvore XML que está em um namespace e usar as propriedades XML, deverá usar um namespace global para que as propriedades XML também estejam no namespace correto. O exemplo a seguir declara uma árvore XML em um namespace e, em seguida, imprime a contagem de `Child` elementos.

```vb
Dim root As XElement = _
    <Root xmlns="http://www.adventure-works.com">
        <Child>content</Child>
    </Root>
Console.WriteLine(root.<Child>.Count())
```

Este exemplo indica que não há nenhum elemento de `Child` . Ele produz esta saída:

```output
0
```

Se, no entanto, você declarar um namespace global padrão, então a literal XML e a propriedade XML estão no namespace global padrão:

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root>
                <Child>content</Child>
            </Root>
        Console.WriteLine(root.<Child>.Count())
    End Sub
End Module
```

Este exemplo indica que há um elemento de `Child` . Ele produz esta saída:

```output
1
```

Se você declarar um namespace global que tenha um prefixo, você pode usar o prefixo para literais XML e propriedades XML:

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <aw:Child>content</aw:Child>
            </aw:Root>
        Console.WriteLine(root.<aw:Child>.Count())
    End Sub
End Module
```

## <a name="example-use-getxmlnamespace-to-get-an-xnamespace"></a>Exemplo: use `GetXmlNamespace` para obter um `XNamespace`

Você pode obter um <xref:System.Xml.Linq.XNamespace> objeto usando o `GetXmlNamespace` método:

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <aw:Root/>
        Dim xn As XNamespace = GetXmlNamespace(aw)
        Console.WriteLine(xn)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
http://www.adventure-works.com
```

## <a name="see-also"></a>Confira também

- [Visão geral dos namespaces](namespaces-overview.md)
