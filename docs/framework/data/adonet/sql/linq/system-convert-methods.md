---
description: 'Saiba mais sobre: métodos System. Convert'
title: Métodos de System.Convert
ms.date: 03/30/2017
ms.assetid: 3ca6c5b6-ea5d-4ab0-b675-f082135b342c
ms.openlocfilehash: a323f8d0c3c4a8d1248409d2ec27565acdc58222
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681403"
---
# <a name="systemconvert-methods"></a>Métodos de System.Convert

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não oferece suporte aos seguintes métodos de <xref:System.Convert> .

- Versões com um parâmetro de <xref:System.IFormatProvider> .

- Métodos que envolvem matrizes de char ou matrizes de bytes:

  - <xref:System.Convert.FromBase64CharArray%2A>

  - <xref:System.Convert.ToBase64CharArray%2A>

  - <xref:System.Convert.FromBase64String%2A>

  - <xref:System.Convert.ToBase64String%2A>

- Os seguintes métodos:

  - `public static <Type2> To<Type2>(<Type1> value);` em que

    `Type1` e `Type2` são cada um de `sbyte`, `uint`, `ulong`, ou `ushort`.

  - C#:

    `int To<int type>(string value, int fromBase),`

    `ToString(... value, int toBase)`

  - Visual Basic:

    `Function To(Of [Numeric])(value as String, fromBase As Integer)`

    `As [Numeric], ToString( value As …, toBase As Integer)`

  - <xref:System.Convert.IsDBNull%2A>

  - <xref:System.Convert.GetTypeCode%2A>

  - <xref:System.Convert.ChangeType%2A>

## <a name="see-also"></a>Consulte também

- [Tipos de dados e funções](data-types-and-functions.md)
