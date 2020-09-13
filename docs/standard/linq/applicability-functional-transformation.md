---
title: Aplicabilidade da transformação funcional-LINQ to XML
description: Saiba quando você pode fazer uso de transformações funcionais.
ms.date: 07/20/2015
ms.assetid: c78107bd-b006-4574-a3d4-bbf808388ff3
ms.openlocfilehash: cfba2a32887891cd4b735c76e940ff2400e55bef
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552032"
---
# <a name="applicability-of-functional-transformation-linq-to-xml"></a>Aplicabilidade da transformação funcional (LINQ to XML)

Transformações e puras são aplicáveis em uma variedade de situações.

A abordagem funcional de transformação é mais idealmente consultando e manipulando dados; estruturados portanto couber bem com as tecnologias LINQ. No entanto, a transformação funcional tem uma aplicabilidade muito maior do que o uso com LINQ. Alguns processam onde o foco principal está em transformar dados de um formulário para outro provavelmente deve ser considerado como um candidato para a transformação funcional.

Essa abordagem é aplicável a muitos problemas que não podem parecer à primeira vista para ser um candidato. Usado em conjunto ou separadamente com LINQ, a transformação funcional deve ser considerada para as seguintes áreas:

- Documentos com base em XML. Os dados bem formado do dialeto de XML podem facilmente ser manipulados pela transformação funcional. Para obter mais informações, consulte [transformação funcional do XML](functional-transformation-xml.md).
- Outros formatos de arquivo estruturados. De Windows.ini arquivos aos documentos de texto sem formatação, a maioria dos arquivos têm qualquer estrutura que se empresta a análise e a transformação.
- Os protocolos de streaming de dados. Os dados de codificação e nos dados de decodificação dos protocolos de comunicação geralmente podem ser representados por um funcional simples tornam-se.
- Dados de RDBMS e de OODBMS. Os bases de dados relacionais e orientados a objeto, assim como XML, são estruturados fontes de dados amplamente usadas.
- Matemático, estatística, e soluções de ciência. Esses campos tendem a manipular grandes conjuntos de dados para ajudar o usuário em visualizar, em estimar, ou realmente em resolver problemas não triviais.

Conforme descrito em [Refactor em funções puras](refactor-pure-functions.md), o uso de funções puras é um exemplo de programação funcional. Em adicional a seus benefícios imediatos, usar funções puras fornece a experiência valiosa no pensamento sobre problemas de uma perspectiva funcional de transformação. Essa abordagem pode também ter o impacto principal no design do programa e da classe. Isso é especialmente verdadeiro quando um problema se empresta a uma solução de transformação de dados como descrito acima.

Embora estejam além do escopo deste tutorial, os designs que são influenciados pela perspectiva de transformação funcional tendem a ser centralizado em processos mais do que em objetos como atores, e a solução resultante tende a ser implementada como uma série de transformações em larga escala, em vez de alterações de estado de objeto individual.

 Além disso, lembre-se que C# e Visual Basic suportam abordagens imperativas e funcional, o melhor design do seu aplicativo pode inserir os elementos de ambos.

## <a name="see-also"></a>Confira também

- [Introdução às transformações funcionais puras](introduction-pure-functional-transformations.md)
- [Transformação funcional do XML](functional-transformation-xml.md)
- [Refatorar em funções puras](refactor-pure-functions.md)
