---
title: Conteúdo válido de objetos XElement e XDocument-LINQ to XML
description: Os construtores XElement e XDocument aceitam muitos tipos de argumentos, incluindo coleções retornadas de consultas. Há outros construtores e funções para adicionar conteúdo XML.
ms.date: 07/20/2015
ms.assetid: 0d253586-2b97-459f-b1a7-f30f38f3ed9f
ms.openlocfilehash: e0288dce06f8040385c9b9a30335fd039d3c45bd
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552302"
---
# <a name="valid-content-of-xelement-and-xdocument-objects-linq-to-xml"></a>Conteúdo válido de objetos XElement e XDocument (LINQ to XML)

Este artigo descreve os argumentos válidos que podem ser passados para construtores e métodos que você usa para adicionar conteúdo a elementos e documentos.

## <a name="valid-types-for-the-xelement-constructor"></a>Tipos válidos para o construtor XElement

As consultas geralmente avaliam para <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement> ou <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XAttribute>. Você pode passar coleções de <xref:System.Xml.Linq.XElement> ou de objetos <xref:System.Xml.Linq.XAttribute> para o construtor de <xref:System.Xml.Linq.XElement>. É por isso que é conveniente passar os resultados de uma consulta como conteúdo em métodos e construtores que você usa para popular árvores XML.

Ao adicionar conteúdo simples, vários tipos podem ser passados para esse método, incluindo::

- <xref:System.String>
- <xref:System.Double>
- <xref:System.Single>
- <xref:System.Decimal>
- <xref:System.Boolean>
- <xref:System.DateTime>
- <xref:System.TimeSpan>
- <xref:System.DateTimeOffset>
- Qualquer tipo que implemente `Object.ToString`.
- Qualquer tipo que implemente <xref:System.Collections.Generic.IEnumerable%601>.

Ao adicionar conteúdo complexo, vários tipos podem ser passados para esse método, incluindo:

- <xref:System.Xml.Linq.XObject>
- <xref:System.Xml.Linq.XNode>
- <xref:System.Xml.Linq.XAttribute>
- Qualquer tipo que implementa <xref:System.Collections.Generic.IEnumerable%601>

Se um objeto implementar <xref:System.Collections.Generic.IEnumerable%601>, a coleção no objeto será enumerada, e todos os itens da coleção serão adicionados. Se a coleção contiver objetos <xref:System.Xml.Linq.XNode> ou <xref:System.Xml.Linq.XAttribute>, cada item da coleção será adicionado separadamente. Se a coleção contiver texto (ou objetos que são convertidos em texto), o texto da coleção será concatenado e adicionado como um único nó de texto.

Se o conteúdo for `null`, nada será adicionado. Ao passar uma coleção, os itens na coleção podem ser `null` . Um item `null` na coleção não tem nenhum efeito na árvore.

Um atributo adicionado deve ter um nome exclusivo dentro do elemento que o contém.

Ao adicionar objetos <xref:System.Xml.Linq.XNode> ou <xref:System.Xml.Linq.XAttribute>, se o novo conteúdo não tiver um pai, os objetos serão simplesmente anexados à árvore XML. Se o novo conteúdo já tiver um pai e fizer parte de outra árvore XML, o novo conteúdo será clonado, e o conteúdo recém-clonado será anexado à árvore XML.

## <a name="valid-types-for-the-xdocument-constructor"></a>Tipos válidos para o Construtor XDocument

Atributos e conteúdo simples não podem ser adicionados a um documento.

Não há muitos cenários que exigem a criação de um <xref:System.Xml.Linq.XDocument> . Em vez disso, você normalmente pode criar suas árvores XML com um nó raiz de <xref:System.Xml.Linq.XElement>. A menos que você tenha um requisito específico para criar um documento (por exemplo, porque você precisa criar instruções de processamento e comentários no nível superior, ou você precisa dar suporte a tipos de documento), muitas vezes é mais conveniente usar <xref:System.Xml.Linq.XElement> como seu nó raiz.

Os tipos válidos para o <xref:System.Xml.Linq.XDocument.%23ctor%2A> Construtor incluem o seguinte:

- Zero ou um objeto <xref:System.Xml.Linq.XDocumentType>. Os tipos de documento devem vir antes do elemento.
- Zero ou um elemento.
- Zero ou mais comentários.
- Zero ou mais instruções de processamento.
- Zero ou mais nós de texto que contêm somente espaço em branco.

## <a name="constructors-and-functions-for-adding-content"></a>Construtores e funções para adicionar conteúdo

Os métodos a seguir permitem adicionar conteúdo filho a um <xref:System.Xml.Linq.XElement> ou a um <xref:System.Xml.Linq.XDocument>:

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XElement.%23ctor%2A>|Constrói um <xref:System.Xml.Linq.XElement>.|
|<xref:System.Xml.Linq.XDocument.%23ctor%2A>|Constrói um <xref:System.Xml.Linq.XDocument>.|
|<xref:System.Xml.Linq.XContainer.Add%2A>|Adiciona ao final do conteúdo filho do <xref:System.Xml.Linq.XElement> ou do <xref:System.Xml.Linq.XDocument>.|
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Adiciona conteúdo depois de <xref:System.Xml.Linq.XNode>.|
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Adiciona conteúdo antes de <xref:System.Xml.Linq.XNode>.|
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|Adiciona conteúdo ao início do conteúdo filho de <xref:System.Xml.Linq.XContainer>.|
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A>|Substitui todo o conteúdo (nós filho e atributos) de um <xref:System.Xml.Linq.XElement>.|
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A>|Substitui os atributos de um <xref:System.Xml.Linq.XElement>.|
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A>|Substitui os nós filho pelo novo conteúdo.|
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A>|Substitui um nó pelo novo conteúdo.|

## <a name="see-also"></a>Confira também

- [Árvores XML](functional-construction.md)
