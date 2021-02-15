---
description: 'Saiba mais sobre: design de classe abstrata'
title: Design de classe abstrata
ms.date: 10/22/2008
helpviewer_keywords:
- type design guidelines, abstract classes
- abstract classes, design guidelines
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], abstract
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
ms.openlocfilehash: 5b1cd833bf43e5bf5731176243809393187e84d4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99642455"
---
# <a name="abstract-class-design"></a>Design de classe abstrata

❌ Não defina construtores internos públicos ou protegidos em tipos abstratos.

 Os construtores só devem ser públicos se os usuários precisarem criar instâncias do tipo. Como não é possível criar instâncias de um tipo abstrato, um tipo abstrato com um construtor público é projetado incorretamente e induzindo aos usuários.

 ✔️ definir um construtor protegido ou interno em classes abstratas.

 Um construtor protegido é mais comum e simplesmente permite que a classe base faça sua própria inicialização quando os subtipos são criados.

 Um construtor interno pode ser usado para limitar implementações concretas da classe abstrata ao assembly que define a classe.

 ✔️ fornece pelo menos um tipo concreto que herda de cada classe abstrata que você envia.

 Fazer isso ajuda a validar o design da classe abstrata. Por exemplo,  <xref:System.IO.FileStream?displayProperty=nameWithType> é uma implementação da <xref:System.IO.Stream?displayProperty=nameWithType> classe abstract.

 *Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*

 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*

## <a name="see-also"></a>Confira também

- [Diretrizes de design de tipo](type.md)
- [Diretrizes de design de estrutura](index.md)
