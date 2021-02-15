---
description: 'Saiba mais sobre: BC30033: o identificador é muito longo'
title: O identificador é muito longo
ms.date: 07/20/2015
f1_keywords:
- bc30033
- vbc30033
helpviewer_keywords:
- BC30033
ms.assetid: 3d07f6d0-9a2f-49ca-94e8-1e354932e855
ms.openlocfilehash: f2439c4bfc53f906fdc277b0de1faac0941c8808
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796087"
---
# <a name="bc30033-identifier-is-too-long"></a>BC30033: o identificador é muito longo

O nome, ou identificador, de cada elemento de programação é limitado a 1023 caracteres. Além disso, um nome totalmente qualificado não pode exceder 1023 caracteres. Isso significa que toda a cadeia de caracteres do identificador ( `<namespace>.<...>.<namespace>.<class>.<element>` ) não pode ter mais de 1023 caracteres, incluindo os caracteres do operador de acesso para membro ( `.` ).

 **ID do erro:** BC30033

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Reduza o comprimento do identificador.

## <a name="see-also"></a>Consulte também

- [Nomes de elementos declarados](../../programming-guide/language-features/declared-elements/declared-element-names.md)
