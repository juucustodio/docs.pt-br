---
title: Recursos de nomenclatura
description: Examine as diretrizes de nomenclatura para recursos no .NET, que são semelhantes às diretrizes para nomear Propriedades.
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], localized resources
- localization, naming guidelines
- resource names
- global applications, naming guidelines
- international applications, naming guidelines
ms.assetid: 8b0e97f3-7877-44fd-bc76-e05d36d5d79c
ms.openlocfilehash: 08046fb78638546b3dcab856674424c92c03fe83
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706405"
---
# <a name="naming-resources"></a>Recursos de nomenclatura

Como os recursos localizáveis podem ser referenciados por meio de determinados objetos como se fossem Propriedades, as diretrizes de nomenclatura para recursos são semelhantes às diretrizes de propriedade.

 ✔️ usar PascalCasing em chaves de recurso.

 ✔️ fornecem identificadores descritivos, em vez de curtos.

 ❌ Não use palavras-chave específicas de idioma das principais linguagens do CLR.

 ✔️ usar somente caracteres alfanuméricos e sublinhados na nomenclatura de recursos.

 ✔️ Use a seguinte convenção de nomenclatura para recursos de mensagem de exceção.

 O identificador de recurso deve ser o nome do tipo de exceção, além de um identificador curto da exceção:

 `ArgumentExceptionIllegalCharacters` `ArgumentExceptionInvalidName`
 `ArgumentExceptionFileNameIsMalformed`

 *Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*

 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*

## <a name="see-also"></a>Confira também

- [Diretrizes de design de estrutura](index.md)
- [Diretrizes de nomenclatura](naming-guidelines.md)
