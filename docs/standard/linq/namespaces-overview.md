---
title: Visão geral dos namespaces-LINQ to XML
description: Saiba mais sobre nomes XML, namespaces XML e prefixos de namespace XML e sobre as classes XName e XNamespace.
ms.date: 07/20/2015
ms.assetid: 16283322-8238-4918-ab11-802ac6748eb7
ms.openlocfilehash: 81fe678a8d6be32461c675cc527595033e826165
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551926"
---
# <a name="namespaces-overview-linq-to-xml"></a>Visão geral de namespaces (LINQ to XML)

Este artigo apresenta *nomes XML*, *namespaces XML*, *prefixos de namespace XML*e <xref:System.Xml.Linq.XName> <xref:System.Xml.Linq.XNamespace> classes e.

Os nomes XML são geralmente uma fonte de complexidade na programação XML. Um nome de XML consiste em um namespace XML (também chamado um URI de um namespace XML) e um nome local. Um namespace XML é semelhante a um namespace em um programa .NET. Ele permite qualificar exclusivamente os nomes de elementos e atributos para evitar conflitos de nome entre várias partes de um documento XML. Quando você declarou um namespace XML, você pode selecionar um nome local que só precisa ser exclusivo dentro desse namespace.

Outro aspecto dos nomes XML são os prefixos de namespace XML, que causam a maior parte da complexidade de nomes XML. Esses prefixos permite que você crie um atalho para um namespace XML, que faz o documento XML mais concisas e legível. No entanto, o significado de um prefixo XML depende do contexto, o que adiciona complexidade. Por exemplo, o prefixo XML `aw` pode ser associado a um namespace XML em parte de uma árvore XML e com um namespace diferente em outra parte.

Uma das vantagens de usar o LINQ to XML com o C# é que você não precisa usar prefixos XML. Quando LINQ to XML carrega ou analisa um documento XML, cada prefixo XML é resolvido para seu namespace XML correspondente. Após isso, quando você trabalha com um documento que usar namespaces, você acessa quase sempre namespaces com o URI de namespace, e não com o prefixo de namespace. Quando os desenvolvedores trabalham com nomes XML em LINQ to XML eles sempre trabalham com um nome XML totalmente qualificado (ou seja, um namespace XML e um nome local). No entanto, o LINQ to XML permite que você trabalhe e controle os prefixos de namespace conforme necessário.

Ao usar LINQ to XML com literais Visual Basic e XML, você deve usar prefixos de namespace ao trabalhar com documentos em namespaces.

No LINQ to XML, a classe que representa os nomes XML é <xref:System.Xml.Linq.XName> . Os nomes de XML aparecem frequentemente em toda a API de LINQ to XML e sempre que um nome XML é necessário, você encontrará um <xref:System.Xml.Linq.XName> parâmetro. No entanto, raramente você trabalha diretamente com um <xref:System.Xml.Linq.XName>. <xref:System.Xml.Linq.XName> contém uma conversão implícita de cadeia de caracteres.

Para obter mais informações, consulte <xref:System.Xml.Linq.XNamespace> e <xref:System.Xml.Linq.XName>.
