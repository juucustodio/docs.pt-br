---
title: Transformação funcional de XML-LINQ to XML
description: Saiba mais sobre a abordagem de transformação funcional pura para modificar documentos XML e como ele difere de uma abordagem de procedimento.
ms.date: 07/20/2015
ms.assetid: 0ccb9251-38d7-44e3-9b84-1b5fe25e4b59
ms.openlocfilehash: b23288e013a4104b21523e17e1f266a9f712c451
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551884"
---
# <a name="functional-transformation-of-xml-linq-to-xml"></a>Transformação funcional do XML (LINQ to XML)

Este artigo aborda a abordagem de transformação funcional pura para modificar documentos XML e o contrasta com uma abordagem de procedimento.

## <a name="modifying-an-xml-document"></a>Modificando um documento XML

Uma das tarefas mais comuns para um programador XML está transformando XML de uma forma para outra. A forma de um documento XML é a estrutura do documento, que inclui o seguinte:

- A hierarquia expressa pelo documento.
- Nomes de elementos e atributos.
- Os tipos de dados de elementos e atributos.

Em geral, a abordagem mais eficiente para transformar XML de uma forma para outra é a de transformação funcional pura. Nessa abordagem, a tarefa principal do programador é criar uma transformação que é aplicada ao documento XML inteiro (ou a um ou mais nós estritamente definido). A transformação funcional é teoricamente a mais fácil de código (após um programador estiver familiarizado com a abordagem), produz o código o mais sustentável, e é geralmente mais compacta de abordagens alternativas.

### <a name="xml-functional-transformational-technologies"></a>Tecnologias de transformação funcionais XML

A Microsoft oferece duas tecnologias funcionais de transformação para uso em documentos XML: XSLT e LINQ to XML. XSLT é suportado no namespace gerenciada <xref:System.Xml.Xsl> e na implementação nativo COM de MSXML. Embora XSLT é uma tecnologia robusta para documentos XML de tratamento, requer a experiência em um domínio especializado, como o idioma XSLT e seus APIs de suporte.

LINQ to XML fornece as ferramentas necessárias codificação transformações e puras de uma maneira poderosa completo expressive e, em C# ou de código Visual Basic. Por exemplo, muitos dos exemplos o uso da documentação LINQ to XML uma abordagem funcional pura. Além disso, no tutorial [: manipulando conteúdo em um documento do WordprocessingML](xml-shape-wordprocessingml-documents.md) , usamos LINQ to XML em uma abordagem funcional para manipular informações em um documento do Microsoft Word.

Para obter uma comparação mais completa de LINQ to XML com outras tecnologias XML da Microsoft, consulte [LINQ to XML vs. outras tecnologias XML](linq-xml-vs-xml-technologies.md).

XSLT a ferramenta é recomendada para transformações um documento céntricas quando o documento de origem tem uma estrutura denteada. No entanto, LINQ to XML também pode executar um documento centralizado em transformações. Para obter mais informações, consulte [como usar anotações para transformar LINQ to XML árvores em um estilo XSLT](use-annotations-transform-linq-xml-trees-xslt-style.md).

## <a name="see-also"></a>Confira também

- [Introdução às transformações funcionais puras](introduction-pure-functional-transformations.md)
- [Tutorial: manipular conteúdo em um documento do WordprocessingML](xml-shape-wordprocessingml-documents.md)
- [LINQ to XML vs. outras tecnologias XML](linq-xml-vs-xml-technologies.md)
