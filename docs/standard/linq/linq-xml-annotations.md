---
title: Anotações-LINQ to XML
description: Saiba como usar anotações no LINQ to XML para associar qualquer objeto arbitrário de qualquer tipo arbitrário a qualquer componente XML em uma árvore XML.
ms.date: 07/20/2015
ms.assetid: 54e7b9d0-07f5-488f-9065-b6e6b870f810
ms.openlocfilehash: 80710b3596fc37ed76f23e31d1d781c64d0bc909
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551986"
---
# <a name="linq-to-xml-annotations-linq-to-xml"></a>LINQ to XML anotações (LINQ to XML)

As anotações no LINQ to XML permitem que você associe qualquer objeto arbitrário de qualquer tipo arbitrário a qualquer componente XML em uma árvore XML.

Para adicionar uma anotação a um componente XML, como <xref:System.Xml.Linq.XElement> ou <xref:System.Xml.Linq.XAttribute>, você chama o método de <xref:System.Xml.Linq.XObject.AddAnnotation%2A> . Você recupera anotações pelo tipo.

Observe que as anotações não fazem parte do XML infoset; Eles não são serializados ou desserializados.

## <a name="methods"></a>Métodos

Você pode usar os seguintes métodos para trabalhar com anotações:

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XObject.AddAnnotation%2A>|Adiciona um objeto à lista de anotação de <xref:System.Xml.Linq.XObject>.|
|<xref:System.Xml.Linq.XObject.Annotation%2A>|Obtém o primeiro objeto de anotação do tipo especificado de <xref:System.Xml.Linq.XObject>.|
|<xref:System.Xml.Linq.XObject.Annotations%2A>|Obtém uma coleção de anotações do tipo especificado para <xref:System.Xml.Linq.XObject>.|
|<xref:System.Xml.Linq.XObject.RemoveAnnotations%2A>|Remove as anotações do tipo especificado de <xref:System.Xml.Linq.XObject>.|
