---
title: Preservar espaço em branco ao carregar ou analisar LINQ to XML XML
description: Você pode controlar o comportamento de espaço em branco dos métodos LINQ to XML que populam árvores XML. Por exemplo, você pode remover o recuo para processamento na memória ou deixá-lo como está.
ms.date: 07/20/2015
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
ms.openlocfilehash: 783a1198f0b1754c690f04159860056a0fbadeb4
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551910"
---
# <a name="preserve-white-space-while-loading-or-parsing-xml-linq-to-xml"></a>Preservar espaço em branco ao carregar ou analisar XML (LINQ to XML)

Este artigo descreve como controlar o comportamento de espaço em branco de LINQ to XML.

Um cenário comum é ler XML recuado, criar uma árvore XML na memória sem nenhum nó de texto de espaço em branco (ou seja, não preservar espaço em branco), executar algumas operações no XML e, em seguida, salvar o XML com recuo. Quando você serializa o XML com formatação, somente os espaços em branco significativos na árvore XML são preservados. Esse é o comportamento padrão para LINQ to XML.

Outro cenário comum é ler e modificar XML que já foi recuado intencionalmente. Você pode não querer modificar este recuo de nenhuma forma. Para fazer isso no LINQ to XML, você preserva o espaço em branco quando carrega ou analisa o XML e desabilita a formatação ao serializar o XML.

Este artigo descreve o comportamento de espaço em branco dos métodos que populam árvores XML. Para obter informações sobre como controlar o espaço em branco ao serializar árvores XML, consulte [Preservar espaço em branco ao serializar](preserve-white-space-serializing.md).

## <a name="behavior-of-methods-that-populate-xml-trees"></a>Comportamento de métodos que populam árvores XML

Os seguintes métodos nas classes de <xref:System.Xml.Linq.XElement> e de <xref:System.Xml.Linq.XDocument> preenchem uma árvore XML. Você pode preencher uma árvore XML de um arquivo, um <xref:System.IO.TextReader>, um <xref:System.Xml.XmlReader>, ou de uma cadeia de caracteres:

- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>

Se o método não usar <xref:System.Xml.Linq.LoadOptions> como um argumento, o método não preservará espaço em branco insignificante.

Na maioria dos casos, se o método utiliza <xref:System.Xml.Linq.LoadOptions> como um argumento, você pode opcionalmente preservar espaço em branco irrisória como nós de texto na árvore XML. Entretanto, se o método é carregar XML de <xref:System.Xml.XmlReader>, então <xref:System.Xml.XmlReader> determina se o espaço em branco será preservada ou não. A configuração <xref:System.Xml.Linq.LoadOptions.PreserveWhitespace> não terá efeito.

Com esses métodos, se o espaço em branco é preservada, o espaço em branco irrisória é inserido na árvore XML como nós de <xref:System.Xml.Linq.XText> . Se o espaço em branco não for preservado, os nós de texto não serão inseridos.

Você pode criar uma árvore XML usando <xref:System.Xml.XmlWriter>. Os nós que são gravados em <xref:System.Xml.XmlWriter> são preenchidos na árvore. No entanto, quando você cria uma árvore XML usando esse método, todos os nós são mantidos, independentemente se o nó é o espaço em branco ou não, ou se o espaço em branco é significativo ou não.
