---
title: Serializar para arquivos, textwriters e xmlwriters-LINQ to XML
description: Você pode serializar árvores XML para um arquivo, um TextWriter ou um XmlWriter, e pode serializar qualquer componente XML, incluindo XDocument e XElement, para uma cadeia de caracteres usando o método ToString.
ms.date: 07/20/2015
ms.assetid: bd3ea6f7-895b-4ff4-a625-fe2bb55b1886
ms.openlocfilehash: 20651c06a759d83934c4b035a42eac7c2700eb9f
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552318"
---
# <a name="serialize-to-files-textwriters-and-xmlwriters-linq-to-xml"></a>Serializar para arquivos, textwriters e xmlwriters (LINQ to XML)

Você pode serializar árvores XML a <xref:System.IO.File>, a <xref:System.IO.TextWriter>, ou a <xref:System.Xml.XmlWriter>.

Você pode serializar qualquer componente XML, incluindo <xref:System.Xml.Linq.XDocument> e <xref:System.Xml.Linq.XElement>, uma cadeia de caracteres usando o método `ToString` .

Se você desejar suprimir formatação ao serializar a uma cadeia de caracteres, você pode usar o método de <xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType> .

O comportamento padrão ao serializar para um arquivo é formatar (recuar) o documento XML resultante. Quando você recua, o espaço em branco insignificante na árvore XML não é preservado. Para serializar com a formatação, use uma das sobrecargas dos seguintes métodos que não assumem <xref:System.Xml.Linq.SaveOptions> como um argumento:

- <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>

Se você desejar que a opção não recuar e não preservar espaço em branco irrisória na árvore XML, use uma das sobrecargas dos seguintes métodos que leva <xref:System.Xml.Linq.SaveOptions> como um argumento:

- <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>

Para obter exemplos, consulte o artigo de referência apropriado.
