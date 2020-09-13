---
title: Modificando elementos, atributos e nós em uma árvore XML
description: Saiba mais sobre métodos e propriedades que você pode usar para modificar um elemento, seus nós filho ou seus atributos.
ms.date: 07/20/2015
ms.assetid: 0ed22e4e-4c6b-4eb1-b0eb-06685efd8c33
ms.openlocfilehash: 671ba38350e443d95c92a9bd790eac3d2deb5cdd
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552296"
---
# <a name="modify-elements-attributes-and-nodes-in-an-xml-tree-linq-to-xml"></a>Modificar elementos, atributos e nós em uma árvore XML (LINQ to XML)

A tabela a seguir resume os métodos e as propriedades que você pode usar para modificar um elemento, seus elementos filho ou seus atributos.

Os métodos a seguir modificam um <xref:System.Xml.Linq.XElement> :

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>|Substitui um elemento pelo XML analisado.|
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|Remove todo o conteúdo (nós filho e atributos) de um elemento.|
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|Remove os atributos de um elemento.|
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A?displayProperty=nameWithType>|Substitui todo o conteúdo (nós filho e atributos) de um elemento.|
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A?displayProperty=nameWithType>|Substitui os atributos de um elemento.|
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|Define o valor de um atributo. Cria o atributo se ele não existir. Se o valor for definido como `null`, o método removerá o atributo.|
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|Define o valor de um elemento filho. Cria o elemento se ele não existir. Se o valor for definido como `null`, o método removerá o elemento.|
|<xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType>|Substitui o conteúdo (nós filho) de um elemento pelo texto especificado.|
|<xref:System.Xml.Linq.XElement.SetValue%2A?displayProperty=nameWithType>|Define o valor de um elemento.|

Os métodos a seguir modificam um <xref:System.Xml.Linq.XAttribute> :

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType>|Define o valor de um atributo.|
|<xref:System.Xml.Linq.XAttribute.SetValue%2A?displayProperty=nameWithType>|Define o valor de um atributo.|

 Os métodos a seguir modificam um <xref:System.Xml.Linq.XNode> (incluindo um <xref:System.Xml.Linq.XElement> ou <xref:System.Xml.Linq.XDocument> ):

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A?displayProperty=nameWithType>|Substitui um nó pelo novo conteúdo.|

 Os métodos a seguir modificam um <xref:System.Xml.Linq.XContainer> (a <xref:System.Xml.Linq.XElement> <xref:System.Xml.Linq.XDocument> ):

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A?displayProperty=nameWithType>|Substitui os nós filhos por um novo conteúdo:|
