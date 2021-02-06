---
description: 'Saiba mais sobre: design de campo'
title: Design de campo
ms.date: 10/22/2008
helpviewer_keywords:
- fields, design guidelines
- read-only fields
- member design guidelines, fields
ms.assetid: 7cb4b0f3-7a10-4c93-b84d-733f7134fcf8
ms.openlocfilehash: 88df60c3050035221dc65429bbd543c71d5d69b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99642039"
---
# <a name="field-design"></a>Design de campo

O princípio do encapsulamento é uma das noções mais importantes no design orientado a objeto. Esse princípio determina que os dados armazenados dentro de um objeto devem ser acessíveis somente para esse objeto.

 Uma maneira útil de interpretar o princípio é dizer que um tipo deve ser projetado de forma que as alterações em campos desse tipo (nome ou alterações de tipo) possam ser feitas sem a quebra de código além dos membros do tipo. Essa interpretação implica imediatamente que todos os campos devem ser privados.

 Nós excluímos campos somente leitura e constantes da constante, pois esses campos, quase por definição, nunca precisam ser alterados.

 ❌ Não forneça campos de instância públicos ou protegidos.

 Você deve fornecer propriedades para acessar campos em vez de torná-las públicas ou protegidas.

 ✔️ usar campos constantes para constantes que nunca serão alteradas.

 O compilador grava os valores de campos const diretamente no código de chamada. Portanto, os valores const nunca podem ser alterados sem o risco de perder a compatibilidade.

 ✔️ usar campos estáticos públicos `readonly` para instâncias de objeto predefinidos.

 Se houver instâncias predefinidas do tipo, declare-as como campos estáticos somente leitura públicos do próprio tipo.

 ❌ Não atribua instâncias de tipos mutáveis a `readonly` campos.

 Um tipo mutável é um tipo com instâncias que podem ser modificadas depois de terem sido instanciadas. Por exemplo, matrizes, a maioria das coleções e fluxos são tipos mutáveis, mas <xref:System.Int32?displayProperty=nameWithType> , <xref:System.Uri?displayProperty=nameWithType> e <xref:System.String?displayProperty=nameWithType> são todos imutáveis. O modificador somente leitura em um campo de tipo de referência impede que a instância armazenada no campo seja substituída, mas não impede que os dados de instância do campo sejam modificados chamando Membros que alteram a instância.

 *Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*

 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*

## <a name="see-also"></a>Confira também

- [Diretrizes de design de membro](member.md)
- [Diretrizes de design de estrutura](index.md)
