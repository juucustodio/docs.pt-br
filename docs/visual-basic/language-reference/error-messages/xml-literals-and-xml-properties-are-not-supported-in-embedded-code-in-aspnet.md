---
description: 'Saiba mais sobre: BC31200: não há suporte para literais XML e propriedades XML no código inserido dentro do ASP.NET'
title: Literais e propriedades de XML não são suportados em código inserido dentro do ASP.NET
ms.date: 07/20/2015
f1_keywords:
- vbc31200
- bc31200
helpviewer_keywords:
- BC31200
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
ms.openlocfilehash: 0a5328676ee38a56334b77f665a464daa586ce3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701398"
---
# <a name="bc31200-xml-literals-and-xml-properties-are-not-supported-in-embedded-code-within-aspnet"></a>BC31200: não há suporte para literais XML e propriedades XML no código inserido dentro do ASP.NET

Não há suporte para literais XML e propriedades XML no código inserido dentro de ASP.NET. Para usar recursos XML, mova o código para code-behind.

 Uma propriedade XML literal ou XML Axis é definida no código inserido ( `<%= =>` ) em um arquivo ASP.net.

 **ID do erro:** BC31200

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Mova o código que inclui o literal XML ou a propriedade de eixo XML para um arquivo code-behind ASP.NET.

## <a name="see-also"></a>Consulte também

- [Literais XML](../xml-literals/index.md)
- [Propriedades do eixo XML](../xml-axis/index.md)
- [XML](../../programming-guide/language-features/xml/index.md)
