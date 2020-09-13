---
title: LINQ to XML vs. outras tecnologias XML
description: Saiba como LINQ to XML se compara ao XSLT, ao MSXML e ao XmlLite para fazer melhores escolhas de tecnologia.
ms.date: 07/20/2015
ms.assetid: 01b8e746-12d3-471d-b811-7539e4547784
ms.openlocfilehash: ac118543bd1101e50edfcf99a609a715b885bfbd
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552014"
---
# <a name="linq-to-xml-vs-other-xml-technologies"></a>LINQ to XML vs. outras tecnologias XML

Este artigo compara LINQ to XML com as seguintes tecnologias XML: <xref:System.Xml.XmlReader> , XSLT, MSXML e XmlLite. Essas informações podem ajudá-lo a decidir quais tecnologias usar.

Para obter uma comparação de LINQ to XML para o Modelo de Objeto do Documento (DOM), consulte [LINQ to XML vs. Dom](linq-xml-vs-dom.md).

## <a name="linq-to-xml-vs-xmlreader"></a>LINQ to XML vs. XmlReader

A classe <xref:System.Xml.XmlReader> é um analisador rápido, somente encaminhamento e não armazenado em cache.

O LINQ to XML é implementado na parte superior do <xref:System.Xml.XmlReader> e está totalmente integrado. No entanto, você também pode usar o <xref:System.Xml.XmlReader> diretamente.

Por exemplo, suponha que você esteja criando um serviço Web que analisará centenas de documentos XML por segundo e que os documentos tenham a mesma estrutura, o que significa que você só precisa escrever uma implementação do código para analisar o XML. Nesse caso, você provavelmente desejaria usar <xref:System.Xml.XmlReader> diretamente.

Por outro lado, se você estiver criando um sistema que analisa muitos documentos XML menores, e cada um deles for diferente, você desejará aproveitar as melhorias de produtividade que o LINQ to XML fornece.

## <a name="linq-to-xml-vs-xslt"></a>LINQ to XML vs. XSLT

O LINQ to XML e o XSLT fornecem recursos extensivos de transformação de documentos XML. A linguagem XSLT é uma abordagem declarativa baseada em regras. Programadores avançados de XSLT criam XSLT em um estilo funcional de programação que enfatiza uma abordagem sem estado. As transformações podem ser criadas com o uso de funções puras que são implementadas sem efeitos colaterais. Essa abordagem funcional baseada em regras é desconhecida para muitos desenvolvedores e sua compreensão pode ser difícil e demorada.

O XSLT pode ser um sistema produtivo que produz aplicativos de alto desempenho. Por exemplo, algumas grandes empresas Web usam o XSLT como uma maneira de gerar HTML a partir de XML que foi extraído de diferentes tipos de armazenamentos de dados. O mecanismo XSLT gerenciado compila o XSLT no código Common Language Runtime (CLR) e executa ainda melhor em alguns cenários do que o mecanismo XSLT nativo.

No entanto, o XSLT não aproveita o C# e Visual Basic conhecimento que muitos desenvolvedores têm. Ela requer que os desenvolvedores criem código em uma linguagem de programação diferente e complexa. O uso de dois sistemas de desenvolvimento não integrados, como C# (ou Visual Basic) e XSLT, resulta em sistemas de software que são mais difíceis de desenvolver e manter.

Depois de dominar LINQ to XML expressões de consulta, as transformações de LINQ to XML são uma tecnologia poderosa que é fácil de usar. Basicamente, você forma seu documento XML usando construção funcional, extraindo dados de várias fontes, construindo objetos <xref:System.Xml.Linq.XElement> dinamicamente e montando o todo em uma nova árvore XML. A transformação pode gerar um documento completamente novo. A construção de transformações no LINQ to XML é relativamente fácil e intuitiva, e o código resultante é legível. Isso reduz custos de desenvolvimento e de manutenção.

LINQ to XML não se destina a substituir o XSLT. O XSLT ainda é a ferramenta preferida para transformações XML complicadas e centradas em documentos, especialmente se a estrutura do documento não estiver bem definida.

A linguagem XSLT tem a vantagem de ser um padrão W3C (World Wide Web Consortium). Se você tiver um requisito de usar apenas tecnologias que sejam padrões, a linguagem XSLT pode ser mais apropriada.

O XSLT é XML e é por isso que pode ser manipulado de forma programática.

## <a name="linq-to-xml-vs-msxml"></a>LINQ to XML vs. MSXML

O MSXML é a tecnologia baseada em COM para o processamento de XML que está incluído no Microsoft Windows. A tecnologia MSXML fornece uma implementação nativa do DOM com suporte para XPath e XSLT. Ela também contém o analisador SAX2 baseado em eventos e não armazenado em cache.

O MSXML também tem um bom desempenho, é seguro por padrão na maioria dos cenários e pode ser acessado no Internet Explorer para fazer o processamento de XML do lado do cliente em aplicativos estilo AJAX. A MSXML pode ser usada por meio de qualquer linguagem de programação que seja compatível com o COM, incluindo C++, JavaScript e Visual Basic 6.0.

O MSXML não é recomendado para uso em código gerenciado com base no CLR.

## <a name="linq-to-xml-vs-xmllite"></a>LINQ to XML vs. XmlLite

XmlLite é um analisador de pull, somente encaminhamento e não armazenado em cache. Os desenvolvedores usam XmlLite principalmente com C++. Não é recomendável para os desenvolvedores usar o XmlLite com código gerenciado.

A principal vantagem do XmlLite é que ele é um analisador XML leve e rápido que é seguro na maioria dos cenários. Sua área de superfície de ameaça é pequena. Se você precisar analisar documentos não confiáveis e quiser protegê-los contra ataques de negação de serviço ou da exibição de dados, XmlLite pode ser uma boa opção.

O XmlLite não está integrado à LINQ (consulta integrada à linguagem). Ele não produz os aprimoramentos de produtividade do programador que são a força motivadora por trás do LINQ.

## <a name="see-also"></a>Confira também

- [Visão geral de LINQ to XML](linq-xml-overview.md)
