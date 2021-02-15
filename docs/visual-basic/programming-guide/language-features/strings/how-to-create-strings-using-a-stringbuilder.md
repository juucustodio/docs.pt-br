---
description: 'Saiba mais sobre: como criar cadeias de caracteres usando um StringBuilder no Visual Basic'
title: 'Como: criar cadeias de caracteres usando um StringBuilder'
ms.date: 07/20/2015
helpviewer_keywords:
- StringBuilder class
- strings [Visual Basic], using StringBuilder
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
ms.openlocfilehash: 6def32517f71ec3c2a7795c3395e3e572903ce1e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429813"
---
# <a name="how-to-create-strings-using-a-stringbuilder-in-visual-basic"></a>Como: criar cadeias de caracteres usando um StringBuilder no Visual Basic

Este exemplo constrói uma cadeia de caracteres longa a partir de muitas cadeias de caracteres menores usando a <xref:System.Text.StringBuilder> classe. A <xref:System.Text.StringBuilder> classe é mais eficiente do que o `&=` operador para concatenar muitas cadeias de caracteres.

## <a name="example"></a>Exemplo

O exemplo a seguir cria uma instância da <xref:System.Text.StringBuilder> classe, acrescenta 1.000 cadeias de caracteres a essa instância e, em seguida, retorna sua representação de cadeia de caracteres:

 [!code-vb[VbVbalrStrings#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#70)]

## <a name="see-also"></a>Consulte também

- [Uso da classe StringBuilder](../../../../standard/base-types/stringbuilder.md)
- [ Operador&=](../../../language-reference/operators/and-assignment-operator.md)
- [Cadeias de caracteres](index.md)
- [Criar novas cadeias de caracteres](../../../../standard/base-types/creating-new.md)
- [Manipular cadeias de caracteres](../../../../standard/base-types/best-practices-strings.md)
