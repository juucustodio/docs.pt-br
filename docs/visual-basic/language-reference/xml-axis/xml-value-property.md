---
description: 'Saiba mais sobre: propriedade de valor XML (Visual Basic)'
title: Propriedade do Valor XML
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionValue
helpviewer_keywords:
- Value property [Visual Basic]
- Visual Basic code, accessing XML
- XML axis [Visual Basic], Value
- XML Value property [Visual Basic]
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
ms.openlocfilehash: 49762c1fcc0059472a5be11726aa344a001807ea
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99768760"
---
# <a name="xml-value-property-visual-basic"></a>Propriedade do valor XML (Visual Basic)

Fornece acesso ao valor do primeiro elemento de uma coleção de <xref:System.Xml.Linq.XElement> objetos.

## <a name="syntax"></a>Syntax

```vb
object.Value
```

## <a name="parts"></a>Partes

|Termo|Definição|  
|---|---|  
|`object`|Obrigatório. Coleção de objetos <xref:System.Xml.Linq.XElement>.|  

## <a name="return-value"></a>Valor retornado

 Uma `String` que contém o valor do primeiro elemento da coleção ou `Nothing` se a coleção estiver vazia.

## <a name="remarks"></a>Comentários

 A <xref:System.Xml.Linq.XElement.Value%2A> Propriedade facilita o acesso ao valor do primeiro elemento em uma coleção de <xref:System.Xml.Linq.XElement> objetos. Essa propriedade verifica primeiro se a coleção contém pelo menos um objeto. Se a coleção estiver vazia, essa propriedade retornará `Nothing` . Caso contrário, essa propriedade retornará o valor da <xref:System.Xml.Linq.XElement.Value%2A> Propriedade do primeiro elemento na coleção.

> [!NOTE]
> Quando você acessa o valor de um atributo XML usando o \@ identificador ' ', o valor do atributo é retornado como um `String` e você não precisa especificar explicitamente a <xref:System.Xml.Linq.XAttribute.Value%2A> propriedade.

 Para acessar outros elementos em uma coleção, você pode usar a propriedade do indexador de extensão XML. Para obter mais informações, consulte [Propriedade do indexador de extensão](extension-indexer-property.md).

## <a name="inheritance"></a>Herança

 A maioria dos usuários não precisará implementar <xref:System.Collections.Generic.IEnumerable%601> e, portanto, pode ignorar esta seção.

 A <xref:System.Xml.Linq.XElement.Value%2A> propriedade é uma propriedade de extensão para tipos que implementam `IEnumerable(Of XElement)` . A associação dessa propriedade de extensão é como a associação de métodos de extensão: se um tipo implementar uma das interfaces e definir uma propriedade com o nome "valor", essa propriedade terá precedência sobre a propriedade de extensão. Em outras palavras, essa <xref:System.Xml.Linq.XElement.Value%2A> propriedade pode ser substituída definindo-se uma nova propriedade em uma classe que implementa `IEnumerable(Of XElement)` .

## <a name="example"></a>Exemplo

 O exemplo a seguir mostra como usar a <xref:System.Xml.Linq.XElement.Value%2A> propriedade para acessar o primeiro nó em uma coleção de <xref:System.Xml.Linq.XElement> objetos. O exemplo usa a propriedade do eixo filho para obter a coleção de todos os nós filho chamados `phone` que estão no `contact` objeto.

 [!code-vb[VbXMLSamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#15)]

 Esse código exibe o seguinte texto:

 `Phone number: 206-555-0144`

## <a name="example"></a>Exemplo

 O exemplo a seguir mostra como obter o valor de um atributo XML de uma coleção de <xref:System.Xml.Linq.XAttribute> objetos. O exemplo usa a Propriedade Axis do atributo para exibir o valor do `type` atributo para todos os `phone` elementos.

 [!code-vb[VbXMLSamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#16)]

 Esse código exibe o seguinte texto:

 ```console
 home
 work
```

## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XElement>
- <xref:System.Collections.Generic.IEnumerable%601>
- [Propriedades do eixo XML](index.md)
- [Literais XML](../xml-literals/index.md)
- [Criando XML no Visual Basic](../../programming-guide/language-features/xml/creating-xml.md)
- [Métodos de Extensão](../../programming-guide/language-features/procedures/extension-methods.md)
- [Propriedade do Indexador de Extensão](extension-indexer-property.md)
- [Propriedade do Eixo Filho XML](xml-child-axis-property.md)
- [Propriedade de Eixo do Atributo XML](xml-attribute-axis-property.md)
