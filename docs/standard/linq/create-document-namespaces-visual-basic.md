---
title: Como criar um documento com namespaces no Visual Basic-LINQ to XML
description: Use literais XML no Visual Basic para criar documentos que tenham namespaces ou namespaces padrão com um prefixo.
ms.date: 07/20/2015
ms.assetid: cc5b0d4d-360c-4ada-94fa-2d2916e989be
ms.openlocfilehash: 48e2a1abf8f7a82df3db5cb2f580804d67776b15
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552021"
---
# <a name="how-to-create-a-document-with-namespaces-in-visual-basic-linq-to-xml"></a>Como criar um documento com namespaces no Visual Basic (LINQ to XML)

Este artigo mostra como criar um documento com namespaces no Visual Basic.

Ao usar literais XML no Visual Basic, os usuários podem definir um namespace XML global padrão. Este namespace é o namespace padrão para literais XML e propriedades XML. O namespace XML padrão pode ser definida no nível de projeto ou nível de arquivo. Se ele for definido no nível do arquivo, ele substituirá o namespace padrão no nível do projeto.

Você também pode definir namespaces, e especifica os prefixos de namespace para esses namespaces. Você usa a `Imports` palavra-chave para definir os dois tipos de namespace.

Para obter mais informações, consulte [literais XML no Visual Basic](xml-literals.md).

Observe que o namespace XML padrão se aplica somente aos elementos e não a atributos. Os atributos são, por padrão, no namespace padrão. No entanto, você pode usar um prefixo de namespace para colocar um atributo em um namespace.

## <a name="example-create-a-document-that-has-a-namespace"></a>Exemplo: criar um documento que tem um namespace

Este exemplo cria um documento que contém um namespace.

```vb
Imports <xmlns:aw="http://www.adventure-works.com">
Module Module1
    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <aw:Child aw:Att="attvalue"/>
            </aw:Root>
        Console.WriteLine(root)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```xml
<aw:Root xmlns:aw="http://www.adventure-works.com">
  <aw:Child aw:Att="attvalue" />
</aw:Root>
```

## <a name="example-create-a-document-that-has-two-namespaces-one-with-a-prefix"></a>Exemplo: criar um documento que tem dois namespaces, um com um prefixo

Este exemplo cria um documento que contém dois namespaces. Um é o namespace padrão, o outro tem um prefixo.

```vb
Imports <xmlns="http://www.adventure-works.com">
Imports <xmlns:fc="www.fourthcoffee.com">

Module Module1

    Sub Main()
        Dim root As XElement = _
            <Root>
                <Child Att="attvalue"/>
                <fc:Child2>child2 content</fc:Child2>
            </Root>
        Console.WriteLine(root)
    End Sub

End Module
```

Esse exemplo gera a saída a seguir:

```xml
<Root xmlns:fc="www.fourthcoffee.com" xmlns="http://www.adventure-works.com">
  <Child Att="attvalue" />
  <fc:Child2>child2 content</fc:Child2>
</Root>
```

## <a name="example-create-a-document-that-has-two-namespaces-both-with-prefixes"></a>Exemplo: criar um documento que tem dois namespaces, ambos com prefixos

O exemplo a seguir cria um documento que contém dois namespaces, ambos tendo os prefixos de namespace.

Ao serializar uma árvore XML, LINQ to XML emite declarações de namespace conforme necessário para que cada elemento esteja no namespace designado.

```vb
Imports <xmlns:aw="http://www.adventure-works.com">
Imports <xmlns:fc="www.fourthcoffee.com">

Module Module1

    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <fc:Child>
                    <aw:DifferentChild>other content</aw:DifferentChild>
                </fc:Child>
                <aw:Child2>c2 content</aw:Child2>
                <fc:Child3>c3 content</fc:Child3>
            </aw:Root>
        Console.WriteLine(root)
    End Sub

End Module
```

Esse exemplo gera a saída a seguir:

```xml
<aw:Root xmlns:fc="www.fourthcoffee.com" xmlns:aw="http://www.adventure-works.com">
  <fc:Child>
    <aw:DifferentChild>other content</aw:DifferentChild>
  </fc:Child>
  <aw:Child2>c2 content</aw:Child2>
  <fc:Child3>c3 content</fc:Child3>
</aw:Root>
```

## <a name="see-also"></a>Confira também

- [Visão geral dos namespaces](namespaces-overview.md)
