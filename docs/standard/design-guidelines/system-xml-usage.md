---
description: 'Saiba mais sobre: uso de System.Xml'
title: Uso de System.XML
ms.date: 10/22/2008
ms.assetid: 82302f0d-a621-4c6f-b57d-999bd61f21a6
ms.openlocfilehash: 51886c07f0b68bb329c258daa93e809d94839341
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641844"
---
# <a name="systemxml-usage"></a>Uso de System.XML

Esta seção fala sobre o uso de vários tipos que residem em <xref:System.Xml?displayProperty=nameWithType> namespaces que podem ser usados para representar dados XML.

 ❌ Não use <xref:System.Xml.XmlNode> ou <xref:System.Xml.XmlDocument> para representar dados XML. Favorecer o uso de instâncias de <xref:System.Xml.XPath.IXPathNavigable> , <xref:System.Xml.XmlReader> , <xref:System.Xml.XmlWriter> ou subtipos de <xref:System.Xml.Linq.XNode> em vez disso. `XmlNode` e `XmlDocument` não são projetados para exposição em APIs públicas.

 ✔️ usar `XmlReader` , `IXPathNavigable` ou subtipos de `XNode` como entrada ou saída de membros que aceitam ou retornam XML.

 Use essas abstrações em vez de `XmlDocument` , `XmlNode` ou <xref:System.Xml.XPath.XPathDocument> , porque isso dissocia os métodos de implementações específicas de um documento XML na memória e permite que eles trabalhem com fontes de dados XML virtuais que expõem `XNode` , `XmlReader` ou <xref:System.Xml.XPath.XPathNavigator> .

 ❌ Não crie a subclasse `XmlDocument` se você quiser criar um tipo que represente uma exibição XML de um modelo de objeto subjacente ou fonte de dados.

 *Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*

 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*

## <a name="see-also"></a>Confira também

- [Diretrizes de design de estrutura](index.md)
- [Diretrizes de uso](usage-guidelines.md)
