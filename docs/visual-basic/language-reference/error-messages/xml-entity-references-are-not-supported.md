---
description: 'Saiba mais sobre: BC31180: não há suporte para referências de entidade XML'
title: As referências de entidade XML não são suportadas
ms.date: 07/20/2015
f1_keywords:
- vbc31180
- bc31180
helpviewer_keywords:
- BC31180
ms.assetid: 2a393327-d8e2-4187-85b1-642b4f53b4ae
ms.openlocfilehash: c45202fbd97d2343caf6bf4cdccf9368d0a7a295
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701411"
---
# <a name="bc31180-xml-entity-references-are-not-supported"></a>BC31180: não há suporte para referências de entidade XML

Uma referência de entidade (por exemplo, `©` ) que não está definida na especificação XML 1,0 é incluída como um valor para um literal XML. Somente `&` as `"` `<` referências de entidade XML,,, `>` e `'` são suportadas em literais XML.

 **ID do erro:** BC31180

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Remova a referência de entidade sem suporte.

## <a name="see-also"></a>Consulte também

- [Especificação dos literais XML e do XML 1.0](../../programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)
- [Literais XML](../xml-literals/index.md)
- [XML](../../programming-guide/language-features/xml/index.md)
