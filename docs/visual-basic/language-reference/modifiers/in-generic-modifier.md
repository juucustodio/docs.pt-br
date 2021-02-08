---
description: 'Saiba mais sobre: in (modificador genérico) (Visual Basic)'
title: In (modificador genérico)-Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.VarianceIn
helpviewer_keywords:
- contravariance, In keyword [Visual Basic]
- In keyword [Visual Basic]
ms.assetid: 59bb13c5-fe96-42b8-8286-86293d1661c5
ms.openlocfilehash: e6ac95a77253b28e45a4be8a29623bdd76a231f1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774532"
---
# <a name="in-generic-modifier-visual-basic"></a>In (modificador genérico) (Visual Basic)

Para parâmetros de tipo genérico, a palavra-chave `In` especifica que o parâmetro de tipo é contravariante.

## <a name="remarks"></a>Comentários

A contravariância permite que você use um tipo menos derivado do que aquele especificado pelo parâmetro genérico. Isso permite a conversão implícita de classes que implementam interfaces variantes e a conversão implícita de tipos delegados.

Para obter mais informações, consulte [Covariância e contravariância](../../programming-guide/concepts/covariance-contravariance/index.md).

## <a name="rules"></a>Regras

Você pode usar a palavra-chave `In` em delegados e interfaces genéricas.
  
Um parâmetro de tipo pode ser declarado contravariant em uma interface genérica ou delegado se for usado apenas como um tipo de argumento de método e não usado como um tipo de retorno de método. `ByRef` os parâmetros não podem ser covariant ou contravariant.

Covariance e contravariância têm suporte para tipos de referência e não têm suporte para tipos de valor.

No Visual Basic, você não pode declarar eventos em interfaces contravariant sem especificar o tipo delegado. Além disso, as interfaces contravariant não podem ter classes aninhadas, enums ou estruturas, mas podem ter interfaces aninhadas.

## <a name="behavior"></a>Comportamento

Uma interface que tem um parâmetro de tipo contravariante permite que os seus métodos aceitem argumentos de tipos menos derivados que aqueles especificados pelo parâmetro de tipo de interface. Por exemplo, como no .NET Framework 4, na <xref:System.Collections.Generic.IComparer%601> interface, o tipo T é contravariant, você pode atribuir um objeto do `IComparer(Of Person)` tipo a um objeto do `IComparer(Of Employee)` tipo sem usar nenhum método de conversão especial se `Employee` herdar de `Person` .

Um delegado contravariante pode ser atribuído a outro delegado do mesmo tipo, mas com um parâmetro de tipo genérico menos derivado.

## <a name="example---contravariant-generic-interface"></a>Exemplo – interface genérica contravariant

O exemplo a seguir mostra como declarar, estender e implementar uma interface genérica contravariante. Ele também mostra como você pode usar a conversão implícita para classes que implementam essa interface.

[!code-vb[vbVarianceKeywords#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#1)]

## <a name="example---contravariant-generic-delegate"></a>Exemplo – delegado genérico contravariant

O exemplo a seguir mostra como declarar, instanciar e invocar um delegado genérico contravariante. Ele também mostra como você pode converter implicitamente um tipo delegado.

[!code-vb[vbVarianceKeywords#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#2)]

## <a name="see-also"></a>Consulte também

- [Variação em interfaces genéricas](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [Fora](out-generic-modifier.md)
