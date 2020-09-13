---
title: Preservar espaço em branco ao serializar-LINQ to XML
description: Você pode controlar o espaço em branco de várias maneiras ao serializar uma árvore XML.
ms.date: 07/20/2015
ms.assetid: 0c4f8b98-483b-4cf8-86be-fa146eef90dc
ms.openlocfilehash: 6d907e68a2df3905794b555954330f31b5e75655
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551903"
---
# <a name="preserve-white-space-while-serializing-linq-to-xml"></a>Preservar espaço em branco ao serializar (LINQ to XML)

Este artigo descreve como controlar o espaço em branco ao serializar uma árvore XML.

Um cenário comum é ler XML recuado, criar uma árvore XML na memória sem nenhum nó de texto de espaço em branco (ou seja, não preservar espaço em branco), executar algumas operações no XML e, em seguida, salvar o XML com recuo. Quando você serializa o XML com formatação, somente os espaços em branco significativos na árvore XML são preservados. Esse é o comportamento padrão para LINQ to XML.

Outro cenário comum é ler e modificar XML que já foi recuado intencionalmente. Você pode não querer modificar este recuo de nenhuma forma. Para fazer isso no LINQ to XML, você preserva o espaço em branco quando carrega ou analisa o XML e desabilita a formatação ao serializar o XML.

## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>Comportamento de espaço em branco de métodos que serializam árvores XML

Os seguintes métodos nas classes de <xref:System.Xml.Linq.XElement> e de <xref:System.Xml.Linq.XDocument> serialize uma árvore XML. Você pode serializar uma árvore XML para um arquivo, um <xref:System.IO.TextReader>, ou um <xref:System.Xml.XmlReader>. O método de `ToString` serializa a uma cadeia de caracteres.

- <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>
- [XElement.ToString()](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)
- [XDocument.ToString()](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)

Se o método não usar <xref:System.Xml.Linq.SaveOptions> como um argumento, o método formatará (recuará) o XML serializado. Nesse caso, qualquer espaço em branco irrisória na árvore XML é descartado.

Se o método utiliza <xref:System.Xml.Linq.SaveOptions> como um argumento, então você pode especificar que o formato de método não (corte XML serializável.) Nesse caso, qualquer espaço em branco na árvore XML é preservada.
